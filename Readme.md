# Obi-Wan Microbi: Omero based integrated Workflow for annotating Microbes in the Cloud

Obi-Wan Microbi is a toolkit collection for semi-automated segmentation of (biological) image data in the cloud. It relies on the [Omero](https://www.openmicroscopy.org/omero/) image server to handling image storage and access handling. We contribute **SegUI** - a browser-based tool for semi-automated manual segmentation - and **SegServe** - a remote neural network execution server. All three components are combined into a docker-compose setup to be easily deployed on a local computer or in a cloud system.

## Installation

An ubuntu linux system is recommended to install the microarchitecture service. After installation you can access the services in your local network with any computer, notebook, tablet or smartphone.

Please download this repository including its submodules using

```bash
git clone --recurse-submodules https://github.com/hip-satomi/ObiWan-Microbi.git
cd obiwan-microbi
```

For installing the ObiWan Microbi Toolkit make sure that [docker](https://docs.docker.com/get-docker/) and [docker-compose](https://docs.docker.com/compose/install/) are installed on your computer.

The Toolkit has to be built and launched using your bash shell

```bash
sudo docker-compose up --build
```

**Note**: Building will take a while for the first time (~1h) because all the necessary resources are downloaded, compiled and provided. However, this only has to be performed once: All following launches will be fast.

After the toolkit startup, the following services are provided:

- SegUI interface at [http://localhost](http://localhost).
- SegServe interface at [http://localhost/segService/](http://localhost/segService/). If you want to interactively test the api and inspect the openapi definitions see [here](http://localhost/segService/docs).
- OmeroWeb interface at [http://localhost:4080](http://localhost:4080).
- Omero server at the default ports (4064) so that it is accessible via [Omero Insight](https://www.openmicroscopy.org/omero/downloads/).

**Note:** Please make sure that the ports `80`, `4080` and `4064` are not used on your computer. Otherwise the launch of ObiWan-Microbi will fail.

### GPU version

We also provided a GPU tailored version of the toolkit to utilize the faster segmentation performance of GPU hardware. Make sure that you have a very recent [docker-compose](https://docs.docker.com/compose/install/) version and an nvidia driver installed. Now you can repeat the startup procedure with the GPU version

```bash
sudo docker-compose -f docker-compose.gpu.yml up --build
```

**Note:** GPU usage can dramatically speed up segmentation execution, especially for larger images. Therfore, GPU usage is recommended in production usage.

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

### Add your own segmentation approach

Video about to come.

## Feature List

A complete feature list of the ObiWan-Microbi software platform

- **SegServe - Remote AI execution**: Execute AI approaches on a single server with specialized hardware (e.g. GPU).
  - **Expandable AI Zoo**: Segmentation approaches are packaged as git repositories and [mflow](https://mlflow.org/) and [anaconda](https://www.anaconda.com/) are used for dependency management. Installations are performed on demand. Your custom model only needs a git repo.
  - **Reproducibility**: AI approaches are executed with version specification (e.g. current git commit hash) and can be reproduced at any time.
  - **State-of-the art microbial segmentation**: Our model zoo currently contains the segmentation approaches [Cellpose](https://doi.org/10.1038/s41592-020-01018-x), [Omnipose](https://doi.org/10.1101/2021.11.03.467199), [Hybrid-Task-Cascade](https://arxiv.org/abs/1901.07518) and general object detector [Yolov5](https://doi.org/10.5281/zenodo.6222936).
  - **Efficient resource usage**: Multiple users access the same computation hardware increasing efficiency and utilization. At the same time specialized hardware (e.g. GPUs) are not necessary on end user devices.
  - **OpenAPI REST schema**: SegServe can also be used by third-party applications via its REST interface. Its usage is automatically documented using the [OpenAPI](https://github.com/OAI/OpenAPI-Specification) standard.
- **User-friendly ground truth annotation (SegUI)**:
  - **Platform independent**: User interface runs in the browser on any browser capable device (e.g. notebook, tablet, smartphone) and no installation is needed.
  - **Easy AI Usage**: Select segmentation approaches from AI model zoo and apply to image data no matter whether you work with your notebook, tablet or smartphone.
  - **Import/Export**: Share segmentation data with OMERO simplifying collaboration and scientific discussion.
  - **Smart data model**: Undo/redo segmentation changes to flexibly try all features without fearing mistakes.
  - **Manual correction tools**: Providing brush tool for drawing segmentations and a multi-select tool for selecting and deleting multiple segmentation contours.
  - **Multi-label handling**: Handles complex segmentation scenarios with multiple annotation labels and also supports AI approaches with multiple annotation classes.
  - **Automated Saving**: Do not loose any progress. We automatically save your work in the background.
- **OMERO Integration**: User and data management using [Omero](https://www.openmicroscopy.org/omero/).
- **Scalability**: The docker setup can be scaled from single-users to teams or a full cloud setup - depending on your demand.
- **Simple docker installation**: Dockers containerization functionalities allow to easily deploy ObiWan Microbi.
- **Remote accessibility**: You are no longer bound to one workstation. All your data is stored in OMERO and available in your browser after your login.
- **Facilitate collaboration**: OMERO allows to share data in groups such that ground truth creation can be performed in a team of experts.
