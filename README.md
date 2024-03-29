<h1>PAM Authentication Features</h1>

<h2>Description</h2>
Project consists of installing PAM and using it to apply password policies to any user added in the machine, and to secure SSH login. 
<br />


<h2>Utilities Used</h2>

- <b>VirtualBox</b>
- <b>Debian Environment</b>
- <b>Terminal</b>
- <b>Putty</b>

<h2>Library Installation:</h2>
The libraries required for this project will be installed
<br />
<br />
On the Debian machine, the command apt update is run to update the database:<br/>
<img src="https://imagizer.imageshack.com/img924/5853/l9vfyM.png"
<br />
<br />
The install command is used to install the cracklib-runtime library. This is a library that provides runtime support for password dictionary generators:<br/>
<img src="https://imagizer.imageshack.com/img923/4930/mV87hB.png"
<br />
<br />
The apt install command is used to install the libpam-pwquality library. This library provides the capability to examine password strength:<br/>
<img src="https://imagizer.imageshack.com/img924/4961/gBetsJ.png"
<br />
<br />

<h2>Password Complexity:</h2>
Nano is used to open the pluggable authentication modules file:<br/>
<img src="https://imagizer.imageshack.com/img922/1788/8IH53V.png"
<br />
<br />
The pam_pwquality line is found:<br/>
<img src="https://imagizer.imageshack.com/img924/792/kN0Tgc.png"
<br />
<br />
The following line is added to create the password policy:<br/>
<img src="https://imagizer.imageshack.com/img922/9257/Aprqwm.png"
<br />
<br />
The system is then rebooted:<br/>
<img src="https://imagizer.imageshack.com/img924/3751/VDFpPp.png"
<br />
<br />
The terminal is then logged in under the root user:<br/>
<img src="https://imagizer.imageshack.com/img922/2562/zn0OjG.png"
<br />
<br />
The adduser command is issued to attempt to make a new user. After entering a bad password, the policy should kick in to effect:<br/>
<img src="https://imagizer.imageshack.com/img924/5618/dSP41j.png"
<br />
<br />
The delete user command is issued to clear the user:<br/>
<img src="https://imagizer.imageshack.com/img923/5113/enFfX3.png"
<br />
<br />
A new user is created following the password guidelines. This time, it goes through:<br/>
<img src="https://imagizer.imageshack.com/img922/2539/eb9xUJ.png"
<br />
<br />

<h2>Disable Reuse of the 10 Oldest Passwords:</h2>
The nano command is used to reopen the PAM file:<br/>
<img src="https://imagizer.imageshack.com/img922/8698/EHkkTc.png"
<br />
<br />
The pam_unix.so line is navigated to:<br/>
<img src="https://imagizer.imageshack.com/img922/6461/wYDjEz.png"
<br />
<br />
At the end of the line, remeber=10 is added. This ensures that the last 10 passwords cannot be reused:<br/>
<img src="https://imagizer.imageshack.com/img922/8204/rL2rTc.png"
<br />
<br />
The delete user command is used to delete the jorge user:<br/>
<img src="https://imagizer.imageshack.com/img923/2030/15WObr.png"
<br />
<br />
The add user command is issued with the password ASDFzxcv123:<br/>
<img src="https://imagizer.imageshack.com/img922/3627/gU74Gr.png"
<br />
<br />
The user is then switched to with su -:<br/>
<img src="https://imagizer.imageshack.com/img922/7591/VrtsCB.png"
<br />
<br />
The passwd command is used to change the user's password to POIqwer12:<br/>
<img src="https://imagizer.imageshack.com/img923/1671/nJtiaO.png"
<br />
<br />
The passwd command is issued again to attempt to change the password back. This time, the password does not work. As it was one of the last 10 already used:<br/>
<img src="https://imagizer.imageshack.com/img923/5527/oAxtY3.png"
<br />
<br />
The root user is returned to:<br/>
<img src="https://imagizer.imageshack.com/img923/3124/YA5vyK.png"
<br />
<br />
The cat /etc/security/opasswd command displays the hash value of the old password:<br/>
<img src="https://imagizer.imageshack.com/img924/8298/DJZxsP.png"
<br />
<br />

<h2>Restrict PAM SSH Authentication:</h2>
The apt install ssh command is used to install the ssh service on the Debian machine:<br/>
<img src="https://imagizer.imageshack.com/img923/4536/NrRFRD.png"
<br />
<br />
The echo command is issued to create a file of allow SSH users and add my user to it:<br/>
<img src="https://imagizer.imageshack.com/img923/8799/QlXQGq.png"
<br />
<br />
The nano command is used to open the SSH PAM configuration file:<br/>
<img src="https://imagizer.imageshack.com/img923/6139/IKOaJ1.png"
<br />
<br />
The following line is written under the @include line. This states that an authentication process is required to allow connection for a user located in the file /etc/ssh/sshd/allow. If an error occurs, the connection will fail:<br/>
<img src="https://imagizer.imageshack.com/img924/2265/JEwyfQ.png"
<br />
<br />
The service ssh start command is run:<br/>
<img src="https://imagizer.imageshack.com/img923/8374/7AyiVr.png"
<br />
<br />
IP a i sused to check the VM's IP address:<br/>
<img src="https://imagizer.imageshack.com/img923/5250/QB1goR.png"
<br />
<br />
The windows 10 vm is run and it is ensured that the machine's are connected via a bridged adapter:<br/>
<img src="https://imagizer.imageshack.com/img923/426/jBUkrE.png"
<br />
<br />
Putty is used on the Windows machine to attempt an SSH connection on port 4567:<br/>
<img src="https://imagizer.imageshack.com/img924/6374/UsyIBw.png"
<br />
<br />
Attempting to connect with a user not listed in the sshd.allow file will deny access:<br/>
<img src="https://imagizer.imageshack.com/img924/9756/ZQTlim.png"
<br />
<br />
A connection is granted if the user is listed in the sshd.allow file:<br/>
<img src="https://imagizer.imageshack.com/img923/1117/miLALf.png"
<br />
<br />

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
