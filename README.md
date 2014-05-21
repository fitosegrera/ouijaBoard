ouijaBoard
==========
###Ouija board SOFTWARE installation and configuration guide:

Created by: fito_segrera
http://fii.to/

Special thanks to the JasperProject http://jasperproject.github.io/

The ouijaBoard project operates using a Raspberry Pi. All the process lsted next is created for this device. All the process has been installed and tested on Raspbian...

###Method 1 (Eassy)

Download the Raspberry Pi Image from this link: http://fii.to/downloads/ouijaBoard.tar.gz unzip and create a new raspberry pi SD card with it. Please use an 8 GB Sd card for this (note: please make sure that the SD card you are ussing is supported by the RBpi... please see: http://elinux.org/RPi_SD_cards)

###Method 2 (The HARDCORE way)

2.1 Download Raspbian Install and Configure

To download and install Raspbian please follow the official guide here: http://www.raspberrypi.org/downloads/

After that continue with the configuration in this guide.

Configure Raspbian
We’re now going to do some basic housekeeping and install some of the required libraries. You should SSH into your Pi with a command similar to the following. The IP address usually falls in the 192.168.2.3-192.168.2.10 range.

    ssh pi@192.168.2.3 # password (default): raspberry
    
Run the following, select to ‘Expand Filesystem’ and restart your Pi:

    sudo raspi-config

Run the following commands to update Pi and some install some useful tools.

    sudo apt-get update
    sudo apt-get upgrade --yes
    sudo apt-get install vim git-core espeak python-dev python-pip bison libasound2-dev libportaudio-dev python-pyaudio     --yes
    sudo apt-get install alsa-utils 
    
To change the audio output of the RBpi type: (replace <n> with 1 for analog aoutput or 2 for HDMI) exaple sudo amixer cset numid=3 1

    sudo amixer cset numid=3 <n> 
    
Update the firmware:

    sudo rpi-update

Plug in your USB microphone. Let’s open up an ALSA configuration file in vim:

    sudo nano /etc/modprobe.d/alsa-base.conf

Change the following line:

    options snd-usb-audio index=-2

To this:

    options snd-usb-audio index=0

Back in the shell, run:

    sudo alsa force-reload

Next, test that recording works (you may need to restart your Pi) by recording some audio with the following command:

    arecord temp.wav

Make sure you have speakers or headphones connected to the audio jack of your Pi. You can play back the recorded file:

    aplay -D hw:1,0 temp.wav



2.2 Install Pocketsphinx
Pocketsphinx is a opensource project for speech recognition. For mor information please see: http://cmusphinx.sourceforge.net/wiki/download/
  
  Installation Instructions:
      
  Let’s download and unzip the sphinxbase and pocketsphinx packages:
      
    wget http://downloads.sourceforge.net/project/cmusphinx/sphinxbase/0.8/sphinxbase-0.8.tar.gz
    wget http://downloads.sourceforge.net/project/cmusphinx/pocketsphinx/0.8/pocketsphinx-0.8.tar.gz
    tar -zxvf sphinxbase-0.8.tar.gz
    tar -zxvf pocketsphinx-0.8.tar.gz
      
  Now we build and install sphinxbase:

    cd ~/sphinxbase-0.8/
    ./configure --enable-fixed
    make
    sudo make install
      
  And pocketsphinx:

    cd ~/pocketsphinx-0.8/
    ./configure
    make
    sudo make install
      
  Once the installations are complete, restart your Pi.


