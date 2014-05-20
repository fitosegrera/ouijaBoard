ouijaBoard
==========
###Ouija board installation guide:

Created by: fito_segrera
http://fii.to/

Special thanks to the JasperProject http://jasperproject.github.io/

###Method 1 (Eassy)

Download the Raspberry Pi Image from this link: http://fii.to/downloads/ouijaBoard.tar.gz unzip and create a new raspberry pi SD card with it. Please use an 8 GB Sd card for this (note: please make sure that the SD card you are ussing is supported by the RBpi... please see: http://elinux.org/RPi_SD_cards)

###Method 2 (The HARDCORE way)

2.1 Download Raspbian (TALK ABOUT THE STEPS FOR THIS)

2.2 Install Pocketsphinx
Pocketsphinx is a opensource project for speech recognition. For mor information please see: http://cmusphinx.sourceforge.net/wiki/download/
  
    #Installation Instructions:
      
      Let’s download and unzip the sphinxbase and pocketsphinx packages:
      
      wget http://downloads.sourceforge.net/project/cmusphinx/sphinxbase/0.8/sphinxbase-0.8.tar.gz
      wget http://downloads.sourceforge.net/project/cmusphinx/pocketsphinx/0.8/pocketsphinx-0.8.tar.gz
      tar -zxvf sphinxbase-0.8.tar.gz
      tar -zxvf pocketsphinx-0.8.tar.gz
      
      #Now we build and install sphinxbase:

      cd ~/sphinxbase-0.8/
      ./configure --enable-fixed
      make
      sudo make install
      
      #And pocketsphinx:

      cd ~/pocketsphinx-0.8/
      ./configure
      make
      sudo make install
      
      #Once the installations are complete, restart your Pi.


