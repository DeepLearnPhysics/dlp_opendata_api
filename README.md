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

**Initialization** The image reader is initialized by providing a file name (or more than one)
```python
fname = 'dlprod_ppn_v10/dlprod_192px_00.root'
img_reader = image_reader_3d(fname)
```

**Useage**

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

The particle API is in the `osf.particle_api` submodule.  
```python
from osf.particle_api import *
```

**Initialization** The particle reader is initialized by providing a file name (or more than one)
```python
fname = 'dlprod_ppn_v10/particle/dlprod_particle_192px_00.root'
preader = particle_reader(fname)
```

**Useage**

See how many events there are in the file:
```python
preader.entry_count()
```

Get event 0 in the file:
```python
event = preader.get_event(0)
```

The event is a dictionary of particle data.  If you want to get an individual particle from the event, use
```python
p = get_particle(event, 5) # gets particle 5
```

## Low-level API

For some tasks, the high-level APIs above may abstract away too many detatils.  There is also a low-level API that you can use if you know what you're looking for.

**See what's in a file*** 
```python
fname = 'dlprod_ppn_v10/dlprod_192px_00.root'
list_data(fname)
[out]: ['cluster3d_mcst', 'sparse3d_data', 'sparse3d_fivetypes', 'particle_mcst']
```

**Data Reader**
The `data_reader` class handles the input.

Initialization:
```python
reader = data_reader()
```
Add a file to read from:
```python
reader.add_file(fname)
```
Add data to read (use `list_data` to see options):
```python
reader.add_data('sparse3d_data')
```
See how many entries are available to read:
```python
reader.entry_count()
```
Set reader pointer to entry `i`
```python
i = 0
reader.read(i)
```
Get the actual data (once pointer is set)
```python
preader.data('sparse3d_data')
```
There are also several provided parsers, such as
```python
parse_sparse3d(preader.data('sparse3d_data'))
```

The two high-level APIs use `data_reader` as a base class, so you can also do the above manipulations to `image_reader_3d` and `particle_reader` instances.  However, their purpose is to wrap everything so it is a bit easier to use.

