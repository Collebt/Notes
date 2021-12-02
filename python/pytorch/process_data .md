#### dataset

```python
class PascalVOCKeypoints(InMemoryDataset):
    r"""The Pascal VOC 2011 dataset with Berkely annotations of keypoints from
    the `"Poselets: Body Part Detectors Trained Using 3D Human Pose
    Annotations" <https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/
    human/ poselets_iccv09.pdf>`_ paper, containing 0 to 23 keypoints per
    example over 20 categories.
    The dataset is pre-filtered to exclude difficult, occluded and truncated
    objects.
    The keypoints contain interpolated features from a pre-trained VGG16 model
    on ImageNet (:obj:`relu4_2` and :obj:`relu5_1`).

    Args:
        root (string): Root directory where the dataset should be saved.
        category (string): The category of the images (one of
            :obj:`"Aeroplane"`, :obj:`"Bicycle"`, :obj:`"Bird"`,
            :obj:`"Boat"`, :obj:`"Bottle"`, :obj:`"Bus"`, :obj:`"Car"`,
            :obj:`"Cat"`, :obj:`"Chair"`, :obj:`"Diningtable"`, :obj:`"Dog"`,
            :obj:`"Horse"`, :obj:`"Motorbike"`, :obj:`"Person"`,
            :obj:`"Pottedplant"`, :obj:`"Sheep"`, :obj:`"Sofa"`,
            :obj:`"Train"`, :obj:`"TVMonitor"`)
        train (bool, optional): If :obj:`True`, loads the training dataset,
            otherwise the test dataset. (default: :obj:`True`)
        transform (callable, optional): A function/transform that takes in an
            :obj:`torch_geometric.data.Data` object and returns a transformed
            version. The data object will be transformed before every access.
            (default: :obj:`None`)
        pre_transform (callable, optional): A function/transform that takes in
            an :obj:`torch_geometric.data.Data` object and returns a
            transformed version. The data object will be transformed before
            being saved to disk. (default: :obj:`None`)
        pre_filter (callable, optional): A function that takes in an
            :obj:`torch_geometric.data.Data` object and returns a boolean
            value, indicating whether the data object should be included in the
            final dataset. (default: :obj:`None`)
    """
    image_url = ('http://host.robots.ox.ac.uk/pascal/VOC/voc2011/'
                 'VOCtrainval_25-May-2011.tar')
    annotation_url = ('https://www2.eecs.berkeley.edu/Research/Projects/CS/'
                      'vision/shape/poselets/voc2011_keypoints_Feb2012.tgz')
    # annotation_url = 'http://www.roemisch-drei.de/pascal_annotations.tar'
    # split_url = 'http://cvgl.stanford.edu/projects/ucn/voc2011_pairs.npz'
    split_url = ('https://github.com/Thinklab-SJTU/PCA-GM/raw/master/data/'
                 'PascalVOC/voc2011_pairs.npz')

    categories = [
        'aeroplane', 'bicycle', 'bird', 'boat', 'bottle', 'bus', 'car', 'cat',
        'chair', 'cow', 'diningtable', 'dog', 'horse', 'motorbike', 'person',
        'pottedplant', 'sheep', 'sofa', 'train', 'tvmonitor'
    ]

    device = 'cuda' if torch.cuda.is_available() else 'cpu'
    batch_size = 8

    def __init__(self, root, category, train=True, transform=None,
                 pre_transform=None, pre_filter=None):
        self.category = category.lower()
        assert self.category in self.categories
        super(PascalVOCKeypoints, self).__init__(root, transform,
                                                 pre_transform, pre_filter)
        path = self.processed_paths[0] if train else self.processed_paths[1]
        self.data, self.slices = torch.load(path)

    @property
    def raw_dir(self):
        return osp.join(self.root, 'raw')

    @property
    def processed_dir(self):
        return osp.join(self.root, self.category.capitalize(), 'processed')

    @property
    def raw_file_names(self):
        return ['images', 'annotations', 'splits.npz']

    @property
    def processed_file_names(self):
        return ['training.pt', 'test.pt']

    def download(self):
        path = download_url(self.image_url, self.raw_dir)
        extract_tar(path, self.raw_dir, mode='r')
        os.unlink(path)
        image_path = osp.join(self.raw_dir, 'TrainVal', 'VOCdevkit', 'VOC2011')
        os.rename(image_path, osp.join(self.raw_dir, 'images'))
        shutil.rmtree(osp.join(self.raw_dir, 'TrainVal'))

        path = download_url(self.annotation_url, self.raw_dir)
        extract_tar(path, self.raw_dir, mode='r')
        os.unlink(path)

        path = download_url(self.split_url, self.raw_dir)
        os.rename(path, osp.join(self.raw_dir, 'splits.npz'))

    def process(self):
        if models is None or T is None or Image is None:
            raise ImportError('Package `torchvision` could not be found.')

        splits = np.load(osp.join(self.raw_dir, 'splits.npz'),
                         allow_pickle=True)
        category_idx = self.categories.index(self.category)
        train_split = list(splits['train'])[category_idx]
        test_split = list(splits['test'])[category_idx]

        image_path = osp.join(self.raw_dir, 'images', 'JPEGImages')
        info_path = osp.join(self.raw_dir, 'images', 'Annotations')
        annotation_path = osp.join(self.raw_dir, 'annotations')

        labels = {}

        vgg16_outputs = []

        def hook(module, x, y):
            vgg16_outputs.append(y)

        vgg16 = models.vgg16(pretrained=True).to(self.device)
        vgg16.eval()
        vgg16.features[20].register_forward_hook(hook)  # relu4_2
        vgg16.features[25].register_forward_hook(hook)  # relu5_1

        transform = T.Compose([
            T.ToTensor(),
            T.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])
        ])

        train_set, test_set = [], []
        for i, name in enumerate(chain(train_split, test_split)):
            filename = '_'.join(name.split('/')[1].split('_')[:-1])
            idx = int(name.split('_')[-1].split('.')[0]) - 1

            path = osp.join(info_path, '{}.xml'.format(filename))
            obj = minidom.parse(path).getElementsByTagName('object')[idx]

            trunc = obj.getElementsByTagName('truncated')[0].firstChild.data
            occ = obj.getElementsByTagName('occluded')
            occ = '0' if len(occ) == 0 else occ[0].firstChild.data
            diff = obj.getElementsByTagName('difficult')[0].firstChild.data

            if bool(int(trunc)) or bool(int(occ)) or bool(int(diff)):
                continue

            if self.category == 'person' and int(filename[:4]) > 2008:
                continue

            xmin = float(obj.getElementsByTagName('xmin')[0].firstChild.data)
            xmax = float(obj.getElementsByTagName('xmax')[0].firstChild.data)
            ymin = float(obj.getElementsByTagName('ymin')[0].firstChild.data)
            ymax = float(obj.getElementsByTagName('ymax')[0].firstChild.data)
            box = (xmin, ymin, xmax, ymax)

            dom = minidom.parse(osp.join(annotation_path, name))
            keypoints = dom.getElementsByTagName('keypoint')

            if len(keypoints) < 3:
                continue
            poss, ys = [], []
            for keypoint in keypoints:
                label = keypoint.attributes['name'].value
                if label not in labels:
                    labels[label] = len(labels)
                ys.append(labels[label])
                x = float(keypoint.attributes['x'].value)
                y = float(keypoint.attributes['y'].value)
                poss += [x, y]
            y = torch.tensor(ys, dtype=torch.long)
            pos = torch.tensor(poss, dtype=torch.float).view(-1, 2)

            if pos.numel() == 0:
                continue  # These examples do not make any sense anyway...

            # Add a small offset to the bounding because some keypoints lay
            # outside the bounding box intervals.
            box = (min(pos[:, 0].min().floor().item(), box[0]) - 16,
                   min(pos[:, 1].min().floor().item(), box[1]) - 16,
                   max(pos[:, 0].max().ceil().item(), box[2]) + 16,
                   max(pos[:, 1].max().ceil().item(), box[3]) + 16)

            # Rescale keypoints.
            pos[:, 0] = (pos[:, 0] - box[0]) * 256.0 / (box[2] - box[0])
            pos[:, 1] = (pos[:, 1] - box[1]) * 256.0 / (box[3] - box[1])

            path = osp.join(image_path, '{}.jpg'.format(filename))
            with open(path, 'rb') as f:
                img = Image.open(f).convert('RGB').crop(box)
                img = img.resize((256, 256), resample=Image.BICUBIC)

            img = transform(img)

            data = Data(img=img, pos=pos, y=y, name=filename)
            # print(data)

            if i < len(train_split):
                train_set.append(data)
            else:
                test_set.append(data)

        data_list = list(chain(train_set, test_set))
        imgs = [data.img for data in data_list]
        loader = DataLoader(imgs, self.batch_size, shuffle=False)
        for i, batch_img in enumerate(loader):
            vgg16_outputs.clear()

            with torch.no_grad():
                vgg16(batch_img.to(self.device))

            out1 = F.interpolate(vgg16_outputs[0], (256, 256), mode='bilinear',
                                 align_corners=False)
            out2 = F.interpolate(vgg16_outputs[1], (256, 256), mode='bilinear',
                                 align_corners=False)

            for j in range(out1.size(0)):
                data = data_list[i * self.batch_size + j]
                idx = data.pos.round().long().clamp(0, 255)
                x_1 = out1[j, :, idx[:, 1], idx[:, 0]].to('cpu')
                x_2 = out2[j, :, idx[:, 1], idx[:, 0]].to('cpu')
                data.img = None
                data.x = torch.cat([x_1.t(), x_2.t()], dim=-1)
            del out1
            del out2

        if self.pre_filter is not None:
            train_set = [data for data in train_set if self.pre_filter(data)]
            test_set = [data for data in test_set if self.pre_filter(data)]

        if self.pre_transform is not None:
            train_set = [self.pre_transform(data) for data in train_set]
            test_set = [self.pre_transform(data) for data in test_set]

        torch.save(self.collate(train_set), self.processed_paths[0])
        torch.save(self.collate(test_set), self.processed_paths[1])

    def __repr__(self):
        return '{}({}, category={})'.format(self.__class__.__name__, len(self),
                                            self.category)

```

