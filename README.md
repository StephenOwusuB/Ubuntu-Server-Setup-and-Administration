# Ubuntu Server Setup, Deployment and Management

## Table of Contents
- [Ubuntu Server Setup, Deployment and Management](#ubuntu-server-setup-deployment-and-management)
  - [Table of Contents](#table-of-contents)
  - [Objectives](#objectives)
  - [Languages and Utilities Used](#languages-and-utilities-used)
  - [Environment](#environment)
  - [Project Walk-Through](#project-walk-through)
  - [Skills Learned](#skills-learned)
  - [Acknowledgments](#acknowledgments)

## Objectives

In this project, we will set up a Ubuntu Server 26.04 LTS (Long Term Support) versions provide: on our local laptop using virtual box. This hands-on lab aims to enhance our understanding of setting up, configuration, deployment, managing and securing an organization's linux server environment by by establishing best practices and implementing baseling security measures. Configuring and managing this lab has significantly contributed to my knowledge of maintaining a Linux-based environment.

## Languages and Utilities Used

- **Git**: For version control and collaboration.
- **Visual Studio Code**: As the primary code editor for writing and managing scripts.
- **Markdown**: For creating detailed documentation and guides.
- **VirtualBox**: To create and manage virtual machines for testing and deployment.
- **Ubuntu Server 26.04 LTS**: The operating system used for the server environment.

## Environment

To set up a Ubuntu Server 26.04 LTS environment and secure it, you will need the following components:

- **Ubuntu Server 26.04 LTS**  
    - Install Ubuntu Server 26.04 LTS on a virtual machine using VirtualBox.
    - Configure the network settings for the virtual machine.


## Project Walk-Through

1. **Download Ubuntu Server 26.04 LTS from: https://ubuntu.com/download/server#manual-install-tab**  
    ![Ubuntu Install](images/ubuntu%20install.jpg)

2. **Download and Install VirtualBox from: https://virtualbox.com**
    ![VirtualBox](images/virtualbox.jpg)

3. **Create a new virtual machine in VirtualBox and install Ubuntu Server 26.04 LTS.**  
    To begin creating your Ubuntu Server virtual machine in VirtualBox, follow these steps:

    **Steps**

    a. Enter a **name** for your server.
    b. Under **Folder**, open the dropdown and select **Other**.
       - Choose a location where you want to store your Ubuntu Server files.
    c. Select the **ISO Image** option.
       - Browse and select your Ubuntu Server ISO file.
    d. Choose **Skip Unattended Installation**, then click **Next**.
    e. Configure system resources:
       - **Base Memory (RAM):** Set to your preferred value (example: 8192 MB)
       - **Processors (CPU):** Select the number of CPUs (example: 4)
    f. Leave **Enable EFI** unchecked, then click **Next**.
    g. Set the **Virtual Hard Disk size**:
       - Example: 80 GB (or based on your needs)
   h. Click **Next**, then **Finish** to complete the VirtualBox Ubuntu Server setup.
    ![VirtualBox](images/virtualbox.jpg)

4. **Language and Keyboard Setup** 
    During the initial setup of Ubuntu Server, you will be prompted to configure language and keyboard settings.

    **Steps**

    a. Select your preferred **Language** (e.g., English).
    b. Review the **Keyboard Layout**.
       - If the layout works correctly for your keyboard, continue.
    c. Ensure **Ubuntu Server** is selected.
    d. Use the **Arrow Keys** to navigate to **Done**.
    e. Press **Enter** to proceed.

    ![VirtualBox](images/virtualbox.jpg)

5. **Network Configurations** 
    Since this is a server, it is recommended to configure a static IP address to ensure the server always keeps the same network address.

    You can configure a static IP address in two ways:
      - On the router (DHCP reservation)
      - Directly on the server

    In this guide, we will configure it directly on the server.

    **Steps**

    a. Make sure the cursor is on `enp1s0` (the network adapter), then press **Enter**.
    b. Use the **Down Arrow** key to select **Edit IPv4**, then press **Enter**.
    c. Change the IPv4 method from **Automatic (DHCP)** to **Manual**.
    d. Enter the following network information:
      - **Subnet Mask**
      - **Static IP Address**
      - **Gateway**
      - **DNS Servers**

    **Important Notes**

     - Choose an IP address that is outside your router’s DHCP range to avoid IP conflicts.  
     Example: if your router assigns addresses from `.100` to `.150`, you could use something like `.200`.

     - For DNS servers, you can use:
       - Your Internet Service Provider's DNS servers
       - Public DNS servers such as Google's (`8.8.8.8`, `8.8.4.4`)

     - To find your current gateway and DNS information on a Windows computer, run:
     powershell
    **ipconfig /all** 
  
6. **Disk Selection and Partitioning**  
    In this step, you will select the storage drive and review the disk layout before installation begins.

    **Steps**
     
    a. Select the **drive** you intend to use for the installation.
    b. Review the **system summary** that is displayed.
       - This shows how the disk will be partitioned before installation.
    c. You will typically see:
       - A **boot partition**
       - A larger **root partition** (similar to the `C:` drive in Windows)
    d. Once you have reviewed the layout, select **Done** to proceed.
    e. A warning message will appear indicating that all data on the selected disk will be erased.
       - Select **Continue** to confirm and proceed with the installation. 

7. **Setup Admin and User accounts** 
    During the installation process, you will be prompted to create the administrator account for the server.

    **Steps**

    a. Enter a name for the administrator account, then press the **Tab** key.
    b. Enter the **Server Name**.
    c. Enter a **Username**.  
       - It is recommended to keep the username in lowercase.
    d. Enter a **Password**, then confirm the password.
    e. Once completed, select **Done** and press **Enter**.
    
    **Headless Server Setup and OpenSSH**
    In many cases, it is preferable to run a server without a monitor, keyboard, or mouse attached. This is known as a **headless server**.
    To manage a headless server remotely, you will need remote access software such as the **OpenSSH Server** package.
    Ubuntu Server provides several optional Snap packages during installation, including OpenSSH Server. However, I prefer to install the base operating system first and add additional software afterward.

    **Steps**
    a. Press the **Tab** key to highlight **Done**.
    b. Press **Enter** to continue the installation.

    **Completing the Installation**
    The installation process may take several minutes to complete.
    Once you see the message **Install Complete**:

    a. Press the **Tab** key twice to highlight **Reboot Now**.
    b. Press **Enter** to restart the server.

8. **Logging In and Using the Command Line**
    After installation, you can log into the server using the username and password you created.
    
    **What You Will See**
    Once logged in, you will be presented with the Linux command line interface.
       - You will see that you are logged into your user account (e.g., `housingdown`).
       - The prompt will appear in this format:
     username@servername:~ 
     Example:
     housingdown@ubuntuvm:~
       - The `~` symbol represents your current directory, which is the user’s **home directory**.
    **Confirming Your Current Directory**
    To verify your current location in the file system, type:
    `pwd`
    This stands for print working directory and will display the full path of your current location.
    **Logging Out**
    To log out of the server, type:
    `exit`
 
9. **Network Troubleshooting and Internet Connectivity Fix**
    If you cannot access the internet on your Ubuntu Server VM, the first step is to troubleshoot the network configuration.

    **a. Check Internet Connectivity**
    Start by testing basic connectivity using the `ping` command:
    `ping 8.8.8.8`
    If you receive a message like "no destination reachable", it indicates a network configuration issue.

    **b. Check IP Address Configuration**
    Verify your current IP address and network settings:
    `ip addr`
    You may suspect that the IP address or default gateway is incorrectly configured.

    **c. Check VirtualBox Network Adapter Settings**
    Open VirtualBox and review the network adapter configuration. There are two options namely NAT or bridge mode.

    **NAT Mode**
    Use NAT when:
       - You only need internet access inside the VM
       - You are learning Linux
       - You are building isolated labs
       - You do not need other devices on your home network to access the VM

    **Bridged Mode**
    Use Bridged Adapter when:
      - You want the VM to behave like a separate device on your network
    Examples:
      - SSH into the VM from another computer
      - Host a web server accessible on your LAN
      - Active Directory lab environments
      - Multiple VMs communicating directly on the same network 
    For this lab, we will use Bridged Mode.

    **d. Manually Configure Network Settings (Netplan)**
    We will manually configure the IP address and gateway using Netplan.
    Open the configuration file by typing in the terminal
    `sudo nano /etc/netplan/00-installer-config.yaml`
    This file is generated by Subiquity, the Ubuntu Server installer. It can be safely edited manually.

    **e. Edit Netplan Configuration**
    Inside the file:
      - Navigate using the arrow keys
      - Locate the addresses section and update the IP address
      - Ensure the IP address matches your home network range
    
    **Finding Your Network Details (Windows)**
    On your WIndows machine, open command prompt(run as administrator):
    `ipconfig`
    Look for:
      - IP Address
      - Default Gateway

    **Important Rules**
      - Do not use the same IP as your default gateway
      - Choose an IP address that is likely not in use
      - Example format:
        `192.168.150.10/24` 

    **f. Configure Default Gateway**
      - Scroll to the routes section
      - Under via, set the default gateway to match your Windows gateway

    **g. Save and Exit Nano**
    To save changes:
      - Press:
        `CTRL + O` then `Enter` 
      - Exit:
        `CTRL + X`

    **h. Apply Network Changes**
    To apply changes type in the terminal
    `sudo netplan apply`

    **i. Verify Configuration**
    Check the updated network settings by typing in the terminal:
    `ip addr` or `ip route`

    **j. Test Internet Connectivity**
    Finally, test your connection again:
    `ping 8.8.8.8`
    If configured correctly, you should now receive successful replies.
    
    ![Add Domain to Email](images/add%20domain%20to%20your%20email%20setup.png)

10. **Updating the Server and Enabling Automatic Updates**  
    It is important to keep your Ubuntu Server up to date to ensure security and stability.

    **What is APT?**
    APT (Advanced Package Tool) is used to manage software installation, upgrades, and removals on Ubuntu systems.

    **a. Update Packgae Lists**
    First, update the list of available packages, to do so type in the terminal:
    `sudo apt update`
    Since this is an administrative command, you will be prompted to enter your password.

    **b. Upgrade Installed Packages**
    Next, upgrade all installed packages, to do so type in the terminal:
    `sudo apt upgrade`
    When prompted, type:
    `y`
    Then press **Enter** to continue.

    **c. Reboot the Server**
    After updates are complete, it is recommended to restart the server. To do so type in the terminal:
    `sudo reboot`

    **d. Install and Verify Automatic Updates**
    Ubuntu Server typically includes unattended upgrades by default, but you can verify it:
    `sudo apt install unattended-upgrades`
    If already installed, you will see a message indicating it is the newest version.

    **e. Install Update Notification Tools**
    To allow automatic reboot functionality and better update handling, install:
    `sudo apt install update-notifier-common`
    This is also usually pre-installed.

    **f. Configure Automatic Updates**
    Navigate to the configuration directory:
    `cd /etc/apt/apt.conf.d`
    List files in the directory:
    `ls`
    You will focus on two key files:
      - 50unattended-upgrades
      - 20auto-upgrades 

    **g. Configure Unattended Upgrades**
    Open the first configuration file:
    `sudo nano 50unattended-upgrades`

    **Key Changes:**
      - Ensure allowed origins for security updates are not commented out (// must be removed if present).
      - This enables automatic installation of security updates.

    **h. Enable Automatic Reboots**
    To find the reboot setting:
      - Press `CTRL` + `W`
      - Search for: **automatic-reboot**
    
    **Update the following:**
      - Change: **Automatic-Reboot "false"**
      - To: **Automatic-Reboot "true"**
    This allows the server to reboot automatically after updates.

    Also set the reboot time:
      - Uncomment the reboot time line
      - Set a suitable time for automatic restarts

    To save changes:
      - Press `CTRL` + `X`
      - Then press `Y`
      - Press **Enter**  
 
    **i. Configure Auto-Upgrade Settings**
    Open the second file:
    `sudo nano 20auto-upgrades`

    **Purpose:**
      - Enables automatic package list updates
      - Enables unattended upgrades  

    **Ensure both values are set to 1:**
      - APT::Periodic::Update-Package-Lists "1";
      - APT::Periodic::Unattended-Upgrade "1";
    Save and exit:
    `CTRL` + `X`, then `Y`, then **Enter**

    **j. Restart the Server**
    Apply all changes by rebooting:
    `sudo reboot`

    **k. Verify Unattended Upgrades Service**
    Check that the service is running correctly:
    `sudo systemctl status unattended-upgrades`
    Enter your password if prompted.
    ![Add DNS Records](images/add%20dns%20records%20in%20365.png)

11. **Network Connections**
    To view and verify network connections on the server, use the following command:
    `ip a`

    **Understanding Network Interfaces**
      - This server has one network adapter.
      - Network interface naming conventions:
        - en* → Wired Ethernet adapters
        - wl* → Wireless adapters

    In this VirtualBox environment, the system simulates a wired network connection.

    **MAC Address Information**
    If you need to locate the MAC address of the network adapter, look for:
    **link/ether**
    This value represents the hardware (MAC) address of the network interface.

    **Network Configuration File**
    Network settings are managed using Netplan.
    The configuration file is located at:
    **/etc/netplan/00-installer-config.yaml**
    This file contains the system’s network configuration, including IP addresses, gateways, and DNS settings.

12. **SSH (Secure Shell) Setup and Remote Access**
    SSH allows you to securely access and manage your Ubuntu Server remotely from another machine.

    **a. Install OpenSSH Server (on Ubuntu Server)**
    If SSH was not installed during setup, install it using:
    `sudo apt install openssh-server`
    This enables the server to accept remote SSH connections.

    **b. Install OpenSSh Client (on Windows)**
    If you are using a Windows machine to connect to the server, ensure the OpenSSH Client is installed.
    **Steps:**
      - Open Settings
      - Go to Apps
      - Search for Optional Features
      - Click View Features
      - Look for OpenSSH Client
    If you do not see it:
      - Go to Optional Features
      - Click Add a feature
      - Search for OpenSSH Client
      - Install it

    **c. Open Command Prompt as Administrator**
    Once the SSH client is installed:
      - Press the Windows key
      - Search for cmd
      - Right-click and select Run as Administrator

    **d. Connect to the Server via SSH**
    Use the following command:
    **ssh username@server-ip-address**
    replace the username with your username and replace the server-ip-address with your servers IP

    **e. First-Time Connection Prompt**
    When connecting for the first time, you will see a fingerprint verification message
      - Type: **yes**
      - Press **Enter**
      - Then enter your password

    **f. Successfu Login**
    If successful, you will be logged into your Ubuntu Server remotely. You can now manage the server directly from your laptop or desktop.

    **g. Headless Server Setup** 
    At this point, if your server is fully configured for remote access, you can disconnect:
      - Monitor
      - Keyboard
      - Mouse
    This is known as running a headless server

    **Logging Out of SSH**
    To end your remote session, simply type:
    `exit`

    **Final Note**
    A fresh Ubuntu Server installation provides a minimal but stable foundation. From here, you can build and customize it based on your specific needs.

13. **Desktop + Server (Installing a GUI)**
    If you want a graphical user interface (GUI) on your Ubuntu Server, you can install a lightweight desktop environment.

    **Important Note**
    Ubuntu Server is designed to be lightweight and efficient. Adding a desktop environment will:
      - Increase resource usage (CPU, RAM, storage)
      - Reduce performance on low-spec hardware
    Before proceeding, ensure your system has sufficient resources.

    **a. Install a Lightweight Desktop Environment (LXDE)**
    We will install **LXDE**, which is a minimal and lightweight desktop environment.
    Run the following command:  
    `sudo apt install lxde-core lxappearance`
    When prompted, type:
    `y`
    and press **Enter** to continue.

    **b. What is Being Installed**
      - lxde-core → Provides a minimal desktop environment
      - lxappearance → Allows customization of the desktop appearance (themes, icons, etc.)

    **c. Select Display Manager**
    During installation, you will be prompted to choose a display manager.
    You will see options such as:
      - gdm3
      - lightdm
    **Recommended Choice:**
      - Use the Arrow Keys to select:
        **lightdm**
      - Press **Enter** to confirm 

    **d. After Installation**
    Once installation is complete, the system will boot into a graphical login screen using the selected display manager. You now have a functional GUI on top of your Ubuntu Server.

14. **Remote Login to Server Desktop (Local Network)**
    If you want to access your Ubuntu Server desktop remotely over your local network, you can use **RDP (Remote Desktop Protocol)** with **xRDP**.

    **a. Install xRDP**
    First, install the required package:
    `sudo apt install xrdp`
    When prompted, type:
    `y`
    and press **Enter** to continue.

    **b. Edit xRDP Configuration File**
    Next, modify the xRDP startup configuration:
    `sudo nano /etc/xrdp/startwm.sh`

    **c. Modify the File**
    Inside the file:
       - Navigate quickly to the end of the file:
         - Press Ctrl + End (on some keyboards this may be F12)
       - Locate the following lines and comment them out by adding # at the beginning:
         - test
         - exec

    **d. Add LXDE Session Start Command**
    At the bottom of the file, add a new line:
    `lxsession -s LXDE -e LXDE`
    This ensures xRDP connects to the LXDE desktop environment.

    **e. Save and Exit**
    To save changes:
       - Press `Ctrl` + `X`
       - Type `y`
       - Press **Enter**

    **f. Add xRDP User to SSL Group**
    Run the following command:
    `sudo adduser xrdp ssl-cert`
    This is required because RDP uses encrypted SSL connections.

    **g. Reboot the Server**
    Apply all changes:
    `sudo reboot`

    **h. Connect from Windows**
    On your Windows machine:
       - Search for Remote Desktop Connection
       - Open the application
       - Enter your server IP address
       - Click Connect
       - Accept the security prompt
    
    **i. Login to Ubuntu Server**
       - Enter your Ubuntu username
       - Enter your password
       - Click OK
    You should now be connected to your Ubuntu Server desktop remotely.

    **j. Ending or Leaving the Session
    You can:
    Option 1: Log out completely
       - Use the Ubuntu start menu
       - Select Logout
    Option 2: Disconnect without closing session
       - Close the Remote Desktop window (X button)
       - Click OK when prompted
    This allows background tasks to continue running, and you can reconnect later.

15. Cockpit Web Console (server Management via Browser)
    **Cockpit** is a lightweight web-based interface that allows you to manage your Ubuntu Server from any device on your local network using only a web browser.

    **a. Update Package List**
    Before installing Cockpit, ensure your package manager is up to date:
    `sudo apt update`

    **b. Install Cockpit**
    Install the Cockpit web console:
    `sudo apt install cockpit`
    When prompted, type:
    `y`
    and press **Enter**.

    **c. Check Cockpit Service Status**
    Verify that Cockpit is running:
    `sudo systemctl status cockpit.socket`
    You should see the status as:
    - active (listening)

    **d. Fix Netplan Configuration (Required Step)**
    Cockpit may require a network backend change due to Ubuntu’s updated network manager.
    Open the Netplan configuration file:
    `sudo nano /etc/netplan/00-installer-config.yaml`

    **e. Modify Netplan Renderer**
    Locate the line:
    version: 2
    Directly underneath it, add:
    renderer: NetworkManager

    **Important:**
      - Ensure proper indentation (same level as surrounding lines)

    **f. Save and Apply Changes**
    Save and exit Nano:
      - Press `Ctrl` + `X`
      - Press `Y`
      - Press `Enter`

    Apply the configuration:
    `sudo netplan try`
    When prompted:
    Press **Enter** to accept the new configuration

    **g. Access Cockpit Web Interface**
    From any computer on the same network, open a browser and go to:
    `https://server:9090/` or `https://your-server-ip:9090/`

    **h. Browser Security Warning**
    Because Cockpit uses a self-signed certificate, your browser may show a warning.
       - Click Advanced
       - Click Proceed

    **i. Login to Cockpit**
    Use your Ubuntu Server username and password to log in.
    Then click:
       - Turn on administrative access

    **j. What You Can Do in Cockpit**
    Once logged in, you can manage your server through a web interface, including:
       - View system logs
       - Monitor network activity
       - Manage storage
       - Add or manage user accounts
       - Start and stop services
       - Install updates
       - Use an integrated terminal

    **Summary**
    Cockpit provides a simple, browser-based way to manage your Ubuntu Server without needing SSH or a desktop environment.

16. **Add a New User Account**
    You can create additional user accounts on the server using the `adduser` command.

    **a. Create a New User**
    Run the following command, replacing `new-username` with your desired username:
    `sudo adduser new-username`
    Replace the username with new username

    **b. Setup Up User Details**
    During the setup process, you will be prompted to enter:
       - A password for the new user
       - Confirmation of the password
       - Full name of the user account
       - Optional details such as:
          - Room number
          - Work phone
          - Home phone
          - Other information
    When finished, type:
    `y`
    to confirm the details.

    **c. Verify the User Account**
    Navigate to the home directory:
    `cd /home`
    List all user directories:
    `ls`
    You should see the newly created user account listed.

    **d. User Privileges**
    By default, the new account is a standard user.
    This means:
      - It can log in and use the system
      - It cannot perform administrative tasks unless explicitly granted sudo privileges

16. **Adding Administrative Privileges**
    If you need to grant a user administrative (sudo) privileges, you can add the user to the `sudo` group.

    **What is `sudo`?**
    `sudo` stands for **SuperUser Do**. It allows a standard user to execute commands with administrative privileges.

    **a. Add user to the sudo group**
    Use the following command, replacing `account-username` with the actual username:
    `sudo usermod -a -G sudo account-username`

    **b. What This Does**
       - usermod → modifies a user account
       - -a → appends the user to a group (without removing other groups)
       - -G sudo → adds the user to the sudo administrative group

    **c. Result**
    After running this command:
       - The user will be able to run administrative commands using sudo
       - The account effectively gains admin-level privileges on the system

17. **Switching User Accounts (su command)**
    Linux allows you to switch between user accounts using the `su` command.

    **a. Run Administrative Commands**
    If a user has sudo privileges, they can run administrative commands like:
    `sudo apt update`
    The system will execute the command using elevated permissions.

    **b. Switch to Another User Acccount**
    To switch to another user account, use:
    `su - username`
    replace username with your username e.g. `su - housingdown`
    You will be prompted to enter the password for that user.

    **c. Confirm Current User**
    After switching users, you can confirm your current session by running:
    `whoami`
    This will display the active username.

    **d. Switch Back to Previous User**
    To return to your original user session, type:
    `exit`

    **e. Switching to the Root User**
    Another use of the `su` command is to switch to the root user.
    In Linux, root is the superuser account with full administrative control over the system.
    Switch to root: `sudo su -`
    The - (dash) logs you into the root user's home directory

    **f. Root User Behaviour**
    After switching to root:
      - The prompt changes to root@yourserver
      - The $ symbol changes to #
      - You no longer need to use sudo
    Instead of:
    `sudo apt update`
    You can simply run:
    `apt update`

    **Important Warning**
    Be very careful when operating as root:
       - Root has full control over the system
       - Mistakes can affect or damage the entire system

    **h. Exit Root Session**
    To return to your normal user account:
    `exit`

18. **Listing User Accounts on the Server**
    To display all user accounts on the server, run:
    `compgen -u`
    This command lists:
       - System accounts created by Ubuntu
       - User accounts you have manually created

19. **Remove a user**
    To remove a user account, use the deluser command.
    e.g. `sudo deluser nbassey`
    You will be prompted to enter your password.

    **Confirm User Removal**
    To verify that the account has been removed, run:
    `compgen -u`
    The deleted account should no longer appear in the list.

    **Root Account Access**
    For security reasons, Ubuntu Server disables direct root login by default.
    While this is recommended for most environments, there may be situations where you need to activate the root account temporarily.

    **Enable the Root Account**
    To enable root login, set a password for the root account:
    `sudo passwd root`
    You will be prompted to:
       - Enter a new root password
       - Confirm the password
    Once completed, you can log out and log in directly as root.

    **Disable Root Login Again**
    If you later want to lock and disable the root account again, run:
    `sudo passwd -l root`
    You may be prompted to enter the root password.

    **Security Recommendation**
    Direct root login should generally remain disabled unless absolutely necessary. Using `sudo` with a standard administrative account is considered safer and more secure.

20. **Hostname Management**
    While it is best to choose the correct server name during installation, Ubuntu allows you to change the hostname later if needed.

    **a. View the Current Hostname**
    To display the current server name, run:
    `hostname`
    For more detailed system and hostname information:
    `hostnamectl`

    **b. Change the Hostname**
    To rename the server, use:
    `sudo hostnamectl set-hostname new-name`
    e.g. `sudo hostnamectl set-hostname Christian`
    You will be prompted to enter your password.

    **c. Verify the New Hostname**
    `hostname`
    You should now see the updated server name.

    **d. Refresh the Command Prompt**
    You may notice that the terminal prompt still shows the old hostname.To refresh the shell session, run:
    `exec bash`
    The new hostname should now appear in the command prompt.

    **e. Update the Hosts File**
    When the server boots, local hostnames are mapped to IP addresses using the /etc/hosts file.
    View the file with:
    `cat /etc/hosts`
    You may notice that the old hostname is still listed.

    **f. Edit the Hosts File**
    Open the file for editing:
    `sudo nano /etc/hosts`

    **Steps**
       - Use the arrow keys to locate the old hostname
       - Replace it with the new hostname

    Save the changes:
       - Press Ctrl + X
       - Press Y
       - Press Enter

    **Test the Hostname**
    To confirm the server recognizes its new hostname, run
    ping Christian
    If configured correctly, you should receive successful replies.

21. **Tasksel and LAMP Stack Installation**
    `Tasksel` is a useful Ubuntu utility that simplifies the installation of common server packages and services.

    **a. Update the Package Manager**
    Before installing new software, update the package list:
    `sudo apt update`

    **b. Install Tasksel**
    Install Tasksel using:
    `sudo apt install tasksel`
    When prompted, type: `y` and press `Enter`.

    **c. Launch Tasksel**
    Run Tasksel with:
    `sudo tasksel`
    You will see a list of installable server packages and environments.

    **d. Installing the LAMP Stack**
    For this lab, the goal was to install a LAMP Server.
    However, if Tasksel does not display the expected options, you can manually install the LAMP stack.
    View Available Tasksel Tasks
    `sudo tasksel --list-tasks`

    **e. Manual LAMP Installation**
    Install the LAMP stack manually:
    `sudo apt install apache2 mysql-server php libapache2-mod-php -y`

    **f. What is LAMP?**
    LAMP is a collection of open-source software commonly used for hosting web applications.
    LAMP stands for:
      - Linux → Operating System 
      - Apache – the web server
      - MySQL – the database server
      - PHP – the scripting language
    The Linux portion has already been configured earlier in the lab.

    **g. Securing MySQL**
    MySQL is used to manage databases for web applications.
    After installation, it is recommended to secure the database server by running:
    `sudo mysql_secure_installation`
    During setup:
    Enable password validation by typing: `y`
    Select password policy level: `2`
    This enforces strong password requirements.
    Additional recommended security options:
    Remove anonymous users: `y`
    Disable remote root login: `y`
    Remove the test database: `y`
    Reload privilege tables so changes take effect: `y`

    **h. Testing Apache Web Server**
    Apache is the web server component of the LAMP stack.
    To verify Apache is working:
    Open a web browser on another device such as a Windows laptop.
    Enter the IP address of the Ubuntu server. e.g. `http://192.168.1.10`
    If Apache is functioning correctly, the default Apache web page will appear.

    **i. Creating a PHP Test Page**
    PHP is a scripting language widely used in web development.
    To create a PHP information page, first move to Apache’s default web directory:
    `cd /var/www/html`
    List the contents of the directory: `ls`
    You should see the default file: `index.html`
    Create a new PHP file using the Nano text editor:
    `sudo nano phpinfo.php`
    Add the following code:
    `<?php`
    // show php information
    `phpinfo();`
    `?>`
    To save and exit Nano:
       - Press CTRL + X
       - Type Y
       - Press Enter

    **j. Viewing PHP Information**
    From a web browser on another device, enter:
    `http://server-ip/phpinfo.php`
    e.g. `http://192.168.1.10/phpinfo.php`
    This page displays detailed information about the PHP installation and server configuration.

    **k. Removing the PHP Information File**
    Leaving the PHP information page publicly accessible can create a security risk because it exposes server configuration details that could assist attackers.
    Delete the file with:
    `sudo rm phpinfo.php`
    Refresh the browser page afterward. You should now see a “Not Found” message, confirming the file has been removed.
    At this stage, the Ubuntu server has been configured with a working LAMP stack consisting of:
     - Linux
     - Apache
     - MySQL
     - PHP
    This setup provides a foundation for hosting dynamic web applications and services.
    To make full use of the LAMP environment, additional software can be installed depending on the intended use case. Many popular open-source projects rely on the LAMP stack, including:
     - Nextcloud
     - WordPress

22. **Disk Usage and Addtional Storage Setup**
    Adding an Additional Drive in VirtualBox. To add a second virtual drive to your Ubuntu Server:
     - Open VirtualBox.
     - Select your Ubuntu Server virtual machine.
     - Click Settings.
     - Open the Storage section.
     - Select the hard drive icon with the + symbol.
     - Choose Create.
     - Select VDI (Virtual Disk Image).
     - Click Next.
     - Enter the desired size for the new drive.
     - Finish the wizard and attach the new drive.
    You should now see two VDI drives attached to the virtual machine.

    **a. Viewing Connected Drives**
    Back in Ubuntu Server, I recommend using SSH to make copying commands easier.
    List all connected drives with: `lsblk`
    Typically:
     - sda = primary operating system drive
     - sdb = secondary storage drive
    The plan is to use:
     - Primary drive for the operating system
     - Secondary drive for storage

    **b. Preparing the Secondary Drive**
    Before using the drive, remove any existing filesystem signatures:
    `sudo wipefs -a /drive/path`
    e.g. `sudo wipefs -a /dev/sdb`
    Enter your password when prompted.

    **c. Creating a GPT Partition Table**
    Because this drive will store large amounts of data, GPT (GUID Partition Table) is recommended instead of MBR.
    Use gdisk to create the partition table:
    `sudo gdisk /drive/path`
    e.g.`sudo gdisk /dev/sdb`
    Inside `gdisk`:
     - Press `n` to create a new partition.
     - Enter `1` for the partition number.
     - Press **Enter** to accept the default starting sector.
     - Press **Enter** again to use the full drive size.
     - Press **Enter** to accept the default partition type.
     - Press `w` to write the changes.
     - Type `y` to confirm
    
    **d. Verifying the Partition**
    To view the partition table:
    `sudo gdisk -l /drive/path`
    e.g. `sudo gdisk -l /dev/sdb`

    **e. Creating a Filesystem**
    Now create a filesystem on the new partition.
    Linux commonly uses the ext4 filesystem.
    `sudo mkfs.ext4 /dev/sdb1`
    `mkfs` stands for make filesystem.
    The partition is named `sdb1` because only one partition was created.

    **f. Creating a Mount Point**
    Unlike Windows, Linux does not use drive letters. Additional drives must be mounted somewhere within the root filesystem.
    Linux commonly uses the `/mnt` directory for temporary or additional mounts.
    Navigate to /mnt: `cd /mnt`
    Create a mount point directory:
    `sudo mkdir mount-point-name`
    e.g. `sudo mkdir drive2`
    Verify the directory exists: `ls`
    Enter the directory: `cd drive2`

    **f. Why the Drive Is Not Mounted Yet**
    At this stage, files created inside the folder are still stored on the primary drive because the secondary drive has not been mounted yet.
    e.g. `sudo touch test`
    Remove the test file:
    `sudo rm test`
    Return to the /mnt directory:
    `cd ..`
    `cd ..` moves up one directory level to the parent directory.

    **g. Making the Mount Point Immutable**
    To avoid accidentally storing files on the operating system drive if the secondary disk fails to mount, make the mount point immutable.
    `sudo chattr +i mount-point-name`
    e.g. `sudo chattr +i drive2`
    `chattr` means change attributes.
    Test the protection:
    `cd drive2`
    `sudo touch test`
    You should receive an error similar to: Permission denied
    Return to /mnt: `cd ..`

    **h. Finding the Drive UUID**
    Drives can change device names such as /dev/sdb if hardware changes occur. Using a UUID is more reliable.
    Display UUID information: `sudo blkid`
    Copy the UUID for `/dev/sdb1`

    **i. Configuring Automatic Mounting with fstab**
    Edit the filesystem table: `sudo nano /etc/fstab`
    Add a new line at the bottom:
    `UUID="0f048d8a-03c2-4a1a-9683-52c6664d1f49" /mnt/drive2 ext4 defaults 0 2`
    This entry tells Linux to:
       - Identify the drive using its UUID
       - Mount it to /mnt/drive2
       - Use the ext4 filesystem
       - Apply default mount settings

    The final two values represent:
       - 0 = dump setting
       - 2 = filesystem check order (fsck)
    For non-system drives, 0 2 is recommended.
    Save and exit Nano:
    `CTRL` + `X`
    `Y`
    **Enter**

    **j. Testing the Mount Configuration**
    Before rebooting, test the fstab configuration: `sudo mount -a`
    This mounts all filesystems listed in `/etc/fstab`.
    If you receive this message:
    mount: (hint) your fstab has been modified, but systemd still uses the old version
    Reload systemd: `sudo systemctl daemon-reload`
    Then run again: `sudo mount -a`

    **k. Verifying the Mount**
    You can verify the mounted drive using: `df -h` or `df -Th` or `lsblk`
    `df` stands for disk filesystem.
    Options:
       - h = human-readable sizes
       - -T = display filesystem type
    You can also check a specific mount point:
    `df -h /mnt/drive2`

    **l. Testing File Storage**
    Enter the mounted directory: `cd /mnt/drive2`
    Create a test file: `sudo touch test`
    Verify it exists: `ls`

    **m. Understanding Ownership and Permissions**
    Currently, the mounted directory is owned by root, which is why sudo is required.
    View detailed permissions: `ls -l`
    Return to `/mnt`: `cd ..`
    Change ownership of the directory: `sudo chown -R username directory/`
    e.g. `sudo chown -R housingdown drive2/`
    The `-R` option applies changes recursively to all existing files and folders.
    Verify ownership:
    `cd drive2`
    `ls -l`
    You should now see your user account listed as the owner.

    **n. Setting Directory Permissions**
    Linux permissions are displayed using letters such as: `rwxr-x---`
    These permissions are grouped into:
       - Owner
       - Group
       - Others
    To modify permissions recursively: `sudo chmod -R 750 directory/`
    e.g. `sudo chmod -R 750 drive2/`
    Octal Permission Values
    | Number | Permission           |
    | ------ | -------------------- |
    | 7      | Read, Write, Execute |
    | 6      | Read, Write          |
    | 5      | Read, Execute        |
    | 4      | Read                 |
    | 3      | Write, Execute       |
    | 2      | Write                |
    | 1      | Execute              |
    | 0      | No Permissions       |
     750 means:
       - Owner = full access
       - Group = read and execute
       - Others = no access
    Check the updated permissions: `ls -l`
    The leading `d` indicates the entry is a directory.
    You can now remove files without using `sudo`: `rm test`
    Verify removal: `ls`

23. **File Sharing with Samba**
    To make the storage drive accessible over the network, Samba can be used.
    Samba allows Linux systems to share files using SMB/CIFS protocols commonly used by Windows systems.

    **a. Installing Samba**
    First update the package manager: `sudo apt update`
    Install Samba: `sudo apt install samba`

    **b. Creating a Samba User**
    Add an existing Linux user account to Samba: `sudo smbpasswd -a existing-username`
    e.g. `sudo smbpasswd -a housingdown`
    You will be prompted to create a Samba password.
    For simplicity, you may choose to use the same password as the Linux user account.

    **c. Configuring a Samba Share**
    Navigate to the Samba configuration directory: `cd /etc/samba`
    List the files: `ls`
    You should see: `smb.conf`
    Before editing the configuration, create a backup: `sudo cp smb.conf smb.bk`
    Edit the Samba configuration file: `sudo nano smb.conf`
    Add the following section at the bottom of the file:
    **My shared drive**
    [Drive2]
    path = /mnt/drive2
    valid users = housingdown
    read only = no
    Explanation:
      - path = shared directory location
      - valid users = allowed Samba users
      - read only = no = enables write access
    Save the file:
      - `CTRL` + `X`
      - `Y`
      - **Enter**

24. **Access a Network Share on Windows**
    To access the Samba network share from a Windows device:
      - Open File Explorer.
      - In the address bar, enter the server IP address followed by the share name.
    e.g. \\server-ip-address\share-name In my case: \\192.168.0.233\share
    Press **Enter**.

    **a. Logging In**
    When prompted, enter the credentials for the Samba user account created earlier.
    Example:
     - Username: your Samba username
     - Password: your Samba password
    After authentication, the shared folder should open successfully.

    **b. Testing the Network Share**
    To confirm the share is working correctly:
     - Create a new folder
     - Delete an existing file
     - Copy files to and from the share
    In my case:
     - I deleted a test file named burger
     - Created a new folder on the network share
    The changes were successful, confirming that the Samba share was working correctly.

24. **Ubuntu Firewall Setup (UFW)**
    Ubuntu Server includes a built-in firewall called UFW (Uncomplicated Firewall). By default, it is disabled.

    **a. Checking Firewall Status**
    To check whether the firewall is active: `sudo ufw status`
    Enter your password when prompted.
    If the firewall is not enabled, you will see: Status: inactive

    **Important Warning (Remote Access)**
    Before enabling the firewall, be careful if you are connected remotely via SSH.
    By default, enabling UFW will:
      - Block incoming connections
      - Allow outgoing traffic only
    If SSH is not explicitly allowed, you may lock yourself out of the server.
 
    **b. Allowing SSH Access**
    To ensure remote access remains available, allow SSH before enabling the firewall:
    `sudo ufw allow ssh`

    **c. Enabling the Firewall**
    Once SSH access is permitted, enable the firewall: `sudo ufw enable`
    Confirm when prompted.

    **d. Testing SSH Access**
    From a Windows machine, test remote access using: `ssh username@server-ip`
    Even with the firewall enabled, SSH should still work because the rule allows it.

    **e. Blocking SSH Access**
    If you later decide to disable remote SSH access: `sudo ufw deny ssh`

    **f. Verifying SSH is Blocked**
    From Windows (Command Prompt in Administrator mode), try connecting again: `ssh housingdown@192.168.0.233`
    You should see an error similar to:
    ssh: connect to host 192.168.0.233 port 22: Connection timed out

    **g. Allowing Samba Through the Firewall**
    If you are using file sharing (Samba), you must also allow it through the firewall.
    `sudo ufw allow samba`
    After allowing it, Windows File Explorer should be able to access the network share again:
    \\server-ip\share
    You will then be able to browse shared files and authenticate if required.

    **h. Disabling the Firewall (Optional)**
    If you decide not to use UFW: `sudo ufw disable`
    This turns off the firewall completely and removes all active filtering rules.

25. **Network Statistics (netstat)**
    The netstat command is a useful tool for viewing network connections and understanding which services are running on your Ubuntu Server.
    Since a server’s main role is to provide services over a network, netstat is helpful for monitoring active connections and listening ports.

    **a. Installing netstat**
    netstat is not installed by default on Ubuntu Server. Install it using:
    `sudo apt install net-tools`

    **b. Running netstat with Useful Options**
    To get detailed network information, run netstat with administrative privileges:
    `sudo netstat -tulpn`
    Explanation of Common Options
    | Option | Description                                         |
    | ------ | --------------------------------------------------- |
    | `-t`   | Show TCP connections                                |
    | `-u`   | Show UDP connections                                |
    | `-l`   | Show only listening sockets                         |
    | `-p`   | Show process ID and program name                    |
    | `-n`   | Show numerical addresses instead of resolving names |

    **c. Understanding the Output**
    Each line in the output represents a network connection or listening service.
    Key columns include:
     - Protocol: Shows whether the connection uses TCP or UDP.
     - Local Address: The IP address and port the service is listening on.
     - Foreign Address: The remote machine connected to the service (e.g. other computers on the network).
     - State: Indicates whether a service is listening or actively connected.
     - PID/Program Name: Shows which process is using the network port.

    **Imoortant Concepts**
    *Listening Services*
    A “listening” socket means a service is running and waiting for incoming connections (e.g. SSH, Apache, Samba).

    *IP Address Format*
    0.0.0.0:* means:
     - The service is listening on all network interfaces
     - Any IP address can connect on that port
    
    **d. Why This is Useful**
    Using netstat helps you:
     - Identify running services
     - Check if ports are open
     - Troubleshoot network issues
     - Monitor server activity
     - Improve security by spotting unexpected services

26. **Monitoring Server Resources**
    Monitoring system resources is an important part of server management. It helps identify performance issues, overloaded services, and potential security problems.
    There are two commonly used tools for this:
     - top (traditional tool)
     - htop (modern interactive tool)

    **a. Using top**
    The top command provides a real-time view of running processes on the server.
    Run it with: `top`
    What top shows
     - Running processes (also called tasks)
     - CPU and memory usage
     - System load
    Processes consuming the most resources appear at the top of the list.
    Exiting top
    To exit the interface, press: **q**

    **Understanding Processes**
    A process is an instance of a running program.
    Monitoring processes helps you:
    - Identify what is using CPU or RAM
    - Troubleshoot performance issues
    - Investigate unusual or suspicious activity

    **b. Using htop (Recommended)**
    htop is a more advanced and interactive version of top.
    Installing (if needed)
    `sudo apt install htop`
    Running htop: `htop`

    **Features of htop**
    Unlike top, htop is interactive and easier to use.

    **Searching for Processes**
    To search for a process:
    - Press F3
    - Type a keyword (e.g. smb for Samba)
    - Press **Enter**
    This will highlight matching processes.
    Press F3 again to move to the next match.

    **Key Columns in htop**
    - PID → Process ID (unique identifier)
    - USER → The user running the process
    - CPU% → Percentage of CPU usage
    - MEM% → Percentage of RAM usage
    - COMMAND → The command or service being executed
    CPU and memory usage are especially important for spotting resource-heavy processes.

    **Exiting Search Mode**
    Press: **Esc**

    **Killing a Process**
    If a process becomes unresponsive or uses too many resources, it can be stopped.

    *Steps*
    - Select the process in htop
    - Press: **F9**
    - Choose a signal type

    **Common Signals**
    - SIGTERM (default): Politely asks the process to stop
    - SIGKILL (force kill): Immediately terminates the process
    ⚠️ Use caution when killing processes, especially with SIGKILL, as stopping the wrong process may destabilize the server.

26. **Pro Tips for Ubuntu Server**
    These are useful shortcuts and commands that make working in the Linux terminal faster and easier.

    **a. Tab Autocomplete**
    The Tab key can be used to automatically complete commands, file paths, and directory names.
    Instead of typing the full path: `cd /var/www`
    You can start typing and press Tab: `cd /var/w` + **TAB**
    This expands to: `cd /var/www`
    Tab completion helps prevent typing errors and speeds up navigation.

    **b. Using the Manual (man) Pages**
    If you're unsure what a command does, you can view its manual page.
    e.g. `man sudo`
    This displays detailed information about the sudo command, including:
    - Description
    - Options
    - Usage examples
    *Exiting the Manual*
    Press: **q** to quit and return to the terminal.

    **c. Powering Off the Server**
    To safely shut down the server, use: `sudo poweroff`
    This will stop all services and power off the machine.



 




























































     



















    ![Add DNS Records](images/add%20dns%20records%20in%20365.png)

27. **Refresh the page, and you should see the domain status change to 'Healthy'.**  
    ![Health Status](images/health%20status%20green%20check.png)

28. **Verify SPF Setup**: Open [MXToolbox](https://mxtoolbox.com), change the search type to 'SPF Lookup', and enter your domain.  
    ![Verify SPF](images/verify%20spf%20was%20setup%20successfully%20.png)

29. **Proceed to set up DKIM**.  
    ![DKIM Setup](images/click%20on%20security%20for%20DKIM.png)

30. **Create DKIM keys and add CNAME records to your domain registrar.**  
    ![Create DKIM Keys](images/create%20DKIM%20keys.png)

31. **Enable DKIM signing.**  
    ![Enable DKIM](images/successful%20enabled%20sign%20messages.png)

32. **Configure DMARC**: Create a TXT record in your domain registrar and monitor the email system for any issues.  
    ![DMARC Success](images/successful%20email%20received.png)

## Skills Learned

- **Linux Server Administration**: Gained hands-on experience managing an Ubuntu Server, including system configuration, package installation, service management, and general system maintenance.
- **Storage and Disk Management**: Learned how to add, partition, format, and mount additional storage drives, as well as configure automatic mounting using /etc/fstab.
- **File Permissions and Ownership**: Developed understanding of Linux permission structures and practiced using chmod and chown to control access and ownership of files and directories.
- **Networking and File Sharing**: Configured and tested network file sharing using Samba, including setting up shares and accessing them from Windows systems.
- **Firewall Administration and Network Security**: Gained experience configuring and managing the UFW firewall, including allowing and denying services such as SSH and Samba, and understanding how firewall rules impact network access.
- **Ubuntu Server Hardening**: Learned basic server hardening practices, including securing SSH access, controlling exposed services, restricting network ports, and reducing attack surface through firewall configuration and secure service setup.
- **Network Diagnostics and Monitoring**: Gained experience using tools like netstat to inspect open ports and connections, and htop/top to monitor system performance and running processes.
- **Web Server Setup (LAMP Stack)**: Installed and configured a LAMP stack (Linux, Apache, MySQL, PHP), including securing MySQL and testing PHP functionality.
- **Server Troubleshooting and Maintenance**: Practiced identifying and resolving configuration issues such as fstab errors, service access problems, and permission-related errors.
- **Command-Line Efficiency**: Improved productivity using Linux terminal skills such as tab completion, manual pages (man), and system control commands like poweroff.
- **Technical Documentation**: Developed the ability to clearly document step-by-step system configurations and administrative procedures in a structured and professional format.

## Acknowledgments

This project was developed as part of hands-on learning in Ubuntu Server administration, networking, and system security. It builds on established industry practices in system administration, cybersecurity, and IT infrastructure management.

Appreciation is given to the broader open-source community for providing extensive documentation, tools, and resources that made it possible to explore and implement concepts such as server configuration, firewall management, file sharing, and system hardening.

