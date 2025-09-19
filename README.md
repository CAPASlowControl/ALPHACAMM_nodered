IAXO ZGZ nodered
===
***

This repository includes the nodered flows of the AlphaCAMMIAXO Zgz detector.

The repository is installed in `/home/iaxo/.node-red/`.

Functionalities or code that need To Be Checked is marked as (<mark>TBC</mark>).

# Flows

The code is composed of the following flows:

 - Bronkorst:
	 + Pressure controler
		 * At line output
		 * Bronkhorst *P-702CV-6K0A-MBD-33-V*
		 * SerialPort `/dev/APHCMM_S3` 
	 + Outlet Flow Controller 
		 * At line input
	  	 * Placed at the line outlet
	 	 * Bronkhorst *F-201CB-200-ABD-00-V*
	 	 * SerialPort `dev/APHCMM_S2` 
	 + Note: when the Bronkhorst relay is closed there is no communicatio.

 - Thyracont
	+ Pressure  Sensors
		+ S1: Line input
		+ S4 Line Output 
	+ Thyracont *VSR53USB*
	+ SerialPort `dev/APHCMM_S1` 
	+ SerialPort `dev/APHCMM_S4` 
	
 - PLC 
	+ Arduino UNO
	+ Temperature and Humidity Sensor
	+ Relays/ElectroValves Control:
		* V14: Before Detector (After Flow Controller, Before Radon system)
		* V5: Before Detector (After Radon System)
		* V8: After Detector
		* Bronkhorst: Power to Bronkhorst pressure and flow controllers

 - Database
	 + Postgressql Database
	 + Database: *alphacammdb*
	 + User: *iaxo*
	 + Password: *bujaruelo*

# NODERED NOTES

## Memory Leaks
Nodered is prone to memory leaks. 

To avoid memory leaks it is important to avoid errors in the code. In serial ports it is important to:

 - Check the status of the response from the serial port and filter the message only when the `msg.status` is  `OK`.
 - Send messages to the serialport only when the port is connected (<mark>TBC</mark>)
	 + If messages are always sent nodered is not able to reconnect upon a communication error.

## USB Configuration
The serialport configuration is included in `/etc/udev/rules.d/99-sub-serial.rules

For information on the serial ports  `devadm info --name=/dev/<device>`

## Credentials
Credentials are set in `settings.js`.

Credentials are encryptes usin `node-red admin hash-pw`.

# TODO LIST

- Include Input check in serialports