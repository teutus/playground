# Vagrant Demo Setup

## (Install Git on Windows)

1. Go to https://git-scm.com/download/win.
2. Download 64-bit Git for Windows.
3. Run the .exe file once it finishes downloading.

## Install VirtualBox on Windows
1. Go to https://www.virtualbox.org/wiki/Downloads.
2. Click on Windows Hosts link.
3. Run the .exe file once it finishes downloading.
4. (Optional) Download and install the Extension Pack.

## Enable Windows Subsystem for Linux (WSL)
1. Open a Powershell Console as Administrator
2. Execute:

        Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
3. Reboot

## Install Ubuntu 18.04 LTS from Windows Store
1. Go to https://www.microsoft.com/en-us/p/ubuntu-1804-lts/9n9tngvndl3q#activetab=pivot:overviewtab.
2. Click the Get / Install option.
3. Run Ubuntu 18.04 from the Start menu.
4. Create a username and password when prompted.
5. Close the Ubuntu terminal window.

## (Configure VS Code to use WSL in the Integrated Terminal)
1. Press Ctrl+Shift+P to open the Command Palette.
2. Type: Terminal: Select Default Shell
3. Select: WSL Bash

## Install Python and PIP in WSL
1. (Press Ctrl+` in VS Code to open the Integrated Terminal.); Alternatively press <Windows-Key>-R and type bash <Enter>
2. Type the following in the terminal:

        cd ~
        sudo apt-get update && sudo apt-get -y upgrade
        sudo apt-get -y install python-pip python-dev libffi-dev libssl-dev

3. Add the local bin directory to PATH:

        echo 'export PATH="${PATH}:/home/<USER>/.local/bin"' >> ~/.bashrc

    *Note: Replace \<USER> with your actual username.*

## Install Ansible in WSL
1. Type the following in the terminal:

        pip install ansible
## Test Ansible Installation
1. Create a file ~/test.yml with the following content:

        ---
        - hosts: localhost
          tasks:
          - debug: msg="Ansible is working!"
2. Execute

        ansible-playbook ~/test.yml -connection=local

3. Check the output. It should be similar to this:
 
        stefan@fme-pc752:~$ ansible-playbook ~/test.yml -connection=local
        [WARNING]: Skipping 'ansible_port' as this is not a valid group definition

        [WARNING]: Skipping 'ansible_psrp_cert_validation' as this is not a valid group definition
        [WARNING]: Skipping 'ansible_psrp_transport' as this is not a valid group definition
        [WARNING]: Skipping 'ansible_user' as this is not a valid group definition
        [WARNING]: Skipping 'ansible_connection' as this is not a valid group definition
        [WARNING]: Skipping 'ansible_password' as this is not a valid group definition
        [WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does notmatch 'all'

        PLAY [localhost] ***********************************************************************************************
        TASK [Gathering Facts] *****************************************************************************************
        ok: [localhost]
        TASK [debug] ***************************************************************************************************
        ok: [localhost] => {
            "msg": "Ansible is working!"
        }
        PLAY RECAP *****************************************************************************************************
        localhost                  : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

## Install Vagrant in WSL
1. Go to https://www.vagrantup.com/downloads.html.
2. Right-click and copy the link for the 64-bit Debian package.
3. Type the following in the terminal:

        cd ~
        wget https://releases.hashicorp.com/vagrant/2.2.6/vagrant_2.2.6_x86_64.deb
        dpkg -i vagrant_2.2.6_x86_64.deb
    
    *Note: Replace the link and the .deb package name with the one you actually copied. (At the point in time of writing this (NOV2019) the current Version was 2.2.6.*

## Configure Vagrant in WSL to Use VirtualBox on Windows
1. Type the following in the terminal:

        echo 'export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"' >> ~/.bashrc
        echo 'export PATH="${PATH}:/mnt/c/Program Files/Oracle/VirtualBox"' >> ~/.bashrc
        source ~/.bashrc

## Clone my Demo GitHub Repository
1. Type the following in the terminal:

        cd /mnt/c/Users/stefan/Desktop/
        git clone https://github.com/teutus/playground.git
        cd config-mgmt/vagrant-demo

## Start the VM in VirtualBox using Vagrant
1. Type the following in the terminal:

        vagrant up
        
## Verify VM was Provisioned
1. Go to http://192.168.36.11/ in a browser.
2. Verify that a demo page is displayed.

## Stop and Destroy the VM
1. Type the following in the terminal:

        vagrant halt
        vagrant destroy

## Helpful Links
### MS Windows Subsystem Linux (WSL)
- https://docs.microsoft.com/en-us/windows/wsl/install-win10

### Vagrant
- https://www.vagrantup.com/downloads.html
- https://www.vagrantup.com/docs/other/wsl.html
- https://www.tothenew.com/blog/using-vagrant-to-deploy-aws-ec2-instances/

### Ansible
- https://geekmonkey.de/ansible-unter-windows/
- https://pip.pypa.io/en/stable/installing/
- https://www.digitalocean.com/community/tutorials/configuration-management-101-writing-ansible-playbooks
    - https://github.com/erikaheidi/cfmgmt

### Kubernetes
- https://www.digitalocean.com/community/tutorials/how-to-create-a-kubernetes-cluster-using-kubeadm-on-ubuntu-18-04


## Resources

Stefans sample code on GitHub: https://github.com/teutus/playground/tree/master/config-mgmt/vagrant-demo
