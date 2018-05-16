### Make the screenly work on a Raspberry Pi which is more secure to the outside world.

As a guidence for this https://blog.alexellis.io/hardened-raspberry-pi-nas/ is used.

#### First build the image like it is described in screenly-ose/docs/create-disk-image.md.
Boot your raspberry pi from this image.

Login with the standard credentials: user: pi and password: raspberry

#### Add a new user to the system and delete the built-in pi-user:
```
$ sudo useradd newuser -m -G adm,sudo,gpio
$ sudo passwd newuser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```
Instead of ```newuser``` you can enter here the username of your choice.

The option ```-m``` creates the user's home directory if it does not exist.

The option ```-G``` adds the user to the following groups. Groups are seperated by a comma, with no intervening whitespace.
The ```adm``` group allows access to log files in /var/log and using xconsole.
The ```sudo``` group enables sudo access for the user.
The ```gpio``` group is a Pi-specific group for GPIO pin access, I need it for motion detection. If you don't use motion detection then you won't need it.

The command
```
sudo passwd newuser
```
makes you set a new password for the newly created user. Also here you have to replace newuser with the username you used for the useradd command.

#### Now log out and log back in as the new user.
```
logout
```

#### Remove the pi user:
```
$ sudo userdel pi
$ sudo rm -rf /home/pi
```

### Change the hostname
```
sudo raspi-config
```
goto
```
2 Network Options   Configure network settings
```
then
```
N1 Hostname         Set the visible name for this Pi on the network
```
```
<Ok>
```
Enter the hostname you want to use for this device for example: ```screenlypi```
```
<Ok>
```
##### If you haven't configured your wifi yet it's a good time to do it now

goto
```
2 Network Options   Configure network settings
```
then
```
N2 Wi-fi            Enter SSID and passphrase
```
Select your country, mine is ```NL Netherlands```
```
<Ok>
```
```
<Ok>
```
Enter the SSID of your Wi-fi:
```
myhomewifi
```
```
<Ok>
```
Enter the passphrase:
```
mysecretpassword
```
```
<Ok>
```
```
<Finish>
```
```<Yes>``` to reboot the Raspberry Pi.
