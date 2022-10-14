Description

A simple script to dynamically download and display movie posters based on “now playing” information pulled from minidlna. 
The project uses low cost hardware ( raspberry pi zero ) to display posters via HDMI and is intended to be lightweight.

Technical theory of operations 

The Model works in a client-server architecture. The client being the RPI display device, the server a Linux based DLNA sever, readymedia or minidlna. A remote mount session is created between the mini dlna sever and the client (RPi poster device) to pull the minidlna log data. When a movie is played through a DLNA request, the script monitors the minidlna.log file for any updates.

The file name is pulled from the log and is parsed using the PTN library. The movie title name is then fed into imdby/cimeongoer to “search” for the appropriate movie poster. The poster is downloaded and Finally , displayed using FBI ( frame buffer ) via raspberry pi CLI.

Limitations 

The script will fail unfortunately if no movie name is found. 

The script is roughly 95% accurate  however sometimes returns the wrong movie. This is a limitation of the the search function unless index selection is implemented. See features needed to be implemented. 


Because of the limitations of minidlna , there is no API or way to pull data other than log parsing. 

The log does not provide the current host. If another movie is played on a different device for instance if you have multiple  DLNA clients , the script will overwrite what’s on the screen. It is intended for 1:1 sever to movie playing.


Hardware requirements

Raspberry pi (Peferrably Rpi Zero W)
Dietpi or raspbian light 
Hdmi display 

Required Linux software 

 fbi 
 Python3
 Python pip
 SSHFS 
 

Required python libraries 

Pip install 

Parse-torrent-title 
IMDbpy
Cinemongoer


Instructions 

SSH to server running minidlna 
Modify the minidlna log level to “info”
Restart mini dlna services 
Verify log directory location typically /var/log/minidlna 

Log into rpi client ( movie poster device )

Create directory mount on client device pointing 
Example: sshfs username@dlna-server:/var/log/minidlna/ /mnt/remote-minidlna/

Update the script to include 

Run python3 movie-poster. 


Features to be implemented

More accurate parse algorithm 
Easy Install / Pre-req script 
Better error handling when no movie is found 
Index selection via GPIO button 
Movie timeout 

![My Image](IMG_5004.jpeg)
