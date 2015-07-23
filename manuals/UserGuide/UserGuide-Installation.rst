.. include:: /manuals/templates/pdf_constants.rst

Installing the Application
==========================

To download |TVB| check out the `official site <http://www.thevirtualbrain.org>`_

The TVB software package can be used in 3 different configurations:

- on a single machine (personal usage).
  This machine will need to meet the `Application requirements`_ for both the visualization and the computation/storage part.
  Any operation launched will use resources from current machine (graphic card, CPU, disk and RAM).

- in a client/server configuration, where TVB is installed on a server and made accessible to an unlimited number of users.

  This configuration is recommended when you have a powerful server to be used as back-end, where TVB is running and simulation or analysis operations are to be executed.
  The server machine will not require powerful graphics, as visualization will not be done here at all. Only the computation requirements from above will need to be met by the server.

  The visualization can be accessed from a personal computers by a browser (via HTTP).
  A network connection needs to exist between the server where TVB is running and the computer doing the visualization and access.
  http://${SERVER-IP}:8080 is the default URL.

- using a cluster (similar with server installation, but with parallelization support).
  Please note that for cluster installations, OAR is expected to be configured separately from TVB and accessible to the user for which the TVB software is launched.


To install |TVB| unzip the package and it will create a folder TVB_Distribution.


Launching the application
-------------------------

In the TVB_Distribution folder you should find a sub-folder `bin` with a number of scripts:

- tvb_start
- tvb_clean
- tvb_stop
- contributor_setup
- distribution

On Linux these scripts will have the `.sh` termination, on Mac the `.command` termination and on Windows the `.bat` termination.
We will omit the termination in this manual. For example if you are using Windows and tvb_start is mentioned
in this document then tvb_start.bat is meant.


Launching the GUI
.................

For Mac users the `TVB_Distribution` folder contains an application file `tvb.app`.
To start |TVB| in your web browser double click `tvb.app`.
Please be patient, as depending on your computer resources, the startup process might take about 1-2 minutes.

For Linux and Windows users, to start |TVB| in your web-browser, run the `tvb_start` script in `TVB_Distribution\bin`.

To make sure that no processes will remain open after you use the application,
you should always close |TVB| by running the `tvb_stop` script.


Launching scripting interfaces
..............................

The `distribution` script is used from a terminal to control the |TVB| distribution.
Run `distribution -h` too get help with this command.

To access the console interface, run in a terminal `distribution start COMMAND_PROFILE` or `distribution start LIBRARY_PROFILE`.
The interactive Python shell will appear. See the :ref:`console <shell_ui>` and :ref:`web interface<top_gui_guide>`
sections for more details on how to use the different interfaces of |TVB|.

The `tvb_clean` script will reset your TVB database and delete **all** data stored by |TVB|. Be careful!
Use this to get to a clean state, as if |TVB| had just been installed and never configured.

Configuring TVB
---------------

The preferred method to configure |TVB| is from the web interface. See :ref:`tvb_settings_ui`.

However if |TVB| is installed on a headless server (no GUI), then the web interface might not be available remotely.
See :ref:`tvb_settings_headless`.


Upgrading the Application
-------------------------

To upgrade to a new version, stop the server with `tvb_stop`, then delete the old distribution
and install the new distribution by unzipping the new TVB downloaded package.
Finally run the appropriate script for your platform to launch |TVB|.
The first run after update will migrate your projects to the new version.


Supported operating systems
---------------------------

The current |TVB| package was tested on :

- Debian Squeeze and Fedora 16.
  Other Linux flavors might also work as long as you have installed a glibc version of 2.11 or higher.

- Mac OS X greater than 10.7 are supported.

- Windows XP (x32), Windows Server 2008 (x64) and Windows 7 (x64).


Application requirements
------------------------

As |TVB| redefines what's possible in neuroscience utilizing off-the-shelf computer hardware, a few requirements are essential when using the software.

Requirements for front-end visualization:

- **High definition monitor** -
  Your monitor should be capable of displaying at least 1600 x 1000 pixels. Some views might be truncated if TVB is run on smaller monitors.

- **WebGL and WebSockets compatible browser** -
  We've tested the software on Mozilla Firefox 30+, Apple Safari 7+ and Google Chrome 30+.
  Using a different, less capable browser might result in some features not working or the user interface looking awkward at times.

- **WebGL-compatible graphics card** -
  The graphic card has to support OpenGL version 2.0 or higher. The operating system needs to have a proper card driver as well to expose the graphic card towards WebGL.
  This requirement only affects PCs, not (somewhat recent) Macs.


Requirements for computation/storage power, dependent on the number of parallel simulations that will be executed concurrently:

- **CPU power** -
  1 CPU core is needed for one simulation. When launching more simulations than the number of available cores, a serialization is recommended.
  This can be done by setting the "maximum number of parallel threads" (in TVB settings) to the same value as the number of cores.

- **Memory** -
  For a single simulation 8GB of RAM should be sufficient for region level simulations, but 16GB are recommended, especially if you are to run complex simulations.

- **Disk space** is also important, as simulating only 10 ms on surface level will occupy 280MB of disk space. A minimum of 50GB of space per user is a rough approximation.

- For Linux and Mac, we are only supporting x64 architectures.
  Due to licensing and packaging, for Windows we are currently distributing an x32 package.
  Please take note that some simulations on surface level might require more memory that 32 bit programs can address,
  at which point the TVB software will notify you about this with a "Memory Error".
  So for complex operations, on Windows, you might need to install TVB from sources (see our repositories on GitHub),
  but this requires separate installation of Python x64 and all the other TVB dependencies.

- Optional **MatLab or Octave** -
  A special feature in TVB is utilizing functions from the Brain Connectivity Toolbox.
  This feature thus requires a MatLab or Octave package on your computer (installed, activated and added to your OS' global PATH variable).
  The Brain Connectivity Toolbox doesn't need to be installed or enabled separately in any way, as TVB will temporarily append it to your MatLab/Octave path.