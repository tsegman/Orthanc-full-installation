# Orthanc-full-installation
Instructions to install Orthanc DICOM server with plugins on Proxmox CT running Ubuntu Server Create CT DNS 8.8.8.8

Update Ubuntu

 apt update && apt upgrade -y
Add user

 sudo adduser tsegman
Add user to root privileges

 sudo adduser tsegman sudo
Switch user

 sudo su - tsegman
Reboot to take effect

 sudo reboot
install Orthanc and dependencies

 sudo apt install orthanc
  sudo apt install orthanc-dicomweb
  sudo apt install orthanc-gdcm
  sudo apt install orthanc-imagej
  sudo apt install orthanc-mysql
  sudo apt install orthanc-postgresql
  sudo apt install orthanc-python
  sudo apt install orthanc-webviewer
  sudo apt install orthanc-wsi
Commands to start,stop and restart

 sudo service orthanc start
 sudo service orthanc stop
 sudo service orthanc restart
Changes inside configuration file

 sudo nano /etc/orthanc/orthanc.json
Βρες

"RemoteAccessAllowed" : false, 
#και καντο true και

"DicomModalities" : {

"DR" : [ "DRPC", "192.168.0.122", 11112 ]
Restart service

sudo service orthanc restart
install Orthanc explorer 2

sudo wget -O libOrthancExplorer2.so https://orthanc.uclouvain.be/downloads/linux-standard-base/orthanc-explorer-2/mainline/libOrthancExplorer2.so
 sudo mv libOrthancExplorer2.so /usr/share/orthanc/plugins/
 sudo service orthanc restart
 sudo nano /etc/orthanc/credentials.json
Σβήνεις τα πάντα και paste

{ "RegisteredUsers" : { "tsegman" : "280783" } }

sudo nano /etc/orthanc/orthanc.json
Στο τέλος paste:

"OrthancExplorer2" : { "Enable": true, "IsDefaultOrthancUI": true },

sudo systemctl restart orthanc
install OHIF Viewer

sudo wget https://orthanc.uclouvain.be/downloads/linux-standard-base/orthanc-ohif/1.7/libOrthancOHIF.so --output-document /usr/share/orthanc/plugins/libOrthancOHIF.so
 sudo systemctl restart Orthanc
Με την εντολή μέσα στο console του container βλέπεις  τον διαθέσιμο χώρο

 df -h 
