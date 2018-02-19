5-Switch_VXLAN with MLAG Configurations
============================================
The flatfiles in this repository will set up a BGP unnumbered routing fabric between the leafs and spines, will configure MLAG between the two top-of-rack switches and one server in that rack, and then make a VXLAN (VNI 13) for network 10.2.4.0/24. 

Topology
--------
This demo runs on a spine-leaf topology with single dual-attached host running with uplink mlag, and single attached host with standalobe leaf. The ansible playbook requires an out-of-band management network that provides access to eth0 on all of the in-band devices. Toplogy picture is attached in the zip file package.


Playbook Package
================

Pre-resiquite
-------------

1. Make sure Ansible is configured. 
2. Make sure switches have latest OS, are with default configuration and with license installed.
3. Make sure switches are with default configuration and with license installed.
4. Server must be running Ubuntu 16.04 or later.
5. Physical connection should be exactly same as shown in topology file.


Running this playbook will configure the system based on the topology attached in this package. The directory will contain following files and sub-directory:

1. deploy_5-sw-evpn-vxlan.yml		# No change required. 
2. hosts				# Inside the file, Change Management IP address of the switches and servers (in this example, servers are named as network is configured with DNS settings).
					# Inside the file, Change the name of your switches or servers to exactly matching this file, or change this file as per your switch name. If you change this file, then change the folder names under inventory folder too.
					# Inside the file, Change the password of switches.
3. ansible.cfg				# No change required.
4. roles/				# Sub folder carring configurations.
5. roles/<switch/server>		# Switch/server = exact host name of the server or switch. This needs to be same as defined in "hosts" file.
6. roles/<sw_name>/interfaces		# Interfaces file under inventroy/<sw_name>/ contains the details of /etc/network/interfaces configuration of switch.
					# IMPORTANT - Look for MGMT interface name and change in configurations, if you will run the script with incorrect name, you may loose connection with the server after you run the script.
					# Inside the file, Change the port speeds for swp7 for different host speeds.
7. roles/<server_name>/interfaces	# Interfaces file under inventroy/<server_name>/ contains the details of /etc/network/interfaces configuration of server. 
					# IMPORTANT - Look for MGMT interface name and change in configurations, if you will run the script with incorrect name, you may loose connection with the server after you run the script.
					# Change the interface names for data plan - so right configuration can be done on servers.
8. roles/<sw_name>/Quagga.conf		# No change
9. roles/<sw_name>/daemons		# No change




Running Configuration Package
=============================

Pre-resiquite
-------------

1. Make sure switches are with default configuration and with license installed.
2. Server must be running Ubuntu 16.04 or later. Other servers can be used, but the config files here are for Ubuntu.
3. Physical connection should be exactly same as shown in topology file.

Following files for direct pasting the configurations as per the topology diagram

1. <swicth_name>			# <swicth_name = spine01; spine02; leaf01; leaf02; leaf03>
					# Configurations will not define any MGMT interface, please have it configured separetly.
					# Change the link speed as required in placed marked with ##ChangeME section in txt file (before you paste the configuration).
					# Do "net pending" to make sure all configuration went in.
					# Do "net commit" to save the configuration
					# Use proper show commands to check configurtaions.
2. <server_name>			# <server_name = your server1; your server2>
					# define any MGMT interface, please have it configured separetly.
					# Change the link speed as required in placed marked with ##ChangeME section in txt file (before you paste the configuration).
					# Reboot after you paste the configuration.

