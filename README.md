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