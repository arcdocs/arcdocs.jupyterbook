# Stata

## Access to Stata

The currently installed versions of Stata are run on multicore systems.
The version installed will support Stata running on up to eight cores
per job.

To uses Stata, you will need to have either your own licence or to be a
member of a research group who already have a licence. The University
does not have a site licence for this product.

Stata should be primarily run through batch queuing system, however
short interactive runs can done on the login nodes. You can run Stata
interactively though the batch queue system.

## Setting the module environment

Before you can run the software you will need to load the Stata module.
To load the module from the command line, do:

    module add stata

To check that module is loaded you can use:

    module list

## Interactive Stata sessions

It is anticipated that the main benefit of running Stata on the facility
will be from running non-interactive/unattended batch sessions. However,
it is also possible to run in interactive more for short test for
visualisation of data for instance.

### Interactive sessions on the login nodes -- for short tests only

Stata can be launched on the login nodes for short tests, ideally less
than 5 minutes computation, by using the appropriate executable name at
the command prompt. For the Stata command line interface use:

    stata-mp

and for the full graphical interface (providing you have connected using
`ssh -X` or `ssh -Y` ) using:

    xstata-mp

### Interactive sessions through interactive shells

For longer interactive sessions, it will be necessary to launch Stata
through batch queues, using the command `qrsh` . The length of time required is specified
as an option to the queueing system and specified in the format
`<hh:mm:ss>` . For instance
to request an interactive session for two hours, the full command takes
the form:

    qrsh -cwd -V -pe smp 8 -l h_rt=02:00:00,h_vmem=1536M xstata-mp

where:

-   `-cwd -V` : run from
    current directory and with current environment, i.e. loaded module.
-   `-pe smp 8` : request 8
    cores in shared memory environment. The requests appropriate number
    of computational cores to take advantage of the multicore nature of
    Stata.
-   `00:02:00` : is the
    length of time needed for the job, 2 hours in this case. Job will be
    killed when this time has elapsed.
-   `h_vmem=1536M` : Amount
    of memory requested per core. The value given here will make use of
    all available memory on the majority of the nodes.

For more details about these and other available options please look at
the page on [Interactive jobs](../usage/interactive).

## Batch execution

In oder to submit a batch job to the cluster it is necessary to use a
submission script. An example submission script for ARC2,
`stata_sub_example.sh` ,
takes the form:

    #!/bin/bash
    # Batch script to run a Stata/MP job

    # Run from current directory and environment.
    #$ -cwd -V
    # Request wallclock time. Format hh:mm:ss, for e.g 6 hours
    # maximum allowed is 48 hours.
    #$ -l h_rt=06:00:00

    # To get an email when the job begins and ends- fill in your 
    #$ -m be
    #$ -M @leeds.ac.uk

    # Request 8 cores from the machine. 
    #Current version of Stata can run on a maximum of 8 Cores
    #$ -l np=8

    # Load the Stata module
    module add stata

    # Start the Stata job, with your program in
    # a file your_do_file.do
    stata-mp -b do your_do_script.do

The job can then be submitted to the queuing system using the command:

    qsub stata_sub_example.sh

For more details on options used above and some of the other options
available please look at the page on [Batch jobs](../usage/batchjob).
