# NAMD

## License Arrangements

This software is installed with a non-commercial use license. Access to this software is restricted. User must agree to the license, found [here](http://www.ks.uiuc.edu/Research/namd/license.html). Please send a written statement accepting the license terms as a ticket to the [Research Computing Team](https://bit.ly/arc-help) in order for us to give you access to NAMD.

## Example submission script

An example script, `namdexample.sh` , looks like:

```bash
#!/bin/bash
# Request 8 cores anywhere on the compute nodes
#$ -pe ib 8
# Run for at most 12 hours
#$ -l h_rt=12:0:0
# Reserve 1Gbyte of RAM
#$ -l h_vmem=1G
# Run in the current directory
#$ -cwd

module add namd/2.13
mpirun namd2 name_of_config_file.conf > output_log_file.log
```

This example requests 8 cores for 12 hours, with each core limited to 1Gb of RAM.  It assumes that you are submitting the job from the directory containing your input files.

```{note}
Prior to NAMD 2.9, the `namd2` MPI binary was called `namd2.MPI`.
```

## Example GPU submission script

You may want to run using GPUs where you are likely to see a considerable speedup.

```bash
#!/bin/bash
# Run for at most 12 hours
#$ -l h_rt=12:0:0
# Request a GPU (in this case a v100)
#$ -l coproc_v100=1
# Run in the current directory
#$ -cwd

module add namd/2.13gpu
namd2 +idlepoll +p${NSLOTS} name_of_config_file.conf > output_log_file.log
```

This example requests 1 GPU, which comes with 1/4 of the resources available on the machine - in this case that means 10 cores and 48Gbytes of RAM.  It assumes that you are submitting the job from the directory containing your input files.