#### in memory 

```python
class InMemoryDataset(Dataset):
    r"""Dataset base class for creating graph datasets which fit completely
    into CPU memory.
    See `here <https://pytorch-geometric.readthedocs.io/en/latest/notes/
    create_dataset.html#creating-in-memory-datasets>`__ for the accompanying
    tutorial.

    Args:
        root (string, optional): Root directory where the dataset should be
            saved. (default: :obj:`None`)
        transform (callable, optional): A function/transform that takes in an
            :obj:`torch_geometric.data.Data` object and returns a transformed
            version. The data object will be transformed before every access.
            (default: :obj:`None`)
        pre_transform (callable, optional): A function/transform that takes in
            an :obj:`torch_geometric.data.Data` object and returns a
            transformed version. The data object will be transformed before
            being saved to disk. (default: :obj:`None`)
        pre_filter (callable, optional): A function that takes in an
            :obj:`torch_geometric.data.Data` object and returns a boolean
            value, indicating whether the data object should be included in the
            final dataset. (default: :obj:`None`)
    """
    @property
    def raw_file_names(self) -> Union[str, List[str], Tuple]:
        r"""The name of the files to find in the :obj:`self.raw_dir` folder in
        order to skip the download."""
        raise NotImplementedError

    @property
    def processed_file_names(self) -> Union[str, List[str], Tuple]:
        r"""The name of the files to find in the :obj:`self.processed_dir`
        folder in order to skip the processing."""
        raise NotImplementedError

    def download(self):
        r"""Downloads the dataset to the :obj:`self.raw_dir` folder."""
        raise NotImplementedError

    def process(self):
        r"""Processes the dataset to the :obj:`self.processed_dir` folder."""
        raise NotImplementedError

    def __init__(self, root: Optional[str] = None,
                 transform: Optional[Callable] = None,
                 pre_transform: Optional[Callable] = None,
                 pre_filter: Optional[Callable] = None):
        super().__init__(root, transform, pre_transform, pre_filter)
        self.data = None
        self.slices = None
        self._data_list: Optional[List[Data]] = None

    @property
    def num_classes(self) -> int:
        r"""The number of classes in the dataset."""
        y = self.data.y
        if y is None:
            return 0
        elif y.numel() == y.size(0) and not torch.is_floating_point(y):
            return int(self.data.y.max()) + 1
        elif y.numel() == y.size(0) and torch.is_floating_point(y):
            return torch.unique(y).numel()
        else:
            return self.data.y.size(-1)

    def len(self) -> int:
        for item in self.slices.values():
            return len(item) - 1
        return 0

    def get(self, idx: int) -> Data:
        if hasattr(self, '_data_list'):
            if self._data_list is None:
                self._data_list = self.len() * [None]
            else:
                data = self._data_list[idx]
                if data is not None:
                    return copy.copy(data)

        data = self.data.__class__()
        if hasattr(self.data, '__num_nodes__'):
            data.num_nodes = self.data.__num_nodes__[idx]

        for key in self.data.keys:
            item, slices = self.data[key], self.slices[key]
            start, end = slices[idx].item(), slices[idx + 1].item()
            if torch.is_tensor(item):
                s = list(repeat(slice(None), item.dim()))
                cat_dim = self.data.__cat_dim__(key, item)
                if cat_dim is None:
                    cat_dim = 0
                s[cat_dim] = slice(start, end)
            elif start + 1 == end:
                s = slices[start]
            else:
                s = slice(start, end)
            data[key] = item[s]

        if hasattr(self, '_data_list'):
            self._data_list[idx] = copy.copy(data)

        return data

    @staticmethod
    def collate(data_list: List[Data]) -> Tuple[Data, Dict[str, Tensor]]:
        r"""Collates a python list of data objects to the internal storage
        format of :class:`torch_geometric.data.InMemoryDataset`."""
        keys = data_list[0].keys
        data = data_list[0].__class__()

        for key in keys:
            data[key] = []
        slices = {key: [0] for key in keys}

        for item, key in product(data_list, keys):
            data[key].append(item[key])
            if isinstance(item[key], Tensor) and item[key].dim() > 0:
                cat_dim = item.__cat_dim__(key, item[key])
                cat_dim = 0 if cat_dim is None else cat_dim
                s = slices[key][-1] + item[key].size(cat_dim)
            else:
                s = slices[key][-1] + 1
            slices[key].append(s)

        if hasattr(data_list[0], '__num_nodes__'):
            data.__num_nodes__ = []
            for item in data_list:
                data.__num_nodes__.append(item.num_nodes)

        for key in keys:
            item = data_list[0][key]
            if isinstance(item, Tensor) and len(data_list) > 1:
                if item.dim() > 0:
                    cat_dim = data.__cat_dim__(key, item)
                    cat_dim = 0 if cat_dim is None else cat_dim
                    data[key] = torch.cat(data[key], dim=cat_dim)
                else:
                    data[key] = torch.stack(data[key])
            elif isinstance(item, Tensor):  # Don't duplicate attributes...
                data[key] = data[key][0]
            elif isinstance(item, int) or isinstance(item, float):
                data[key] = torch.tensor(data[key])

            slices[key] = torch.tensor(slices[key], dtype=torch.long)

        return data, slices

    def copy(self, idx: Optional[IndexType] = None):
        if idx is None:
            data_list = [self.get(i) for i in range(len(self))]
        else:
            data_list = [self.get(i) for i in self.index_select(idx).indices()]

        dataset = copy.copy(self)
        dataset._indices = None
        dataset._data_list = data_list
        dataset.data, dataset.slices = self.collate(data_list)
        return dataset
```

#### Dataset

```python
class Dataset(torch.utils.data.Dataset):
    r"""Dataset base class for creating graph datasets.
    See `here <https://pytorch-geometric.readthedocs.io/en/latest/notes/
    create_dataset.html>`__ for the accompanying tutorial.

    Args:
        root (string, optional): Root directory where the dataset should be
            saved. (optional: :obj:`None`)
        transform (callable, optional): A function/transform that takes in an
            :obj:`torch_geometric.data.Data` object and returns a transformed
            version. The data object will be transformed before every access.
            (default: :obj:`None`)
        pre_transform (callable, optional): A function/transform that takes in
            an :obj:`torch_geometric.data.Data` object and returns a
            transformed version. The data object will be transformed before
            being saved to disk. (default: :obj:`None`)
        pre_filter (callable, optional): A function that takes in an
            :obj:`torch_geometric.data.Data` object and returns a boolean
            value, indicating whether the data object should be included in the
            final dataset. (default: :obj:`None`)
    """
    @property
    def raw_file_names(self) -> Union[str, List[str], Tuple]:
        r"""The name of the files to find in the :obj:`self.raw_dir` folder in
        order to skip the download."""
        raise NotImplementedError

    @property
    def processed_file_names(self) -> Union[str, List[str], Tuple]:
        r"""The name of the files to find in the :obj:`self.processed_dir`
        folder in order to skip the processing."""
        raise NotImplementedError

    def download(self):
        r"""Downloads the dataset to the :obj:`self.raw_dir` folder."""
        raise NotImplementedError

    def process(self):
        r"""Processes the dataset to the :obj:`self.processed_dir` folder."""
        raise NotImplementedError

    def len(self) -> int:
        raise NotImplementedError

    def get(self, idx: int) -> Data:
        r"""Gets the data object at index :obj:`idx`."""
        raise NotImplementedError

    def __init__(self, root: Optional[str] = None,
                 transform: Optional[Callable] = None,
                 pre_transform: Optional[Callable] = None,
                 pre_filter: Optional[Callable] = None):
        super().__init__()

        if isinstance(root, str):
            root = osp.expanduser(osp.normpath(root))

        self.root = root
        self.transform = transform
        self.pre_transform = pre_transform
        self.pre_filter = pre_filter
        self._indices: Optional[Sequence] = None

        if 'download' in self.__class__.__dict__.keys():
            self._download()

        if 'process' in self.__class__.__dict__.keys():
            self._process()

    def indices(self) -> Sequence:
        return range(self.len()) if self._indices is None else self._indices

    @property
    def raw_dir(self) -> str:
        return osp.join(self.root, 'raw')

    @property
    def processed_dir(self) -> str:
        return osp.join(self.root, 'processed')

    @property
    def num_node_features(self) -> int:
        r"""Returns the number of features per node in the dataset."""
        data = self[0]
        if hasattr(data, 'num_node_features'):
            return data.num_node_features
        raise AttributeError(f"'{data.__class__.__name__}' object has no "
                             f"attribute 'num_node_features'")

    @property
    def num_features(self) -> int:
        r"""Alias for :py:attr:`~num_node_features`."""
        return self.num_node_features

    @property
    def num_edge_features(self) -> int:
        r"""Returns the number of features per edge in the dataset."""
        data = self[0]
        if hasattr(data, 'num_edge_features'):
            return data.num_edge_features
        raise AttributeError(f"'{data.__class__.__name__}' object has no "
                             f"attribute 'num_edge_features'")

    @property
    def raw_paths(self) -> List[str]:
        r"""The filepaths to find in order to skip the download."""
        files = to_list(self.raw_file_names)
        return [osp.join(self.raw_dir, f) for f in files]

    @property
    def processed_paths(self) -> List[str]:
        r"""The filepaths to find in the :obj:`self.processed_dir`
        folder in order to skip the processing."""
        files = to_list(self.processed_file_names)
        return [osp.join(self.processed_dir, f) for f in files]

    def _download(self):
        if files_exist(self.raw_paths):  # pragma: no cover
            return

        makedirs(self.raw_dir)
        self.download()

    def _process(self):
        f = osp.join(self.processed_dir, 'pre_transform.pt')
        if osp.exists(f) and torch.load(f) != _repr(self.pre_transform):
            warnings.warn(
                f"The `pre_transform` argument differs from the one used in "
                f"the pre-processed version of this dataset. If you want to "
                f"make use of another pre-processing technique, make sure to "
                f"sure to delete '{self.processed_dir}' first")

        f = osp.join(self.processed_dir, 'pre_filter.pt')
        if osp.exists(f) and torch.load(f) != _repr(self.pre_filter):
            warnings.warn(
                "The `pre_filter` argument differs from the one used in the "
                "pre-processed version of this dataset. If you want to make "
                "use of another pre-fitering technique, make sure to delete "
                "'{self.processed_dir}' first")

        if files_exist(self.processed_paths):  # pragma: no cover
            return

        print('Processing...')

        makedirs(self.processed_dir)
        self.process()

        path = osp.join(self.processed_dir, 'pre_transform.pt')
        torch.save(_repr(self.pre_transform), path)
        path = osp.join(self.processed_dir, 'pre_filter.pt')
        torch.save(_repr(self.pre_filter), path)

        print('Done!')

    def __len__(self) -> int:
        r"""The number of examples in the dataset."""
        return len(self.indices())

    def __getitem__(
        self,
        idx: Union[int, np.integer, IndexType],
    ) -> Union['Dataset', Data]:
        r"""In case :obj:`idx` is of type integer, will return the data object
        at index :obj:`idx` (and transforms it in case :obj:`transform` is
        present).
        In case :obj:`idx` is a slicing object, *e.g.*, :obj:`[2:5]`, a list, a
        tuple, a PyTorch :obj:`LongTensor` or a :obj:`BoolTensor`, or a numpy
        :obj:`np.array`, will return a subset of the dataset at the specified
        indices."""
        if (isinstance(idx, (int, np.integer))
                or (isinstance(idx, Tensor) and idx.dim() == 0)
                or (isinstance(idx, np.ndarray) and np.isscalar(idx))):

            data = self.get(self.indices()[idx])
            data = data if self.transform is None else self.transform(data)
            return data

        else:
            return self.index_select(idx)

    def index_select(self, idx: IndexType) -> 'Dataset':
        indices = self.indices()

        if isinstance(idx, slice):
            indices = indices[idx]

        elif isinstance(idx, Tensor) and idx.dtype == torch.long:
            return self.index_select(idx.flatten().tolist())

        elif isinstance(idx, Tensor) and idx.dtype == torch.bool:
            idx = idx.flatten().nonzero(as_tuple=False)
            return self.index_select(idx.flatten().tolist())

        elif isinstance(idx, np.ndarray) and idx.dtype == np.int64:
            return self.index_select(idx.flatten().tolist())

        elif isinstance(idx, np.ndarray) and idx.dtype == np.bool:
            idx = idx.flatten().nonzero()[0]
            return self.index_select(idx.flatten().tolist())

        elif isinstance(idx, Sequence) and not isinstance(idx, str):
            indices = [indices[i] for i in idx]

        else:
            raise IndexError(
                f"Only integers, slices (':'), list, tuples, torch.tensor and "
                f"np.ndarray of dtype long or bool are valid indices (got "
                f"'{type(idx).__name__}')")

        dataset = copy.copy(self)
        dataset._indices = indices
        return dataset

    def shuffle(
        self,
        return_perm: bool = False,
    ) -> Union['Dataset', Tuple['Dataset', Tensor]]:
        r"""Randomly shuffles the examples in the dataset.

        Args:
            return_perm (bool, optional): If set to :obj:`True`, will return
                the random permutation used to shuffle the dataset in addition.
                (default: :obj:`False`)
        """
        perm = torch.randperm(len(self))
        dataset = self.index_select(perm)
        return (dataset, perm) if return_perm is True else dataset

    def __repr__(self) -> str:
        arg_repr = str(len(self)) if len(self) > 1 else ''
        return f'{self.__class__.__name__}({arg_repr})'


def to_list(value: Any) -> Sequence:
    if isinstance(value, Sequence) and not isinstance(value, str):
        return value
    else:
        return [value]


def files_exist(files: List[str]) -> bool:
    # NOTE: We return `False` in case `files` is empty, leading to a
    # re-processing of files on every instantiation.
    return len(files) != 0 and all([osp.exists(f) for f in files])


def _repr(obj: Any) -> str:
    if obj is None:
        return 'None'
    return re.sub('(<.*?)\\s.*(>)', r'\1\2', obj.__repr__())

```

