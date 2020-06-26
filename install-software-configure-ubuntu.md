Content of the this guide..  
* [Configure Laptop](#configure-laptop)  
* [Install Software](#install-software)  
* [Installed tool commands](#installed-tool-commands)  

### Configure Laptop
#### Setup wifi drivers
```
1.sudo apt-get install --reinstall git dkms build-essential linux-headers-$(uname -r)
2.inside driver folder (https://gist.github.com/debojyoti/228729498628e898497557db57619a28)
	sudo make clean	
	sudo make all
	sudo make install
	sudo modprobe -a 8821ce
deactivate SecureBoot (need to be done separately)
```
#### Add kernal parameter
```
1.sudo gedit /etc/default/grub
2.GRUB_CMDLINE_LINUX_DEFAULT="quiet splash ivrs_ioapic[32]=00:14.0"
3.sudo update-grub
```
#### Failed to start Load/Save Screen Backlight Brightness of backlight:acpi_video0.
```
Add one of below parameter to GRUB_CMDLINE_LINUX_DEFAULT
acpi_backlight=video
acpi_backlight=vendor
acpi_backlight=native
acpi_backlight=none
```
#### Add multitouch gestures
```
1.First of all check if your current user is part of the input group. You can do that by : sudo gpasswd -a $USER input  
	Then log out and log back in. Now install xdotool and libinput-tools.

2.sudo apt-get install libinput-tools  
3.sudo apt-get install xdotool  
4.sudo apt install ruby  
5.sudo gem install fusuma 
6.cd ~/.config    
7.mkdir fusuma  
8.cd fusuma
9.touch config.yml   
10.gedit config.yml   

Copy and paste the following instructions if you are using GNOME, which is the default environment in 18.04.

	swipe:
	  3: 
	    left: 
	      command: 'xdotool key alt+Right'
	    right: 
	      command: 'xdotool key alt+Left'
	    up: 
	      command: 'xdotool key super'
	    down: 
	      command: 'xdotool key super'
	  4:
	    left: 
	      command: 'xdotool key ctrl+alt+Down'
	    right: 
	      command: 'xdotool key ctrl+alt+Up'
	    up: 
	      command: 'xdotool key ctrl+alt+Down'
	    down: 
	      command: 'xdotool key ctrl+alt+Up'
	pinch:
	  in:
	    command: 'xdotool key ctrl+plus'
	  out:
	     command: 'xdotool key ctrl+minus'

	threshold:
	  swipe: 0.4
	  pinch: 0.4

	interval:
	  swipe: 0.8
	  pinch: 0.1
11.which fusuma --> /usr/local/bin/fusuma
12.gnome-session-properties (Add new startup application) --> command field : /usr/local/bin/fusuma -d
```
### Install Software
#### JAVA Installation
```
1.Copy jdk folder into root location. --> sudo mv ~/Downloads/jdk-8u212-linux-x64/jdk1.8.0_212/ .
2.Update profile. --> sudo gedit /etc/profile
	JAVA_HOME=/jdk1.8.0_212	
	PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
	export JAVA_HOME
	export PATH
3.Reload prfile. --> . /etc/profile
4.Set jdk installation location.
  sudo update-alternatives --install "/usr/bin/java" "java" "/jdk1.8.0_212/bin/java" 1
  sudo update-alternatives --install "/usr/bin/javac" "javac" "/jdk1.8.0_212/bin/javac" 1
  sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/jdk1.8.0_212/bin/javaws" 1
5.Set default java
  sudo update-alternatives --set java /jdk1.8.0_212/bin/java
  sudo update-alternatives --set javac /jdk1.8.0_212/bin/javac
  sudo update-alternatives --set javaws /jdk1.8.0_212/bin/javaws
6.Test java version. --> java -version
```
#### Install java11
```
Open below file and change it as below
sudo nano /etc/environment
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/jvm/jdk-11/bin"
JAVA_HOME="/usr/lib/jvm/jdk-11"

continue step 4 and 5
```
#### Update NPM and NODEJS
```
1. curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
2. close and open terminal
3. nvm install node
```
#### Uninstall nodejs
```
sudo apt-get purge --auto-remove nodejs

sudo rm -rf /usr/local/bin/npm /usr/local/share/man/man1/node* /usr/local/lib/dtrace/node.d ~/.npm ~/.node-gyp /opt/local/bin/node opt/local/include/node /opt/local/lib/node_modules

sudo rm -rf /usr/local/lib/node*
sudo rm -rf /usr/local/include/node*
sudo rm -rf /usr/local/bin/node*  
```

#### Add .desktop file
To create icon for a installed software.
```
file creation location --> /home/niranjan/.local/share/applications
```

### Installed tool commands
1.jpegoptim --> optimize jpeg images, converts, reduce file size without loosing much quality
```
jpegoptim --size=100k cookie.jpeg
```