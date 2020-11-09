# Paraview 

## Introduction

[Paraview](http://www.paraview.org/) is a data analysis and
visualisation application, developed to be able to analyse large
datasets. We show here how to start the program on our facilities;
however, please refer to the project documentation for details on how to
use the application itself.  You can also use
[X2GO](../getting_started/x2go)
when you login and the images will render better and you will get rid of
the OpenGL warnings that may appear.

Although paraview is flexible in the way it is deployed, the simplest
method of invoking it is to run these commands on a login node:

    $ module load paraview
    $ paraview --mesa-llvm &

or

    $ module load paraview
    $ paraview --mesa-llvm  &

This will provide the core functionality. More complicated methods are
described below, offering different levels of performance. For example,
the graphical interface can be run locally on a low-end
workstation/laptop, while the rendering takes place in parallel on the
cluster -- taking advantage of the CPU, memory and storage resources
available. Although not making use of the acceleration that graphics
cards provide, it can allow larger datasets that cannot fit onto a
graphics card to be analysed.

## Running the paraview graphical interface

The paraview graphical interface can be run in several ways. Once
running, the graphical interface can either be used as-is, or paired
with a separate server program that can offload the rendering and
storage access to one or more cluster compute nodes.

Please note that methods (1) and (2) depend on your workstation having
an X server running and for you to have enabled X11 forwarding through
your SSH client.

### On a cluster login node (quick start)

Recommended for very short or undemanding pieces of work. Login to the
cluster and execute:

    $ module load paraview
    $ paraview --mesa-llvm 

Please note that, as they are shared between all users, it is important
not to tackle large pieces of work on the login nodes.

### On a cluster compute node

Recommended for larger pieces of work:

    $ module load paraview
    $ qrsh -cwd -V -l h_rt= -l h_vmem= paraview --mesa-llvm

In the above command, hh:mm:ss is the length of real time the program
will be run for and vmem is the amount of memory required.

### On your local workstation

Recommended where the graphical interface (menu items, etc.) feels
sluggish, or where the best possible performance is required.

Select a version number from the list of installed versions of the
paraview server, then download and install a copy of that version
appropriate to your machine from <http://www.paraview.org/>. The list of
installed versions is provided by the command:

    $ module avail paraview-osmesa

Once installed and running, it can be used to connect to a paraview
server running on the cluster (see below).

## Running the paraview server

The paraview server does not need to be run on the same computer as the
graphical interface and takes on the role of file access and graphics
rendering. Warning -- there is no authentication step when connecting to
a paraview server! Between the time of start of the server and the time
at which a client is connected to it, anyone logged into the cluster can
connect a client to it!

Once started, it will print a line of the form:

    Accepting connection(s): :

Please take a note of \<hostname\> and \<number\> -- they will be needed
to connect the graphical interface.

### On a cluster login node

Recommended for very short or undemanding pieces of work. Login to the
cluster and execute:

    $ module load paraview-osmesa
    $ pvserver --server-port=

For port, please select a number between 10000 and 20000.

### On a cluster compute node (serial)

    $ module load paraview-osmesa
    $ qrsh -cwd -V -l h_rt= -l h_vmem= pvserver --server-port=

In the above command, hh:mm:ss is the length of real time the program
will be run for and vmem is the amount of memory required. For port,
please select a number between 10000 and 20000.

### On a cluster compute node (parallel)

    $ module load paraview-osmesa
    $ qrsh -cwd -V -l h_rt= -l nodes= pvserver --server-port=

In the above command, hh:mm:ss is the length of real time the program
will be run for and num is the number of compute nodes required.
Recommended to start with 1 node. For port, please select a number
between 10000 and 20000.

## Connecting to a paraview server with the graphical interface

Once a paraview server is running, a graphical interface can connect to
it. Select the menu item File-\>Connect to bring up the Choose Server
Configuration box. Assuming you have not already created a suitable
configuration, select Add Server for the Edit Server Configuration box.

The server configuration details depend on where the graphical interface
is running (below). Once done, click Configure, leave Startup Type and
Manual and click Save. Double-click on the configuration to attempt to
contact the server.

### Graphical interface running on a cluster login or compute node

Please give the configuration a memorable name, and leave Server Type as
Client/Server. Note that you will not be able to save the configuration
unless it is given a name. The hostname from the output of pvserver
should be entered into the Host field, and the number into the Port
field.

### Graphical interface running on your local workstation

Please give the configuration a memorable name, leave Server Type as
Client/Server, enter localhost into the Host field and 11111 into the
Port field. Note that you will not be able to save the configuration
unless it is given a name.

Configure your workstation's SSH client to forward local port 11111 to
the hostname and port from the output of pvserver. On a Linux
workstation and paraview running somewhere on arc2, this can be achieved
via the following command:

    $ ssh -L11111:: arc2.leeds.ac.uk
