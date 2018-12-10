Version 3.4.20-141 - November 2018
  - Driver now uses local workqueues instead of system workqueues. 
    (SuSE BZ: 1078376)
  - Driver refactoring to match kernel.org version of the hpsa driver.
  - Kernel compat work for SLES15.
Version 3.4.20-125 - March 2018
  - Clear tempdevice before use in update_scsi_devices 	
  - Correct smart_path_enabled - turn on/off ioaccel status on a 
    per LUN basis instead of using brute force
  - Mark hpsa_scan_start as in progress to avoid BMIC set/clear config 
    operations. 
  - Correct wait for outstanding commands
Version 3.4.20-100 - August 2017
  - Correct a multipath failover condition where the driver could get 
    overloaded.
Version 3.4.18-105a - June 2017
  - Added missing dkms.conf file.
Version 3.4.18-105  - April 2017
  - The 3.4.18-105 is the same code base used for 3.4.18-108 binaries rebuilt 
    for the final release of RHEL6.9.
  - Corrected reset operation that in rare cases could offline a disk.
  - Added hpsa_lockup_action driver parameter
    "0 = disable device, 1 = panic system, 2 = reboot"
  - Minor driver performance tweaks.
  - Updated reset policy for storage enclosures.
  - Updates to offline detection code.
Version 3.4.16-145  - September 2016
  - New Makefile that automatically determines the kernel and adjusts
    the source accordingly.  Just type "make".
  - Added dkms.conf file.  Helpful for Ubuntu and Debian. Details below.
  - Improved performance by avoiding "spare" drives when doing drive inquiries.
    No longer causing a wait on the spare drives to spin up.
  - Reduced chatty log messages.
  - Adjustments made to the SSD Smart Path code.
  - Addressed possible hot-plug issue when the controller is in HBA mode.
  - Improved MSIX initialization to avoid reverting to legacy interrupts.
  - Adjustment to keep faulty drives from hanging the driver during a rescan.
Version 3.4.14-115  - April 2016
  - Enabled operation with third party external RAID enclosures.
  - Improved device reset recovery behavior.
  - Note - Binary driver packages numbered 3.4.14-116 and 3.4.14-117 are
    based on the indentical source version 3.4.14-115.  They were late builds
    to pick up Gold Master releases of several Linux distros.
Version 3.4.12-110  - October 2015
  - Fixed multilun issue that would occur during multipath installations.
  - Cleaned up driver rmmod issue.
Version 3.4.10-120  - June 2015
  - Adds in sysfs entry for manipulating controller lockup behavior: 
      0 -- default, fail commands and disable device, 
      1 -- panic, 
      2 -- reset server
  - Updates to abort code.
  - Added notes below for Ubuntu compiles.
Version 3.4.8-140  - March 2015
  - Improvements made to abort and reset handling.
  - Improvements made to HBA mode support.
Version 3.4.6-170  - September 2014
  - Update to address a device discovery issue (mostly involving
    tape drives) that was found in hpsa version 3.4.6-165.
Version 3.4.6-165  - September 2014
  - Driver updated to support HP Proliant Gen9 servers with new Smart Array
    and Smart HBA controllers.
  - Many changes to support HBA mode on these new controllers.
  - Driver updates to increase performance especially for SSDs.
  - **NOTE** This version has a known device discovery issue (mostly involving
    tape drives) that will be addresses in the 3.4.6-170.
Version 3.4.4-126  - July 2014
  - Cleaned up memory leak that would occur at device discovery.
Version 3.4.4-125  - January 2014
  - Added HP SSD Smart Path feature.
    http://h18004.www1.hp.com/products/servers/proliantstorage/software-management/smartpath/index.html
  - Updated controller support.
Version 3.4.2-5  - October 2013
  - Fixed chatty debug messages when running hpsa and HP agents.
Version 3.4.2-4  - September 2013
  - Additional Smart Array Controller support.
  - With this version log messages can be chatty if you are running the Hp 
    agents.  This will be fixed shortly.
Version 3.2.0-3  - March 2013
  - Update to Smart Array controller IDs.
  - Added driver parameter (hpsa.reply_queues=4) to allow tuning of reply 
    queues. Default is 4 with a max of 16.
  - Fixed command status return necessary to avoid data inconsistency typically
    in a multipath environment.
Version 3.1.0-7
  - Fixed command status return necessary to avoid data inconsistency.
    Typically found in multipath configurations.
Version 3.1.0-5
  - Fixed device reset value to avoid reset failure.
Version 3.1.0-4
  - Added multiple reply queue support to driver.

DKMS helps insure a driver (like hpsa) gets rebuild for each kernel update
that happens on a system.
  http://linux.dell.com/dkms
  http://help.ubuntu.com/community/DKMS

Steps for using DKMS and the hpsa driver source with Ubuntu:
  - Insure dkms and compiler tools are installed.
    - apt-get install dkms build-essential
  - Unpack hpsa source tarball
  - cd to "drivers" directory
  - copy the scsi subdirectory to /usr/src/hpsa-<driver_version>
    - Note DKMS does not support the "-" in the version number. 
      Substitute with ".".
    - EX. cp -a scsi /usr/src/hpsa-3.4.16.145
  - dkms add -m hpsa -v 3.4.16.145
  - dkms build -m hpsa -v 3.4.16.145
  - dkms install -m hpsa -v 3.4.16.145

To provide kernel/driver development feedback, send email to 
esc.storagedev@microsemi.com.
License: GPLv2
March 2018
