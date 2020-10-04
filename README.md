# pimpmykali.sh

# Fixes for new imported Kali Linux virtual machines
- could be used on a bare metal machines, but thats on you

# Github index updated added +x permission: 
- Script should now be executable upon clone (perms: 755 rwxr-xr-x added to github) 
  - you should not need to chmod +x pimpmykali.sh upon git clone anymore

# Installation script:
- rm -rf pimpmykali/
- git clone https://github.com/Dewalt-arch/pimpmykali
- cd pimpmykali
- sudo ./pimpmykali.sh

# Revision 0.5c - fix_upgrade removed from fix_missing 
   - fix_upgrade removed from fix_missing and is no longer 'forced' as a part of fix_missing 
   - fix_upgrade will now only be called as a part of fix_all (menu 0) or fix_upgrade (menu 9)
     or command line switches --upgrade -upgrade or upgrade 
   - general code cleanup, some additional comments added

# Revision 0.5b - Blindpentesters Essential Collection added
   - added Blindpentesters 'The Essentials' tools and utils collection 
   - menu option 'B' for blindpentesters tools collection, installs, runs the_essentials.sh and exits

# Revision 0.5a - cosmetic fixes
  - minor cosmetic fixes to pimpmyupgrade functions

# Revision 0.5 - pimpmyupgrade added
   - fix_sources deb-src is not enabled in /etc/apt/sources.list - fixed
   - linux-headers-(uname -r) are not installed - fixed
   - new functions check_vm, virt_what, run_update are what comprise pimpmyupgrade
   - virt_what determines if vm is under virtualbox or vmware
   - check_vm checks for virtualbox or vmware and installs proper drivers for each
   - run_update runs fix_sources, runs apt upgrade calls virt_what, calls check_vm
   
# Revision 0.4b : minor updates
   - reworked fix_section works much better now
   - added slient 'mode' variable, uncomment silent= line to turn output on and off from apt etc 
   - misc cleanup in the script

# Revision 0.4a : 2nd warning screen added for --borked impacket removal system
   - If you cant have a little fun with your own scripts your doing something wrong....
   - last chance warning screen ( mostly novelty ), random launch code generation on each run of --borked
   - list of target selection, targets locked, etc 
   - seriously if you made it to --borked 2nd warning your having a bad day with impacket.. enjoy the giggle
   - 10 second wait timer added to last chance launch screen before operations are preformed
   - if no ctrl+c is entered to cancel the operation, fix_sead is run, followed by fix_impacket
   - added apt -y reinstall python3-impacket impacket-scripts to fix error with smbmap after impacket removal

# Revision 0.4 : Major Update for impacket removal
   - added flameshot as a part of the missing group to be installed
   - added clamav-exec.nse wget to fix clamav-exec.nse failed during nmap --script vuln scans
   - new commandline switch of --borked has been implemented for removal of impacket across various locations
   - added --borked notice to menu system, help system
   - added warning screen for --borked, only input of Y will proceed anything else exits
   - fix_sead_warning, fix_sead_run, fix_impacket_array, fix_impacket all executed in order with --borked
     - fix_sead_run removes any and all directories named impacket* in the following locations (you have been warned): 
        /opt /usr/bin /usr/local/lib /usr/lib /home/$finduser/.local/bin /home/$finduser/.local/lib ~/.local/lib ~/.local/bin
      - fix_sead_run, also removes via fix_impacket_array any .py or .pyc related to impacket in the following: 
        /usr/bin/$impacket_file /usr/local/bin/$impacket_file 
         (root)~/.local/bin/$impacket_file 
         (user)/home/$finduser/.local/bin/$impacket_file

# Revision 0.3d
  - added flameshot to fix_missing as a part of the default installed tools
  - emergency fix to --force, everything should be functioning now

# Revision 0.3c: 
  - per request kali-root-login enabling prompt has been reworked and reworded to be less confusing and
    to give the user a better explaniation of what the script is doing at that stage 
  - added to note that if you dont understand what this part of the script is doing hit N
  - added colors for syntax highlighting in the onscreen messages of the script in places
  - added fix_nmap function for fixing /usr/share/nmap/scripts/clamav-exec.nse (commented out at this time
    clamav-exec.nse was an issue at one time but unknown if it is still relevent)
  - --force command line argument was being called without setting $force in fix_all $force - fixed

# Revision 0.3b: 
  - bug fix ( Thanks ShadeauxBoss! for finding it ) impacket installation was missing cd /opt/impacket-0.9.19 
  - feature request added : Gedit installation menu option 7, is included in fix_missing, all and force
  - remove clear from exit screen

# Revision 0.3a: 
- the extraction of the impacket-0.9.19.tar.gz was leaving /opt/impacket-0.9.19 with 700 perms
  and an ownership of 503:root, this has been changed to ownership root:root and all files inside
  /opt/impacket-0.9.19 have had their permissions set to 755 after extraction of impacket-0.9.19.tar.gz
- Ascii art added to the menu
  
# Revision 0.3: 
- added checks for already installed installations, added --force command ( --force will run all fixes/reinstalls )
- fix_impacket function : added both .py and .pyc files to impacket removal array
  - added on screen notification of files being removed by the array
- fix_missing function  : has been reworked new vars check section force type
  - added fix_section function : fix_section is the workhorse for fix_missing
- reworked python-pip installation to its own function python-pip-curl and installs python-pip via curl 

# Revision 0.2: 
- Added colorized notifications, help system, command line arguements, case based menu system
- valid command line arguements are: help, all, go, grub, impacket, missing, menu, smb, grub, root
- anything other than --all or -all or all , will only run that function and then exit.
- command line arguements can be used with -- or - or just the word itself to try can catch for all possible cases
 
- example command line var: --help or -help or help will catch help and works for all valid command line arguements
  anything other the command line arugement catch exits and displays help 

# Fixes : 
- python-pip now removed from kali repos, installation via curl 
- python3-pip not installed
- seclists not installed
- golang not installed 
- kali-root-login not installed and reneables root login
  - reworked and added prompt
- impacket-0.9.19
  - removes any prior installation of impacket (gracefully and forcefully)
  - installs impacket-0.9.19 
  - installs python-pip via curl 
  - installs python wheel
- /etc/samba/smb.conf
  - adds the 2 lines below [global] for min max protocol
  - client min protocol = CORE
  - client max protocol = SMB3
- grub added detection of default /etc/default/grub
  - added mitigations=off 

# TODO   
- .bashrc alias and functions ( currently commented out and is not a part of the running script ) 
  - adds command ex function to extract from any archive with 1 command ex 
  - vpnip - displays tun0 ip address in the terminal via vpnip alias 
  - added /sbin to user path, can now ifconfig without sudo
