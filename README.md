# EasyBuild setup for Biocomplexity Institute at Virginia Tech

## Introduction

This is an EasyBuild setup for HPC resources at Biocomplexity Institute at Virginia Tech (formerly known as Virginia Bioinformatics Instiute). It provides a way to easily maintain large number of scientific software and make it accessible to our users.

This directory is typically found in `/apps/easybuild`. The git repository contains only setup files, basic structure, and module files. Module files include both maintained by BI administrators, and ones automatically generated by EasyBuild.

The main goals behind this setup are:

* Provide pre-configured EasyBuild environment and tools for both end users and HPC system administrators.
* Allow sysadmins to maintain global repositories, while giving users ability to install their own software.
* Use directory structure that works when home directories and shared app locations are shared across multiple different clusters and architectures

## Setup

To install and use this repository please see [setup description and installation notes](docs/installation.md).

EasyBuild has extensive documentation available at [their site](https://easybuild.readthedocs.org/en/latest/)

Other links of great interest:

* [Introduction to LMOD](http://users.ugent.be/~kehoste/Lmod-intro_20150209.pdf)
* [Introduction to EasyBuild](http://users.ugent.be/~kehoste/EasyBuild-20150123-Bayer.pdf)
* [HUST14 EasyBuild paper](http://www.ugent.be/hpc/hust14/hust14_05_easybuild-lmod_geimer-jsc_paper.pdf)

## Using EasyBuild

### Accessing software

* set up environment to access software built by EasyBuild:

```
module load site/discovery-sandy_bridge/easybuild/setup
```

* list all available modules:

```
module avail
```

### Installing new software

##### end-users

Besides having access to software maintained by BI under `/apps/easybuild`, users can install additional software via EasyBuild in their `~/easybuild/` directory. Our environment module sets up all required paths.

To get started, load the setup module and EasyBuild:

```
module load site/discovery-sandy_bridge/easybuild/setup
module load EasyBuild
```

Now you can run `eb` to search and install new software. 

* basic `eb` usage:
  * search for cufflinks
  ```
  eb -S cufflinks
  ```
  * install cufflinks
  ```
  eb Cufflinks-2.2.1-foss-2016a.eb --robot
  ```

#### system administrators

To maintain software in `/apps/easybuild` location we load a slightly different module to set up the environment. The only difference between `hpcadmin` and `setup` modules are:

* hpcadmin module sets up different permissions and groups
* hpcadmin module points only to global paths, and doesn't include anything from `~/easybuild` location


To get started, change your effective group and umask, then load the setup and EasyBuild modules:

```
newgrp hpcadmin
umask 002
module load site/discovery-sandy_bridge/easybuild/hpcadmin
module load EasyBuild
```

* basic `eb` usage:
  * search for cufflinks
  ```
  eb -S cufflinks
  ```
  * install cufflinks
  ```
  eb Cufflinks-2.2.1-foss-2016a.eb --robot
  ```

* review and commit your changes after installing software:

```
cd /apps/easybuild
git status
git add <appropriate dirs or files>
git commit -m 'installed Cufflinks-2.2.1-foss-2016a.eb'
```

## Documentation

### Random installation docs

* [Original design goals](docs/original_design.md)
* [Detailed setup description and installation notes for this repository](docs/installation.md)
* [Installation and setup on individual servers or workstations](docs/installation_on_other_systems.md)
* [How to build new software](docs/building_software.md)
* [Using distributed jobs to compile software with EasyBuild ](docs/distributed_jobs.md)
* [Examples of EasyConfigs](docs/example_easyconfigs.md)

## Presentations

* [Presentation on EasyBuild at Biocomplexity Institute](docs/introduction_to_easybuild-2017.09.11.pdf)




