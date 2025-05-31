# Low-latency Ethernet Communications on FPGA SoC for High Frequency Trading

## Overview

High frequency trading is the method of buying and selling stocks/assets at a rapid rate according to the fluctuations in a market exchange. In order to remain competitive in trading, lower latency is needed in order to respond to fluctuations in the exchange quicker, and this demand for computational power is typically not reachable by non-enterprise traders. This repository explores the performance gain of implementing a high frequency trading pipeline within an FPGA + SoC and communicating exchange information via Ethernet. In doing so, we achieve an average latency of **X** ns with the pipeline and an average latency of **Y** ns.

In our project, we use the PYNQ-Z2 development board to implement a high frequency trading pipeline in order to achieve low latency. We connect the board via Ethernet to a PC, and use the PYNQ-Z2's Jupyter Notebook feature to set up a server on the board. We use a Python script to set up a client on our PC and send/receive data via Python socket between the PC and the board. The board will receive the data and use a DMA module to move the packet data from the PS to the PL, process the data through the pipeline, and move the data from the PL back to the PS in order to send it back to the PC.

## Team

Brandon Reponte is a 4th year at UCSD studying computer science. He has a background in systems programming and computer architecture, as well as higher level skills in machine learning and AI.

Leeze Gutierrez-Ramirez...

Rudy Osuna...

## Repository Contents

In the root directory, there is a *documentation* folder and a *src* folder. The *documentation* folder contains all report, papers, videos, and other logistical parts of our project. The *src* folder contains the technicals of our project.

Within the *src* directory, there are *overlays*, *tests*, and *ethernet_loopback.ipynb*. The *overlays* directory contains ```.bit``` and ```.hwh``` files that are needed in order to load the design on the PYNQ-Z2 board. *tests* contain some Jupyter Notebooks and Python scripts that are useful in testing the hardware. There are client tests and host tests. Client tests are run on the PC. An example is connecting to the board and sending and receiving messages. Host tests are run on the board, specifically the PS.

*ethernet_loopback.ipynb* is the main loop code for the PYNQ-Z2 board. It sets up the server and listens for any client messages. Once the client sends a message, it will take the message and use the DMA to move the data into the PL, and retrieve the output. The output is then sent back to the client.

## Replication

1. [HOST] Open the board's Jupyter Notebook by opening the http://192.168.2.99/ on your browser.
2. [HOST] Within the same directory, upload the ```ethernet.bit```, ```ethernet.hwh```, and the ```ethernet_loopback.ipynb``` files.
3. [HOST] Open up the ```ethernet_loopback.ipynb``` file and run the notebook.
4. [CLIENT] On your PC, run the ```client_test.py``` file to send packets to the ```ethernet_loopback.ipynb``` host code.

## Challenges

### Ethernet

Ethernet implementation on the PL took up most of the time in the quarter. Documentation on FPGA and hardware is extremely limited.