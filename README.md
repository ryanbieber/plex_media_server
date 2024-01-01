# plex_media_server

After starting the docker compose and setting up the data drives to be -755 follow the steps below to make network drive on the plex so you will be able to connect to it.


Creating a share on Linux and then accessing it from Windows is actually a bit easier than the other way around. First, we'll create the shared folder on the Linux system. Then, we'll look at how to access it from a Windows PC.
Step One: Create the Share on Linux

To set up a shared folder on a Linux that Windows to access, start with installing Samba (software that provides access to SMB/CIFS protocols used by Windows). At the terminal, use the following command:

 
sudo apt-get install samba
 

After Samba installs, configure a username and password that will be used to access the share:

 
smbpasswd -a geek
 

Note: In this example, we are using 'geek' since we already have a Linux user with that name, but you can choose any name you'd like.

Create the directory that you'd like to share out to your Windows computer.  We're just going to put a folder on our Desktop.

 
mkdir ~/Desktop/Share
 

Now, use your favorite editor to configure the smb.conf file. We're using Vi here.

 
sudo vi /etc/samba/smb.conf
 

Scroll down to the end of the file and add these lines:

 
[<folder_name>]
 

Obviously, you'll need to replace some of the values with your personal settings.  It should look something like this:

Save the file and close your editor.  Now, you just need to restart the SMB service for the changes to take effect.

 
sudo service smbd restart
 

Your shared folder should now be accessible from a Windows PC.
Step Two: Access the Linux Share from Windows

Now, let's add the Linux share to our Windows Desktop.  Right-click somewhere on your Desktop and select New > Shortcut.

Type in the network location of the shared folder, with this syntax:

 
\\IP-ADDRESS\SHARE-NAME
 

Note: If you need the IP of your Linux computer, just use the ifconfig command at the terminal.

In the shortcut wizard on the Windows PC, click Next, choose a name for the Shortcut, and then click Finish. You should end up with a Shortcut on your Desktop that goes right to the Linux share.