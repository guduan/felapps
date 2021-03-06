# felapps

High-level applications for the commissioning of free-electron laser 
facilities. Purely open-sourced, main developing language is 
`Python`, powered by various well-benchmarked module/packages,
e.g.: `matplotlib` (beautiful scientific plotting);
`numpy` and `scipy` (scientific computing);
`wxPython` (GUI building); `PyEpics` (interface with EPICS);
`h5py` (HDF5 interfacing), etc.

The goal of this project is to make a mature, full-fledged, friendly,
beautiful and stable open source software framework/suite for the 
physics level of FEL commissioning, including the beam tunning, 
parameters optimization and specific physics-related applications 
deployment, etc.

### Installation
<code>felapps</code> could be installed into the operating system by the 
following approaches:

1. (Recommanded) Install directly from PyPI by: 
<code>pip install felapps</code>, the required packages (i.e. the above listed python modules) will be pulled and installed automatically;
2. Clone this repo by <code>git clone https://github.com/Archman/felapps.git</code>.

### How to Use
Assuming the <code>felapps</code> package has been already installed by 
<code>pip</code> way, one can write python script and run it to call 
methods that included by <code>felapps</code>, e.g.:
```python
#!/usr/bin/env python
import felapps
felapps.imageviewer.run()
```
Or just type <code>imageviewer</code> in the terminal, the two methods do
the same thing. Please note that <code>imageviewer</code> app would 
complain that it cannot find any configuration file for loading in the
present working directory, then choose the configuration file as it guided,
the sample configuration file could be found in the source dir tree: 
[felapps/configs](https://github.com/Archman/felapps/tree/master/felapps/configs).

If use <code>felapps</code> by the <code>git clone</code> way, attention
should be paid to make sure the compiled python module (whl or egg) could
be found when imported in python. One may do as follows:

1. python setup.py bdist_wheel install
2. python setup.py bdist_wheel develop
3. python setup.py bdist_wheel

The first approach is to generate <code>felapps.VERSION.whl</code> module 
and install it in <code>/usr/local/lib/python2.7/dist-packages</code> by
default. Since the above path is also by default included in the 
<code>PYTHONPATH</code>, one can successfully import felapps in python,
that means <code>felapps</code> could be found by python.

The second approach is similar as the first, but it does not really put the
compiled python module into system directory, but just creates a link to
ensure python knows where <code>felapps</code> is.

The third approach only generates the python module, which could be imported
into python provided that the correct module path be added into 
<code>PYTHONPATH</code>, e.g.:
```python
import sys
sys.path.append('../dist/felapps.VERSION.whl')
import felapps
...
```
### Deploy Virtual FEL Control Environment
This python suite is degined for the commissioning of real FEL machine, however
we can setup the virtual control environment for the software development stage.
This section shows how to deploy such virtual environment on Linux workstation.

The communication between the suite and control layer is via channel access protocol
of EPICS; generally speaking, IOC application for the virtual machine should be built.

The EPICS base should be compiled and installed in the Linux workstation.

The built IOC application (or template) could be found in 
[felapps/ioc](https://github.com/Archman/felapps/tree/master/felapps/ioc), 
edit configure/RELEASE to make sure the EPICS_BASE path is valid, the database files 
(.db files) could be modified to simulate the FEL machine 
(since here's not any physics issues evolved, just control stuff), 
then build the ioc application; start the ioc to execute st.cmd in iocBoot dir.

The data update is simulated by python script, thanks to the PyEpics interface, 
one can update some PV values at some frequency, for instance, in ioc/apps dir, 
gendata.py script is made to update some waveform record every second.

### Screenshots

1. ImageViewer

<p>
  <img src=/screenshots/imageviewer/startup.png?raw=true alt="ImageViewer Startup" width="400"></img> <img src=/screenshots/imageviewer/roi.png?raw=true alt="imageviewer ROI" width="400"></img>
</p>
<p>
  <img src=/screenshots/imageviewer/configuration.png?raw=true alt="imageviewer Configurations" width="400"></img> <img src=/screenshots/imageviewer/colormap.png?raw=true alt="imageviewer Colormap" width="400"></img>
</p>
