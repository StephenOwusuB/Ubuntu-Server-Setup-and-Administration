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

In this project, we will set up a Ubuntu Server 26.04 LTS on our local laptop using virtual box. This hands-on lab aims to enhance our understanding of setting up, configuration, deployment, managing and securing an organization's linux server environment by by establishing best practices and implementing baseling security measures. Configuring and managing this lab has significantly contributed to my knowledge of maintaining a Linux-based environment.

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
    <b>The first thing I am going to do is enter a name for the server, under folder select the dropdown and select other, decide where you want to create your ubuntu server folder to store the files, select ISO image and under that option select the ubuntu iso image, next select skip unattended installation and select next,choose the base memory of your choice. i will go with 8192, choose the processor of your choice. i will go with 4, leave enable efi unchecked select next, select the disk size of your choice. i will go with 80gb, select next to finish the virtual box ubuntu server setup.
    </b>
    ![VirtualBox](images/virtualbox.jpg)

4. **If your custom domain is not visible, select 'Add Domain' to integrate it.**  
    ![Add Domain](images/click%20on%20add%20domain.png)

5. **Choose your preferred method for connecting your domain.**  
    ![Add Domain to Email](images/add%20domain%20to%20your%20email%20setup.png)

6. **Copy the three records (MX, TXT, and CNAME) and add them to your domain registrar.**  
    ![Add DNS Records](images/add%20dns%20records%20in%20365.png)

7. **Refresh the page, and you should see the domain status change to 'Healthy'.**  
    ![Health Status](images/health%20status%20green%20check.png)

8.  **Verify SPF Setup**: Open [MXToolbox](https://mxtoolbox.com), change the search type to 'SPF Lookup', and enter your domain.  
    ![Verify SPF](images/verify%20spf%20was%20setup%20successfully%20.png)

9.  **Proceed to set up DKIM**.  
    ![DKIM Setup](images/click%20on%20security%20for%20DKIM.png)

10. **Create DKIM keys and add CNAME records to your domain registrar.**  
    ![Create DKIM Keys](images/create%20DKIM%20keys.png)

11. **Enable DKIM signing.**  
    ![Enable DKIM](images/successful%20enabled%20sign%20messages.png)

12. **Configure DMARC**: Create a TXT record in your domain registrar and monitor the email system for any issues.  
    ![DMARC Success](images/successful%20email%20received.png)

## Skills Learned

- **Email Security Configuration**: Gained hands-on experience in setting up SPF, DKIM, and DMARC to secure an organization's email environment.
- **Domain Management**: Learned how to manage custom domains within Microsoft 365 and navigate domain registrars.
- **Technical Documentation**: Developed the ability to create clear and professional documentation for technical processes and configurations.
- **Problem-Solving**: Enhanced problem-solving skills by troubleshooting and resolving issues related to domain verification and email authentication.
- **Cloud-Based Email Administration**: Improved knowledge of administering and maintaining a cloud-based email environment.

## Acknowledgments

Special thanks to all contributors and the community for their support and guidance. This project was inspired by various resources and projects in the cybersecurity and IT fields.

