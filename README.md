# VSS Data Collector

VSS Data Collector is module collecting vehicle data defined with [VSS(Vehicle Signal Specification)](https://github.com/GENIVI/vehicle_signal_specification) using [VSI(Vehicle Signal Inteface)](https://github.com/GENIVI/vehicle_signal_interface)

# Installation

### Tested Envrionment
VSS Data Collector is implemented and tested on:
* VMWare Workstation 12 Player (12.1.1 build-3770994)
* Ubuntu 14.04 64bit
* Qt 5.6.1 (for test application)

### Precondition
To build VSS Data Collector, following package are required
* VSI
* Boost 1.54 (or later)
    * system, thread, log

### Clone Source Codes
Clone source codes from GENIVI GitHub using following command in the terminal window:
#### VSI
Because the latest version of VSI is not compatible with C ++, the VSS Data Collector is implemented based on c2b1c0a Commit.

        $ git clone https://github.com/GENIVI/vehicle_signal_interface.git
  
        $ git checkout c2b1c0a

#### CDL

        $ git clone https://github.com/GENIVI/cat-data-logger.git
  
        $ git checkout trial_integration
  
### Build & Install
#### VSI build & install
Before build the VSI, apply patches for installation.
Copy patch files in VSSDataCollector(add-make-install.patch, add-package-config-file.patch) to VSI directory and apply patches.

        $ patch -p1 < add-make-install.patch
        $ patch -p1 < add-package-config-file.patch

And build and install VSI using following command:

        $ make
        $ sudo make install

#### VSS Data Collector build & install
In VSSDataCollector directory of CDL, build & install using following command:

        $ mkdir build
        $ cd build
        $ cmake ..
        $ make
        $ sudo make install
        
#### Test Application build & install
Navigate to the test directory of VSSDataCollector, and build & install using following command:

        $ qmake -r -spec linux-g++
        $ make
        # make install
        
After the installation, you can find binaries(Data Generator, VSSDataCollector Test Application) and other files for configuration and generated VSS JSON files using tool vspec2json.py in deploy directory

# Usage

### Run
Prepare two terminal windows and navigate to the deploy directory of test.
Run DataGenerator application in one window

        $ ./DataGenerator
        
and run VSSDataCollectorTestApp in the other window.

        $ ./VSSDataCollectorTestApp
        
The DataGenerator generates vehicle data randomly, and flushes data into VSI.
On VSSDataCollector side, you can check data collection status including data validation results.


