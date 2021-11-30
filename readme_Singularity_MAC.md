# Installing Singularity on Mac

I am essentially following along with the [docs](https://sylabs.io/guides/3.0/user-guide/installation.html#install-on-windows-or-mac). 



## 1.Homebrew 
Make sure to have HomeBrew installed (can use `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"` to install).

## 2. Install Packages
Install Vagrant and necessary packages using Brew.
```
brew install virtualbox && \
brew install vagrant && \
brew install vagrant-manager
```

You will almost certainly need to access you preferences to allow "extensions" I had to go into `Security & Privacy` and click on `Details` in the general tab where it was saying some system software requires your attention. I enabled the `Oracle` something or other... I also may have let terminal have Full Disk Write.

If you are working remotely, you may need to access system preferences and allow this plugin to be installed. 

### Remote access by screenshare (using a mac)

1. Create `vim ~/.ssh/config` (create `~/.ssh` folder if necessary) and copy the following:
```
Host ext
    HostName <hostname>
    Port 22
    User <your-username>
    LocalForward 5999 127.0.0.1:5900
```
This will allow you to ssh onto your machine by using `ssh ext` command. If you need to go through a machine via proxy you need to add `ProxyJump` term like so: 
Say you are connecting to machine A going through B

```
Host B_name
    Hostname B_hostname
    User <user on B>
Host A_name
    Hostname A_Hostname
    ProxyJump B_name
    User <user on A>
    LocalForward 5999 127.0.0.1:5900
```

Now you can ssh onto computer A by simply using `ssh A_name`. 

You will be prompted for passwords for each machine you will need to use ssh-keygen to create a public/private SSH key pair (you put the public bit in ~/.ssh/authorized_keys on the remote host), I'll leave it to you to figure that bit out. ;)

2. Open a tunnel to the machine. This will als not forward to the screensharing port thanks to LocalForward.
3. 5999 is the local port which is being forwarded via SSH to the Screen Sharing port (5900) on the remote host. 
To connect you now need to go to Finder and hit <cmd>-k to open the “Connect to Server” dialogue. Enter the following into the address bar
`vnc://localhost:5999`
And click connect.

You should see a screenSharing window open up which will allow you to log into your computer.
4. Open up system preferences and allow virtualbox to be installed!

## 3. Create VM directory
Create a directory to be used with your VM.
`mkdir vm_singularity && cd vm_singularity`

## 4. Deploy VM
### 4.1 Removing a VM
If this folder was used for a previous VM then destroy it using 
```
vagrant destroy && \
    rm Vagrantfile
```

You would not be able to initialize a VM on top of an existing image, so sometimes this is necessary before you can go about initializing your new VM.
    
### 4.2 Initializing the VM
Initialize the VM using sylabs' image with singularity:
`vagrant init sylabs/singularity-ce-3.9-ubuntu-bionic64`

You only need to do this once, then it should be properly set up to run as needed in the future.
    
### 4.3 Starting the VM
To start the VM you need only run:
`vagrant up`

This starts the virtual machine running so you can ssh into it or otherwise interact with it.
    
## 5. Use the VM

### 5.1 Starting up
To ssh in you can use:
`vagrant ssh`
 
You should now see vagrant@vagrant which means you are on your VM! You can `sudo su` as needed, though you probably just want to use singularity directly to run images and probably don't want to mess around too much with any installation there.

### 5.2 Finishing
To finish up you can `exit` out of the vagrant vm. To shut it down you can run `vagrant halt` which will safely stop the VM (it can be restarted again with `vagrant up`)


    
    
    
    
