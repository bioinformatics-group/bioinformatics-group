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


    
    
    
    
