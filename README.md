# gr-gsm-IMSI_Catcher-hachkrf

## Overview

This reposiroty is a guide on how to use a hackrf to find IMSI numbers

## Features

- **HackRF Support**
- **Osmocom Module**: Utilizes the Osmocom module in GNU Radio for interfacing with HackRF.
- **Customized Decoder**: Modified `build.py` script due to errors
- **UI edit:** Removed the UI so it runs in the terminal

## Requirements

- [GNU Radio]([InstallingGR - GNU Radio](https://wiki.gnuradio.org/index.php/InstallingGR)) Using the version 3.11
- HackRF
- [Osmocom Module]([GrOsmoSDR - gr-osmosdr - Open Source Mobile Communications](https://osmocom.org/projects/gr-osmosdr/wiki))

The idea is that gr-gsm will retreive the data and IMSI-catcher by using the gr-gsm will show the IMSI number, country etc.

## Gnuradio Companion

You can open the gnuradio companion by typing `gnuradio-companion` in the terminal assuming you installed gnuradio correctly

## Installation

1. **Install Gnu Radio from the link provided above.**
  
2. **Module install:**
  
  By cloning the gr-gsm original vesion it was not usable with my current GNU radio version so i found this reposiroty [gr-gsm](https://github.com/bkerler/gr-gsm/tree/maint-3.10_with_multiarfcn) but when installed from source code livemon was not available to use, so by installing it with sudo apt-get install gr-gsm i was able to get all the features nescessary but when running gr-gsm_livemon i got an error for the device.py file.
  
3. **Fix build.py:**
  
  Found in my repository I included the build.py file that fixed the not iterable error, replace the current `device.py` found in `/usr/local/lib/python3.12/dist-packages/gnuradio/gsm/` with my version
  
4. **Install IMSI-Catcher:**
  
  Install [IMSI-catcher](https://github.com/Oros42/IMSI-catcher)
  
5. **UI edit(Editing the grgsm_livemon):** By retreiving the grc found [grgsm_livemon.grc](https://github.com/ptrkrysik/gr-gsm/blob/master/apps/grgsm_livemon.grc) you can open it in the `gnuradio-companion` and run it, upon running it it will create a .py you can run independently of the gnuradio-companion. If you do not want a UI you can use the grc found in this repository by downloading it and following the same procedure
    

## Usage

1. Type in terminal `grgsm_scanner` scan the spectrum and find frequencies that have gsm signals,     Eg. Found CCCH arfcn: 979  
  Dont capture immediate assignments, skip extract SDCCH/8 info and scan...  
  ARFCN: 979, Freq: **926.0M**, CID: 10503, LAC: 10, MCC: 280, MNC: 20, Pwr: -40  
  |---- Configuration: 1 CCCH, not combined  
  |---- Cell ARFCNs: 979, 1016  
  |---- Neighbour Cells: 862, 864, 866, 868, 870, 872, 883, 975, 977, 981, 983, 985, 1015, 1019, 1021 Found CCCH arfcn: 981  
  Dont capture immediate assignments, skip extract SDCCH/8 info and scan...  
  ARFCN: 981, Freq: **926.4M**, CID: 10582, LAC: 10, MCC: 280, MNC: 20, Pwr: -28  
  |---- Configuration: 1 CCCH, not combined  
  |---- Cell ARFCNs: 981, 1018  
  |---- Neighbour Cells: 862, 864, 866, 868, 870, 872, 881, 883, 975, 977, 979, 983, 985, 1013, 1015, 1019, 1021The frequencyes are 926.0M and 926.4M
2. You can now either open the flowchart(.grc) file via the companion and run it there, or create and run the .py file the end result will be the same. From the companion if you want to change the frequency you have to change the variable from the flowchart, if you choose to run it from the .py file you run this in the terminal `./grgsm_livemon/py -f 926.0M` the program is now scanning data and sending it to a localhost server
3. Now run the `simple_IMSI-catcher.py` located in the `./IMSI-catcher` directory you cloned by typing in the terminal `sudo python3 ./simple_IMSI-catcher.py -s`
4. It should now be displaying cellphone IMSI numbers in the terminal where you are running the IMSI-cather
