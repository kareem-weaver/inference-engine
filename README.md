
```ascii
  _        __                                                     _            
 (_)      / _|                                                   (_)           
  _ _ __ | |_ ___ _ __ ___ _ __   ___ ___         ___ _ __   __ _ _ _ __   ___ 
 | | '_ \|  _/ _ \ '__/ _ \ '_ \ / __/ _ \  __   / _ \ '_ \ / _` | | '_ \ / _ \
 | | | | | ||  __/ | |  __/ | | | (_|  __/ |__| |  __/ | | | (_| | | | | |  __/
 |_|_| |_|_| \___|_|  \___|_| |_|\___\___|       \___|_| |_|\__, |_|_| |_|\___|
                                                             __/ |             
                                                            |___/              
```

![GitHub manifest version](https://img.shields.io/github/manifest-json/v/BerkeleyLab/inference-engine)
![GitHub branch checks state](https://img.shields.io/github/checks-status/BerkeleyLab/inference-engine/main)
[![GitHub issues](https://img.shields.io/github/issues/BerkeleyLab/inference-engine)](https://github.com/BerkeleyLab/inference-engine/issues)
[![GitHub license](https://img.shields.io/github/license/BerkeleyLab/inference-engine)](https://github.com/BerkeleyLab/inference-engine)
![GitHub watchers](https://img.shields.io/github/watchers/BerkeleyLab/inference-engine?style=social)

Inference-Engine
================

Table of contents
-----------------

- [Overview](#overview)
- [Downloading, Building and testing](#downloading-building-and-testing)
- [Examples](#examples)
- [Documentation](#documentation)

Overview
--------

Inference-Engine is a software library for researching ways to efficiently propagate inputs through deep, feed-forward neural networks exported from Python by the companion package [nexport].  Inference-Engine's implementation language, Fortran 2018, makes it suitable for integration into high-performance computing (HPC) applications.  The first HPC application of interest is the Intermediate Complexity Atmospheric Research ([ICAR]) model.  The novel features of Inference-Engine include

1. Exposing concurrency via 
  - An `elemental` inference function
  - An `elemental` activation strategy 
2. Gathering network weights and biases into contiguous arrays
3. Runtime selection of inference algorithm
  
Item 1 ensures that the `infer` procedure can be invoked inside Fortran's `do concurrent` construct, which some compilers can offload automatically to graphics processing units (GPUs).  We envision this being useful in applications that require large numbers of independent inferences.  Item 2 exploits the special case where the number of neurons is uniform across the network layers.  The use of contiguous arrays facilitates spatial locality in memory access patterns.  Item 3 offers the possibility of adaptive inference method selection based on runtime information.  The current methods include ones based on intrinsic functions, `dot_product` or `matmul`.  Future options will explore the use of OpenMP and OpenACC for vectorization, multithreading, and/or accelerator offloading.

Downloading, Building and Testing
---------------------------------
To download, build, and test Inference-Engine, enter the following commands in a Linux, macOS, or Windows Subsystem for Linux shell:
```
git clone https://github.com/berkeleylab/inference-engine
cd inference-engine
./setup.sh
```
whereupon the trailing output will provide instructions for running the examples in the [example](./example) subdirectory.

Examples
--------
The [example](./example) subdirectory contains demonstrations of several intended use cases.

Documentation
-------------
Please see the Inference-Engine GitHub Pages [site] for HTML documentation generated by [`ford`].

[site]: https://berkeleylab.github.io/inference-engine/ 
[`ford`]: https://github.com/Fortran-FOSS-Programmers/ford
[nexport]: https://go.lbl.gov/nexport
[ICAR]: https://github.com/NCAR/icar
