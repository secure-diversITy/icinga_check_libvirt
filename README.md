## Check your KVM host by Icinga / Nagios

###  Usage

        install virsh on icinga/nagios host

	check the nagios user can connect to remote libvirt machine
	ex. sudo -u nagios virsh -c qemu+ssh://user@remote.libvirt.machine/system --readonly list

	If all looks good put the command into your icinga/nagios

	check_libvirt -H remote.libvirt.machine -m mode <-w warning -c critical>

	-H (libvirt host)
	The remote libvirt host
	!!! mandatory argument !!!

	-n (VM name)
	mandatory when -m net_stats
	The VM name to be checked

	-u (username)
	Username to connect to hypervisor
	!!! mandatory argument !!!

	-t (connection type)
	currently only qemu+ssh supported, this is default"     

        -p (ssh port)
          if not standard 22 you can define a different port here
        
	-k (ssh key)
	the full path to a ssh key (optional)

	-i (interface name)
	mandatory when -m net_stats
	available interface names can be listed by e.g.:
	sudo -u nagios virsh -c "qemu+ssh://user@host/system" --readonly domiflist <vm-name>

	-m (mode):
	    vm_status
	        check virtual machines status (running,paused etc...)
	        returns WARNING when one ore more VM powerwed off or paused
	        returns CRITICAL when one or more VM crashed

	    pool_status
	        check defined storage pools
	        returns warning when inactive pool founded

            pool_usage
		check all active pool usage

	    net_stats
	        retrieve network statistics (requires -i)

	-w (warning)
	Warning threshonld in percentage
	Default: 80%

	-c (critital)
	Critical threshold in percentage
	Default: 95%

