```python
SuperResModel(
  (time_embed): Sequential(
    (0): Linear(in_features=128, out_features=512, bias=True)
    (1): ReLU()
    (2): Linear(in_features=512, out_features=512, bias=True)
  )
  (input_blocks): ModuleList(
    (0): TimestepEmbedSequential(
      (0): Conv2d(6, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
    )
    (1): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=256, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Identity()
      )
    )
    (2): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=256, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Identity()
      )
    )
    (3): TimestepEmbedSequential(
      (0): Downsample(
        (op): Conv2d(128, 128, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1))
      )
    )
    (4): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=256, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Identity()
      )
    )
    (5): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=256, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Identity()
      )
    )
    (6): TimestepEmbedSequential(
      (0): Downsample(
        (op): Conv2d(128, 128, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1))
      )
    )
    (7): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(128, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=512, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(128, 256, kernel_size=(1, 1), stride=(1, 1))
      )
    )
    (8): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=512, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Identity()
      )
    )
    (9): TimestepEmbedSequential(
      (0): Downsample(
        (op): Conv2d(256, 256, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1))
      )
    )
    (10): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=512, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Identity()
      )
    )
    (11): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=512, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Identity()
      )
    )
    (12): TimestepEmbedSequential(
      (0): Downsample(
        (op): Conv2d(256, 256, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1))
      )
    )
    (13): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(256, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=1024, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(256, 512, kernel_size=(1, 1), stride=(1, 1))
      )
      (1): AttentionBlock(
        (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
        (attention): QKVAttentionLegacy()
        (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
      )
    )
    (14): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=1024, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Identity()
      )
      (1): AttentionBlock(
        (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
        (attention): QKVAttentionLegacy()
        (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
      )
    )
    (15): TimestepEmbedSequential(
      (0): Downsample(
        (op): Conv2d(512, 512, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1))
      )
    )
    (16): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=1024, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Identity()
      )
      (1): AttentionBlock(
        (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
        (attention): QKVAttentionLegacy()
        (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
      )
    )
    (17): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=1024, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Identity()
      )
      (1): AttentionBlock(
        (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
        (attention): QKVAttentionLegacy()
        (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
      )
    )
  )
  (middle_block): TimestepEmbedSequential(
    (0): ResBlock(
      (in_layers): Sequential(
        (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (1): ReLU()
        (2): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      )
      (h_upd): Identity()
      (x_upd): Identity()
      (emb_layers): Sequential(
        (0): ReLU()
        (1): Linear(in_features=512, out_features=1024, bias=True)
      )
      (out_layers): Sequential(
        (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (1): ReLU()
        (2): Dropout(p=0.0, inplace=False)
        (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      )
      (skip_connection): Identity()
    )
    (1): AttentionBlock(
      (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
      (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
      (attention): QKVAttentionLegacy()
      (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
    )
    (2): ResBlock(
      (in_layers): Sequential(
        (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (1): ReLU()
        (2): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      )
      (h_upd): Identity()
      (x_upd): Identity()
      (emb_layers): Sequential(
        (0): ReLU()
        (1): Linear(in_features=512, out_features=1024, bias=True)
      )
      (out_layers): Sequential(
        (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (1): ReLU()
        (2): Dropout(p=0.0, inplace=False)
        (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      )
      (skip_connection): Identity()
    )
  )
  (output_blocks): ModuleList(
    (0): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 1024, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(1024, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=1024, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(1024, 512, kernel_size=(1, 1), stride=(1, 1))
      )
      (1): AttentionBlock(
        (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
        (attention): QKVAttentionLegacy()
        (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
      )
    )
    (1): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 1024, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(1024, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=1024, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(1024, 512, kernel_size=(1, 1), stride=(1, 1))
      )
      (1): AttentionBlock(
        (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
        (attention): QKVAttentionLegacy()
        (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
      )
    )
    (2): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 1024, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(1024, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=1024, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(1024, 512, kernel_size=(1, 1), stride=(1, 1))
      )
      (1): AttentionBlock(
        (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
        (attention): QKVAttentionLegacy()
        (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
      )
      (2): Upsample(
        (conv): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      )
    )
    (3): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 1024, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(1024, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=1024, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(1024, 512, kernel_size=(1, 1), stride=(1, 1))
      )
      (1): AttentionBlock(
        (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
        (attention): QKVAttentionLegacy()
        (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
      )
    )
    (4): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 1024, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(1024, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=1024, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(1024, 512, kernel_size=(1, 1), stride=(1, 1))
      )
      (1): AttentionBlock(
        (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
        (attention): QKVAttentionLegacy()
        (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
      )
    )
    (5): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 768, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(768, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=1024, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(768, 512, kernel_size=(1, 1), stride=(1, 1))
      )
      (1): AttentionBlock(
        (norm): GroupNorm32(32, 512, eps=1e-05, affine=True)
        (qkv): Conv1d(512, 1536, kernel_size=(1,), stride=(1,))
        (attention): QKVAttentionLegacy()
        (proj_out): Conv1d(512, 512, kernel_size=(1,), stride=(1,))
      )
      (2): Upsample(
        (conv): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      )
    )
    (6): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 768, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(768, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=512, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(768, 256, kernel_size=(1, 1), stride=(1, 1))
      )
    )
    (7): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(512, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=512, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(512, 256, kernel_size=(1, 1), stride=(1, 1))
      )
    )
    (8): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(512, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=512, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(512, 256, kernel_size=(1, 1), stride=(1, 1))
      )
      (1): Upsample(
        (conv): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      )
    )
    (9): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(512, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=512, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(512, 256, kernel_size=(1, 1), stride=(1, 1))
      )
    )
    (10): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 512, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(512, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=512, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(512, 256, kernel_size=(1, 1), stride=(1, 1))
      )
    )
    (11): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 384, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(384, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=512, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(384, 256, kernel_size=(1, 1), stride=(1, 1))
      )
      (1): Upsample(
        (conv): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      )
    )
    (12): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 384, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(384, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=256, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(384, 128, kernel_size=(1, 1), stride=(1, 1))
      )
    )
    (13): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(256, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=256, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(256, 128, kernel_size=(1, 1), stride=(1, 1))
      )
    )
    (14): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(256, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=256, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(256, 128, kernel_size=(1, 1), stride=(1, 1))
      )
      (1): Upsample(
        (conv): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      )
    )
    (15): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(256, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=256, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(256, 128, kernel_size=(1, 1), stride=(1, 1))
      )
    )
    (16): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(256, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=256, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(256, 128, kernel_size=(1, 1), stride=(1, 1))
      )
    )
    (17): TimestepEmbedSequential(
      (0): ResBlock(
        (in_layers): Sequential(
          (0): GroupNorm32(32, 256, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Conv2d(256, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (h_upd): Identity()
        (x_upd): Identity()
        (emb_layers): Sequential(
          (0): ReLU()
          (1): Linear(in_features=512, out_features=256, bias=True)
        )
        (out_layers): Sequential(
          (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
          (1): ReLU()
          (2): Dropout(p=0.0, inplace=False)
          (3): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
        )
        (skip_connection): Conv2d(256, 128, kernel_size=(1, 1), stride=(1, 1))
      )
    )
  )
  (vgg): VGG19(
    (model): Sequential(
      (0): Conv2d(3, 64, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (1): ReLU(inplace=True)
      (2): Conv2d(64, 64, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (3): ReLU(inplace=True)
      (4): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
      (5): Conv2d(64, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
      (6): ReLU(inplace=True)
      (7): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
    )
  )
  (conv_convert2): ResBlock(
    (in_layers): Sequential(
      (0): GroupNorm32(32, 320, eps=1e-05, affine=True)
      (1): ReLU()
      (2): Conv2d(320, 192, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
    )
    (h_upd): Identity()
    (x_upd): Identity()
    (emb_layers): Sequential(
      (0): ReLU()
      (1): Linear(in_features=512, out_features=384, bias=True)
    )
    (out_layers): Sequential(
      (0): GroupNorm32(32, 192, eps=1e-05, affine=True)
      (1): ReLU()
      (2): Dropout(p=0.0, inplace=False)
      (3): Conv2d(192, 192, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
    )
    (skip_connection): Conv2d(320, 192, kernel_size=(1, 1), stride=(1, 1))
  )
  (out): Sequential(
    (0): GroupNorm32(32, 128, eps=1e-05, affine=True)
    (1): ReLU()
    (2): Conv2d(128, 3, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  )
)
```





Namespace(attention_resolutions='16,8', batch_size=1, class_cond=False, data_dir=PosixPath('/home/wh/data/SN6align200'), diffusion_steps=1000, dropout=0.0, ema_rate='0.9999', fp16_scale_growth=0.001, large_size=256, learn_sigma=False, log_interval=1000, lr=0.0001, lr_anneal_steps=0, microbatch=1, noise_schedule='linear', num_channels=128, num_head_channels=-1, num_heads=4, num_heads_upsample=-1, num_res_blocks=2, predict_xstart=False, resblock_updown=False, rescale_learned_sigmas=False, rescale_timesteps=True, resume_checkpoint='./weights/64_256_upsampler.pt', save_interval=10, schedule_sampler='uniform', small_size=256, timestep_respacing='ddim100', use_checkpoint=True, use_fp16=False, use_kl=False, use_scale_shift_norm=True, weight_decay=0.0)