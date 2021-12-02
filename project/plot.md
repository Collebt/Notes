

```
from urllib.request import urlopen
from itertools import chain

import xml.etree.ElementTree as ET 
import numpy as np

base_url = "https://sid.erda.dk/share_redirect/fndmbD6D4I/"

datasets = ["31.08-C4-01_Tracks.xml",
      "31.08-C4-05_Tracks.xml",
      "09.04-C3-02_Tracks.xml",
      "09.04-C3-05_Tracks.xml",
      "09.04-D3-01_Tracks.xml",
      "09.04-D3-05_Tracks.xml",
      "09.04-E3-04_Tracks.xml",
      "09.04-E3-06_Tracks.xml"]

def load_xml_from_url(filename):
  url = base_url + filename
  with urlopen(url) as f:
    return ET.parse(f).getroot()
  
roots = [load_xml_from_url(f) for f in datasets]

def get_root_values(root):
  return map(lambda x: list(x.attrib.values()), root)

""" Particles is a collection of arrays with the 4 dimensions (t,x,y,z) of all the particles in the data sets """
particles = [np.array(list(get_root_values(r)), dtype=float) for r in chain(*roots)] # all problems can be solved with the information contained in particles

\# Prints can be useful to understand how the data is stored
```

