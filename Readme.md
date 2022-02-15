# Obi-Wan Microbi: Omero based integrated workflow for annotating Microbes

Obi-Wan Microbi is a toolkit collection for semi-automated segmentation of (biological) image data in the cloud. It relies on the [Omero](https://www.openmicroscopy.org/omero/) image server to handling image storage and access handling. We contribute **SegUI** - a browser-based tool for semi-automated manual segmentation - and **SegServer** - a remote neural network execution server. All three components are combined into a docker-compose setup to be easily deployed on a local computer or in a cloud system.

## Installation

An ubuntu linux system is recommended to install this microarchitecture service. Then you can access the services in your local network with any computer providing a web-browser.

Please download this repository including its submodules using

```bash
git clone --recurse-submodules https://jugit.fz-juelich.de/satomi/obiwan-microbi.git
cd obiwan-microbi
```

For installing the ObiWan Microbi Toolkit make sure that [docker](https://docs.docker.com/get-docker/) and [docker-compose](https://docs.docker.com/compose/install/) are installed on your computer.

The Toolkit is be built and launched using your bash shell

```bash
sudo docker-compose up --build
```

**Note**: Building will take a while for the first time as all the necessary resources are downloaded, compiled and provided. However, this only has to be performed once: All following launches will be fast.

After the toolkit startup, the following services are provided:

- SegUI interface at [http://localhost](http://localhost).
- SegServe interface at [http://localhost/segService/](http://localhost/segService/). If you want to interactively test the api and inspect the openapi definitions see [here](http://localhost/segService/docs).
- OmeroWeb interface at [http://localhost:4080](http://localhost:4080).
- Omero server at the default ports (4064) so that it is accessible via [Omero Insight](https://www.openmicroscopy.org/omero/downloads/).

### GPU version

We also provided a GPU tailored version of the toolkit to utilize the faster segmentation performance of GPU hardware. Make sure that you have a very recent [docker-compose](https://docs.docker.com/compose/install/) version and an nvidia driver installed. Now you can repeat the startup procedure with the GPU version

```bash
docker-compose -f docker-compose.gpu.yml build
docker-compose -f docker-compose.gpu.yml up
```

## Getting Started

After the toolkit is built and online, 5 simulated image stacks are automatically added to the omero server to get you started.

### Browsing Projects, Datasets & Images

You can open the SegUI browsing view [here](http://localhost). Video about to come.

### Annotating images

Video about to come.

### Semi-automated segmentation

Video about to come.

### Import & Export for Omero

Video about to come.

### Multi-label handling

Video about to come.