# Python API

This package exposes a data API for larcv data

To use the package, just exectute the following when you start a python session
```python
import sys
sys.path.append("<path>/dlp_opendata_api")
```
The main module is `osf`

## Image API

The image API is in the `osf.image_api` submodule.  A 3D image API is built around a `image_reader_3d` class.
```python
from osf.image_api import image_reader_3d
```

*Initialization* The image reader is initialized by providing a file name (or more than one)
```python
fname = 'dlprod_ppn_v10/dlprod_192px_00.root'
img_reader = image_reader_3d(fname)
```

*Useage*

See how many events are in the file:
```python
img_reader.entry_count()
```

Get energy from event 0:
```python
voxels, energy = img_reader.get_energy(0)
```

Get classes from event 1:
```python
voxels, classes = img_reader.get_classes(1)
```

Get energy and classes from event 0:
```python
voxels, energy, classes = img_reader.get_image(0)
```


## Particle API

## Low-level API

For some tasks, the high-level APIs above may abstract away too many detatils.  There is also a low-level API that you can use if you know what you're looking for.