# Installing conda on Dawn

## 1. Introduction

This is guidance on using the [Miniforge](https://github.com/conda-forge/miniforge) installers to install the [conda](https://docs.conda.io/en/latest/) package
manager on the [Dawn supercomputer](https://www.hpc.cam.ac.uk/d-w-n).  Dawn is
hosted at the University of Cambridge, and is part
of the [AI Resource Research (AIRR)](https://www.gov.uk/government/publications/ai-research-resource/airr-advanced-supercomputers-for-the-uk).  It was initially
installed with 256 nodes, in the form of [Dell PowerEdge XE9640](https://www.delltechnologies.com/asset/en-us/products/servers/technical-support/poweredge-xe9640-spec-sheet.pdf) servers.  Each node consisted of: 2 CPUs ([Intel Xeon Platinum 8468](https://www.intel.com/content/www/us/en/products/sku/231735/intel-xeon-platinum-8468-processor-105m-cache-2-10-ghz/specifications.html)), each with 48 cores and 512 GiB RAM; 4 GPUs ([Intel Data Centre GPU Max 1550](https://www.intel.com/content/www/us/en/products/sku/232873/intel-data-center-gpu-max-1550/specifications.html)),
each with two stacks (or tiles), 1024 compute units, and 128 GiB RAM.

The material collected here is licensed under the
[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).

## 2. Where to install

To avoid taking up space in your home directory, it's suggested that
you install `conda` to a 
[filesystem](https://docs.hpc.cam.ac.uk/hpc/user-guide/io_management.html)
directory in the
[Reseach Data Store](https://www.hpc.cam.ac.uk/research-data-store).  Links
to the directories of the Research Data store to which you have access can be
found in the `rds` subdirectory of your home directory.  You can list these
links, and the absolute paths to which they correspond, on a Dawn login
node or compute node:
```
ls -l ~/rds
``` 
It can be useful to link the path of the `conda` installation to a path in
your home directory.  For example, to link a `conda` installation at
`~/rds/project_folder/my_conda` to the default `Miniforge` installation path,
use:
```
ln -s ~/rds/project_folder/my_conda ~/miniforge3
```

## 3. Installation

Before installing, you should check that you agree with the conditions of the
[Conda license](https://docs.conda.io/en/latest/license.html), and with
the conditions of the
[Miniforge license](https://github.com/conda-forge/miniforge?tab=License-1-ov-file).  Installation may be performed
[via a Slurm job](#31-installation-via-a-slurm-job) or
[from the command line](#32-installation-from-the-command-line).

### 3.1 Installation via a Slurm job

On a Dawn login node or compute node, download the installation script
[miniforge3_install.sh](miniforge3_install.sh):
```
wget https://raw.githubusercontent.com/kh296/dawn-conda/refs/heads/main/miniforge3_install.sh
```

Submit a Slurm job to run the script:
```
# Substitute for <project_account> a valid project account.
# Substitute for <install path> the path to the directory for installation.
# Substitute for <link path> a path to link to <install path>;
# or omit -l option to avoid creating a link.
sbatch --account=<project account> ./miniforge3_install.sh -i <install path> -l <link path>
```
**Warning**: Running the installation script deletes any pre-existing
files at `<install path>` and `<link path>`.  Be sure to use the paths that
you intend.

Once it starts running, the script should take about five minutes to
complete.  The job output is written to `miniforge3_install.log`.  If the
installation was successful, the last line of the output indicates the
command to set up the `Miniforge` environment for using `conda`.

### 3.2 Installation from the command line

On a Dawn compute node, installation may be performed by following
the instructions at:
- [https://github.com/conda-forge/miniforge#unix-like-platforms-macos-linux--wsl](https://github.com/conda-forge/miniforge#unix-like-platforms-macos-linux--wsl)

The basic steps are:
```
# Download installation script.
wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"

# Run installation script, providing responses when prompted,
# including specifying the installation location.
bash Miniforge3-$(uname)-$(uname -m).sh
```
Instructions on subsequently setting up the `Miniforge` environment for
using `conda` are included in the script output.  Any linking of the
installation directory must be done separately:
```
# Substitute for <install path> the path to the installation directory.
# Substitute for <link path> a path to link to <install path>.
ln -s <install path> <link path>
```

As an alternative to the above, it's also possible to run from the
command line the script for
[installation via a Slurm job](#31-installation-via-a-slurm-job).  In this case,
the commands are:
```
# Download installation script.
wget https://raw.githubusercontent.com/kh296/dawn-conda/refs/heads/main/miniforge3_install.sh
```
```
# Run installation script:
# substitute for <install path> the path to the directory for installation;
# substitute for <link path> a path to link to <install path>;
# or omit -l option to avoid creating a link.
bash miniforge3_install.sh -i <install path> -l <link path>
```
Again, instructions on subsequently setting up the `Miniforge` environment for
using `conda` are included in the script output.
