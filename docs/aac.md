# Installing conda on AMD Accelerator Cluster

Conda can be installed on the
[AMD Accelerator Cluster (AAC)](https://aac.amd.com/help/) by following
the guidance for installation on Dawn
([dawn-conda/README.md](../README.md)),
except that for installation via a Slurm job the submission command needs
to be different.  In particular, it's usually not necessary
to specify the account, but it is necessary to specify the partition,
and the resources.

On AAC6, after following the instructions for obtaining the `conda`
installation script, an example submission command is:
```
# Substitute for <install path> the path to the directory for installation.
# Substitute for <link path> a path to link to <install path>;
# or omit -l option to avoid creating a link.
sbatch --partition=1CN192C4G1H_MI300A_Ubuntu22  --cpus-per-gpu=48 ./miniforge3_install.sh -i <install path> -l <link path>
```
