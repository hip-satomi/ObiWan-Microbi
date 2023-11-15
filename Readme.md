# ObiWan-Microbi: OMERO-based integrated Workflow for annotating Microbes in the Cloud

![Preview](https://raw.githubusercontent.com/hip-satomi/ObiWan-Microbi/animation/preview.gif)

ObiWan-Microbi is a toolkit collection for semi-automated segmentation and annotation of (biological) image data in the cloud. It utilizes an [OMERO](https://www.openmicroscopy.org/omero/) image server for data magement. We contribute **SegUI** - a browser-based tool for semi-automated manual segmentation and annotation - and **SegServe** - a remote neural network execution server. All three components are combined into a docker-compose setup to be easily deployed on a local computer or in a cloud system.

## Prerequisites

- install [docker](https://docs.docker.com/get-docker/)
- install [docker-compose](https://docs.docker.com/compose/install/)
- **recommended**: CUDA capable GPU for accelerated deep-learning execution.
- recommended: linux system for hosting (tested on ubuntu)

## Installation (Linux)

ObiWan-Microbi can be installed on your local system, network servers or cloud setups. For small instances and testing, desktop computers or server computers are recommended. For large-scale setups, we recommend a cloud solution.

The installation is performed once on your system. Afterwards, you can access the services in your local network with any computer, notebook, tablet or smartphone.

Please download this repository including its submodules using

```bash
git clone --recurse-submodules https://github.com/hip-satomi/ObiWan-Microbi.git
cd ObiWan-Microbi
```

The toolkit has to be built and launched using your bash shell

```bash
sudo docker-compose up --build
```

**Note**: Building will take a while for the first time (~1h) because all the necessary resources are downloaded, compiled and provided. However, this only has to be performed once: all following launches will be fast.

After the toolkit startup the defaults user (username: `root`, password: `omero`) is created and the following services are available:

- SegUI interface for annotation at [http://localhost](http://localhost).
- SegServe interface for executing segmentation algorithms with the respective openapi documentation of the REST API [http://localhost/segService/](http://localhost/segService/docs).
- OmeroWeb interface at [http://localhost:4080](http://localhost:4080).
- OMERO server at the default ports (4064) accessible with the default configuration of [OMERO Insight](https://www.openmicroscopy.org/omero/downloads/).

**Note:** Please make sure that the ports `80`, `4080` and `4064` are not used on your computer. Otherwise the launch of ObiWan-Microbi will fail.

**Note:** It is possible to connect ObiWan-Microbi to an existing OMERO server. If you would like to do so, please contact us.

### Accelerated Segmentation - GPU version

We also provided a GPU tailored version of the toolkit to utilize the faster segmentation performance of Nvidia GPU hardware. Make sure that you have a very recent [docker-compose](https://docs.docker.com/compose/install/) version, an Nvidia driver installed and please install [nvidia-docker2](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) to use your GPU in the docker container.

Now you can repeat the startup procedure with the GPU version

```bash
sudo docker-compose -f docker-compose.gpu.yml up --build
```

**Note:** GPU usage can dramatically speed up segmentation execution, especially for larger images (~20). Therfore, GPU usage is recommended in production usage. However, incompatibility problems between the computer NVIDIA driver and the NVIDIA driver used in the docker container can lead to problems. If you run into problems with your GPU please create an [issue](https://github.com/hip-satomi/ObiWan-Microbi/issues/new).

## Installation for Windows (Linux is recommended)

Installing ObiWan-Microbi on a Windows computer requires `admin` permissions and is possible using the [Windows subsystem for Linux 2 (WSL2)](https://learn.microsoft.com/de-de/windows/wsl/). Please follow the instructions [here](https://hackernoon.com/how-to-run-docker-linux-containers-natively-on-windows-ti1i3uxr) in order to get docker and Linux running on your Windows machine.

After that launch the linux distribution in `WSL2` mode and proceed with the normal installation instructions.

We used `Ubuntu 22.04.2 LTS` in the WSL mode during our tests.

**Why is Linux recommended?**

> `ObiWan-Microbi` on Linux is much better supported, especially when GPU acceleration is needed for faster segmentation prediction. Therefore, the Linux installation is recommended. For initial testing, the Windows setup can be used.

## Getting Started

For testing purposes, 5 simulated microbial time-lapse sequences are available after building the toolkit.

### Browsing Projects, Datasets & Images

You can open the SegUI browsing view at [http://localhost](http://localhost) and login with default admin credentials (username: `root`, password: `omero`).

In this video tutorial, we show how to browse the data on your OMERO instance.

[![Browsing data Tutorial](https://img.youtube.com/vi/WYo7iMmBehg/sd3.jpg)](https://youtu.be/WYo7iMmBehg)


### Annotating images

In this video tutorial, we show the segmentation features for fast manual cell segmentation.

[![Segmentation Annotation Tutorial](https://img.youtube.com/vi/1UMy6wnDnAU/sd3.jpg)](https://youtu.be/1UMy6wnDnAU)

### Semi-automated segmentation

In this video tutorial, we demonstrate the remote execution of AI segmentation using the user interface.

[![Semi-automated Segmentation Tutorial](https://img.youtube.com/vi/vx0hVg1Ua1U/sd3.jpg)](https://youtu.be/vx0hVg1Ua1U)

### Tracking Annotation

In this video tutorial, we show the manual tracking functionality.

[![Tracking Annotation Tutorial](https://img.youtube.com/vi/ureYzDTspQs/sd3.jpg)](https://youtu.be/ureYzDTspQs)

### Import & Export for OMERO

In this vidoe tutorial, we show the import and export functionality into OMERO's native formats.

[![Import & Export for OMERO Tutorial](https://img.youtube.com/vi/YF_H_Ctd6Cc/sd3.jpg)](https://youtu.be/YF_H_Ctd6Cc)

### Multi-label handling

In this video tutorial, we demonstrate complex image annotation with multiple class labels.

[![Multi-Label Tutorial](https://img.youtube.com/vi/o8xVpZydfLs/sd3.jpg)](https://youtu.be/o8xVpZydfLs)

### Adding Custom Segmentation Models

In this video tutorial, we show how to add custom segmentation models and utilize them in the web interface.

[![Adding Custom Segmentation Models](https://img.youtube.com/vi/WuYc5q68R3U/sd3.jpg)](https://youtu.be/WuYc5q68R3U)

### Training custom deep-learning segmentation

If you want to train your own deep-learning segmentation to get high-quality results on your custom data, we highly recommend using [microbeSEG](https://github.com/hip-satomi/microbeSEG). It allows to manage large training datasets, supports cropping to minimize annotation work, connects to ObiWan-Microbi toolkit for annotation and data management and allows to train microbial segmentation models. Check it out :rocket:

## Keyboard Shortcuts

### General

| Key    | Action |
| -------- | ------- |
| Left arrow | Previous image in the timelapse |
| Right arrow | Next Image in the timelapse |

### Brush Tool

| Key    | Action |
| -------- | ------- |
| A/Enter  | Add new segmentation annotation    |
| Del | Delete selected segmentation     |
| O    | Show/Hide overlays

### Tracking Tool

| Key    | Action |
| -------- | ------- |
| D  | Hold the d key to select multiple children for a cell |
| C | Activate/Deactivate edge cutting mode |

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
- **OMERO Integration**: User and data management using [OMERO](https://www.openmicroscopy.org/omero/).
- **Scalability**: The docker setup can be scaled from single-users to teams or a full cloud setup - depending on your demand.
- **Simple docker installation**: Dockers containerization functionalities allow to easily deploy ObiWan Microbi.
- **Remote accessibility**: You are no longer bound to one workstation. All your data is stored in OMERO and available in your browser after your login.
- **Facilitate collaboration**: OMERO allows to share data in groups such that ground truth creation can be performed in a team of experts.

## Publication:

[J.Seiffarth et al.: ObiWan-Microbi: OMERO-based integrated Workflow for annotation microbes in the cloud](https://doi.org/10.1101/2022.08.01.502297)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
