# ELCON Charger CAN DBC

[![Build Status](https://travis-ci.org/karlding/elcon-charger-dbc.svg?branch=master)](https://travis-ci.org/karlding/elcon-charger-dbc)

CAN DBC file for an ELCON UHF charger

## Requirements

These instructions use [eerimoq/cantools](https://github.com/eerimoq/cantools)
over SocketCAN to decode messages with the DBC. If you're using PCAN-Explorer 
or something similar, feel free to ignore those steps/requirements and 
directly import the DBC.

```
# Ensure that can-utils is installed
sudo apt-get update
sudo apt-get install can-utils

# Start the slcand userspace daemon and create slcan0 interface
# We assume 500 kbps bitrate, see (https://elinux.org/Bringing_CAN_interface_up)
sudo slcand -o -c -s6 /dev/ttyUSB0 slcan0

# Bring up the SocketCAN interface
sudo ifconfig slcan0 up

# Install cantools (either in a virtualenv or something).
pip install cantools
```

## Usage

```
# View the DBC file
cantools dump dbc/elcon.dbc

# Decode CAN messages with the DBC
candump slcan0 | cantools decode --single-line dbc/elcon.dbc
```
