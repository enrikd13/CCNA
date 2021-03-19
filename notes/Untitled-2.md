■ RAM: Sometimes called DRAM, for dynamic random-access memory, RAM is used by the switch just as it is used by any other computer: for working storage. The running
(active) configuration file is stored here.
■ Flash memory: Either a chip inside the switch or a removable memory card, flash memory stores fully functional Cisco IOS images and is the default location where the switch gets its Cisco IOS at boot time. Flash memory also can be used to store any other files, including backup copies of configuration files.
■ ROM: Read-only memory (ROM) stores a bootstrap (or boothelper) program that is loaded when the switch first powers on. This bootstrap program then finds the full Cisco IOS image and manages the process of loading Cisco IOS into RAM, at which point Cisco IOS takes over operation of the switch.
■ NVRAM: Nonvolatile RAM (NVRAM) stores the initial or startup configuration file that
is used when the switch is first powered on and when the switch is reloaded.

copy running-config startup-config

write erase 
erase startup-config
erase nvram:

reload

erase startup-config 
delete vlan.dat
reload 

show mac address-table dynamic
show interfaces status
show interfaces f0/1 counters

switch will remove the entries due to age (default of 300 seconds on many switches) , due to the table filling, and you can remove entries using a command.
mac address-table aging-time time-in-seconds [vlan vlan-number]
clear mac address-table dynamic