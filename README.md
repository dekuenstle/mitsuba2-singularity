# mitsuba2-singularity
Install the Mitsuba2 renderer into a singularity container to render images on compute clusters.


## Using mitsuba2 in a container


### Build the image
We assume that `singularity` is installed on your system (tested with version `3.8.3`).

First configure the variants you want to use in the `mitsuba.conf` file.

Afterwards, build the image file `mitsuba2.sif`.
```
singularity build --fakeroot mitsuba2.sif mitsuba2.def
```
This command downloads the latest mitsuba2 from github to the `/mitsuba2` directory and compiles it with the variants, specified in the `mitsuba.conf` file.

### Run mitsuba
You can run mitsuba by executing `mitsuba2.sif`. 

```
./mitsuba2.sif --help
```

Alternatively, you run an interactive shell where mitsuba is available:

```
singularity shell mitsuba2.sif
Singularity> mitsuba --help
```

### Modify and debug the image

The image file is frozen which can be hindering at development time.
Sometimes it is helpful, to build and run a modifiable sandbox of the container:

```
singualarity build --sandbox --fakeroot mitsuba2-sandbox mitsuba2.def
singularity shell --writable mitsuba2-sandbox
```

## CPU vs GPU
Currently, the container supports just CPU variants of mitsuba2. 

Running GPU variants would require the following modifications of the container definition.
Use an cuda base image (i.e. `nvidia/cuda:<version>-devel-ubuntu20.04`) instead of ubuntu, add gpu variants to the `mitsuba.conf` file, and download and install Nividia OptiX. Pull-requests are welcome 😄

## Licence

Free to use under [MIT License](https://github.com/dekuenstle/mitsuba2-singularity/blob/main/LICENSE).
