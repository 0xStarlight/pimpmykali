# pimpmykali.sh

[![pmk132tkab.png](https://i.postimg.cc/Qd9VCRrd/pmk132tkab.png)](https://postimg.cc/18SyY7tk)

# Fixes for new imported Kali Linux virtual machines
  - Author assumes zero liability for any data loss or misuse of pimpmykali
  - Can be used on a bare metal machines, but thats on you
  - Menu breakdown added below revision history

# Github index updated added +x permission:
  - Script is now be executable upon clone (perms: 755 rwxr-xr-x added to github)
  - There is no need to chmod +x pimpmykali.sh upon git clone

# Installation script:
  - rm -rf pimpmykali/
  - git clone https://github.com/Dewalt-arch/pimpmykali
  - cd pimpmykali
  - sudo ./pimpmykali.sh
  - For a new kali vm, run menu option N

# Special Thanks to Pimpmykali-Mirrors Testers!!
  - Crazy_Man - https://github.com/The-Crazy-Man
  - Andro

# Code Contributors
  - blindpentester https://github.com/blindpentester
  - pswalia2u https://github.com/pswalia2u
  - Alek https://github.com/onomastus
  - Gr1mmie https://github.com/Gr1mmie
  - Aksheet https://github.com/Aksheet10
  - 0xC0FFEE Home Lab Build
    https://docs.google.com/document/d/1DH-epmXJMvQtOnDQYa3zUXvq9497Mm3276K8frNz2UM

# Revision 1.3.2 - Pimpmykali-Mirrors and updates
  - Speedtest for kali linux repo mirrors (http only at this time)
  - This function will only be executed via menu option =  
  - menu option = Pimpmykali-Mirrors (Yes it is literally the = (equals character)
    - obtain kali mirror list and process
      - round-trip-time ping test to all mirrors, select top 10 with shortest rtt
      - small download >1MB from the top 10 mirrors, select top 5 fastest transfers
      - large download 10MB test the final 5 mirrors, select fastest transfer
    - generate new /etc/apt/sources.list with the new selected mirror
      - prompt Y or N to write new changes to /etc/apt/sources.list
        - Y writes changes /etc/apt/sources.list
        - create backup of original sources.list in /etc/apt/sources.list_date_time
        - write new deb and deb-src lines with new mirror to /etc/apt/sources.list
        - N exits and makes no change to /etc/apt/sources.list
  - added --mirrors for command line use sudo./pimpmykali.sh --mirrors

  - new menu option T - reconfigure timezone (new function)
    - calls sudo dpkg-reconfigure tzdata

  - new menu option K - reconfigure keyboard, language, layout (new function)
    - calls sudo dpkg-reconfigure keyboard-configuration

  - menu option 6 - enable root login
     - password prompt now checks exit code if failure, restart password function
     - copy of files from /home/kali/* to /root now uses the actual username not just 'kali'

  - menu option L - Sublime text editor
    - installs sublime text editor

  - functions updated: fix_smbconf fix_grub and fix_sources
    - function updated to use sed -i instead of prior method  

  - Menu clean up, added bold color to "New VM Setup" Menu option N

  - Added Sublime text editor installer - Menu Option L

  - install_atom function
    - removed quiet switches to avoid confusion

  - python2 deprecation warnings - disabled 

  - Alphabetically sorted Main Menu - Stand Alone Functions

  - Revision History for 1.3.1 and 1.3.0 moved to changelog.txt

  - Yes, this really was just 1 update to pimpmykali
  - Minor code cleanup

# Menu Breakdown of Pimpmykali

- Menu option N  (New Users/New VM's Should start here!)
  - executes menu option 0 fix all ( menu options 1 thru 8 )
  - executes menu opiion 9 (pimpmyupgrade)

- Menu option = Pimpmykali-Mirrors (rev 1.3.2)
  - obtain kali mirror list and process
    - round-trip-time ping test to all mirrors, select top 10 with shortest rtt
    - small download >1MB from the top 10 mirrors, select top 5 fastest transfers
    - large download 10MB test the final 5 mirrors, select fastest transfer
    - generate new /etc/apt/sources.list with the new selected mirror
    - prompt Y or N to write new changes to /etc/apt/sources.list
      - Y writes changes /etc/apt/sources.list
      - create backup of original sources.list in /etc/apt/sources.list_date_time
      - write new deb and deb-src lines with new mirror to /etc/apt/sources.list
      - N exits and makes no change to /etc/apt/sources.list

- Menu Option 1 - Fix missing
  - fix_sources
    - uncomment #deb-src from /etc/apt/sources.list
  - python-pip installation via curl
  - python3-pip installed
  - seclists installed
  - gedit installed (feature request)
  - flameshot installed (feature request)
  - locate installed (feature request)
  - fix_rockyou function
    - gunzip /usr/share/wordlists/rockyou.gz to /usr/share/wordlists/rockyou.txt
  - fix_golang function
    - installs golang
    - adds golang GOPATH to .bashrc and .zshrc
  - installs htop
  - installs python requests
  - installs python xlrd==1.2.0
  - disables xfce power management
  - blacklists pcspkr kernel module /etc/modprobe.d/nobeep.conf

- Menu Option 2 - Fix smb.conf
  - Fix /etc/samba/smb.conf
    - adds client min protocol = CORE  below [global]
    - adds client max protocol = SMB3  below [global]

- Menu Option 3 - Fix Golang
  - Installs golang
    - checks for GOPATH in .bashrc and .zshrc
    - if GOPATH is found, adds nothing
    - if not found, adds GOPATH statements to both .zshrc and .bashrc

- Menu Option 4 - Fix Grub
  - adds mitigations=off to GRUB_CMDLINE_LINUX_DEFAULT

- Menu Option 5
  - installs Impacket-0.9.19

- Menu Option 6 - Enable root login
  - installs kali-root-login
    - prompts for root password
    - copy /home/kali/* to /root prompt (1.1.2)
    - prompt are you sure? to copy /home/kali to /root prompt (1.1.3)

- Menu Option 7
  - installs Atom text editor

- Menu Option 8 - Fix Nmap
  - wget nmap script fixes
    - clamav-exec.nse
    - http-shellshock.nse (Thank you Alek!)

- Menu Option 9 - Pimpmyupgrade
  - additional notes will be added
  - fix : Hypervisor detection (vmware, virtualbox, qemu/libvirt)
    - add additional details here
  - fix : virtualbox shared folder fix applied     

- Menu Option 0 - Fix all (1-8)
  - Executes ONLY Menu options 1 thru 8

- Menu Option P - Disable Power Management
  - Based upon detection disable power management for that environment
  - Detect desktop environment
    - XFCE
    - Gnome

- Menu Option F
  - Fixes XFCE Broken Icons "TerminalEmulator" Not Found
  - Fixes XFCE Open Catfish instead of Thunar when double clicking Home or FileSystem Icon
    - this fix is a temporary fix and will be removed once xfce has been corrected

- Menu Option W
  - Install GoWitness precompiled binary

- Menu Option G
  - Apply gedit unable to open display as root fix

- Menu Option C
  - Install Google-Chrome

- Menu Option V
  - Install MS VSCode

- Menu Option S - Fix Spike
  - Fixes undefined symbol error thrown when using generic_send_tcp
    - this fix is temporary and will be removed once a corrected version is available

- Menu Option D - Downgrade metasploit-framework from 6 to 5
  - downgrades metasploit-framework (msfconsole) from msf6 to msf5
  - this is a temporary solution and will eventually be removed once a corrected version is available

- Menu Option ! - Nuke Impacket (yes its literally the ! character)
  - removes any prior installation of impacket (gracefully and forcefully)
    - installs impacket-0.9.19
    - installs python-pip via curl
    - installs python wheel

- Menu Option B    
  - BlindPentesters The_Essentials tools and utilities collection
    - Install all of BlindPentesters favorite tools and utilities to /opt (aprox 8GB)
    - Click the link below for a full list of the_essentials.sh script and its inner workings
    - https://github.com/blindpentester/the-essentials

- Menu Option Q
  - Set Qterminal for unlimited scrollback
     - check for HistoryLimited=True in ~/.config/qterminal.org/qterminal.ini
       - if found set HistoryLimited=False (unlimited scrollback)
       - if already set to False, exit function     

# TODO   
  - clean up todo list :)
