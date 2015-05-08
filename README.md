Bloating
=======

Atmospheric monitoring app for logging and graphing beer fermenation temperatures overtime using a Raspberry Pi and a DS18B20

Currently this documentation assumes you are running Raspian on a Raspberry Pi.

Automatic Setup (with Puppet)
-------------------------------

    ssh pi@[hostname]
    git clone https://github.com/marvinstuart/bloating.git
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install puppet
    chmod 755 bloating/puppet/puppet-install.sh
    ./bloating/puppet/puppet-install.sh
    sudo reboot 

Ignore message: 
warning: Could not retrieve fact fqdn
warning: Host is missing hostname and/or domain: sensor

Create a SQLite database called log.db in the atmospi directory.

sqlite3 log.db
CREATE TABLE Devices(DeviceID INTEGER PRIMARY KEY, Type TEXT, SerialID TEXT, Label TEXT);
CREATE TABLE Temperature(DeviceID INT, Timestamp INT, C REAL, F REAL);
CREATE TABLE Humidity(DeviceID INT, Timestamp INT, H REAL);
CREATE TABLE Flag(DeviceID INT, Timestamp INT, Value TEXT);
CREATE INDEX temperature_dt ON Temperature(DeviceID, Timestamp);
CREATE INDEX humidity_dt ON Humidity(DeviceID, Timestamp);
CREATE INDEX flag_dt ON Flag(DeviceID, Timestamp);
.exit

DS18B20 Wiring Diagram
-------------------------------
http://www.reuk.co.uk/OtherImages/raspberry-pi-ds18b20-connections.jpg

View Temperature Information realtime 
------------------------------------

http://raspberrypi_ip

DS18B20 serial ID Name Change - Optional
-------------------------------
Sensors will be automatically labeled with their serial ID. If you would like to change this label, run the following query for each sensor: Write down the SerialID you see from http://raspberrypi_ip 

     sqlite3 log.db
	UPDATE Devices SET Label = "New label Name" WHERE Type = 'ds18b20' AND SerialID = '28-000000000001';
	.exit


Shoutout credit to Micahel for wrting the orginal code https://github.com/mstenta
