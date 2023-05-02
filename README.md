Download Link: https://assignmentchef.com/product/solved-coen177-lab-6-minix-operating-system
<br>
<strong> </strong><strong>Objectives</strong>

<h5>1.     To setup a virtual machine and install Minix as a guest operating system</h5>

<h5>2.     To understand Minix and modify and re-build Minix kernel</h5>

<h5></h5>

<h5><strong>Guidelines</strong></h5>

In the next two labs, you will be working on Minix operating system. Minix (mini-Unix) is a Unix-like operating system based on a microkernel architecture. Andrew S. Tanenbaum have created a number of MINIX versions for educational purposes<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>. These include Minix 1.0 in 1987, Minix 1.5 in 1991, Minix 2.0 in 1997, and Minix 3 in 2005. Minix 3 <a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a> is not specifically educational but rather a highly reliable and self-healing microkernel OS. Minix 3 has been a free and open-source software distributed under the BSD permissive free software license.




In this lab, you will install, run, and rebuild Minix. You will need a virtual machine on top of which Minix will run.




<strong>Getting started with Minix on the ECC Systems</strong>

You’ll need to set up NoMachine to be able to virtually connect to the SCU Linux Server using a GUI interface. To use Minix on the ECC Systems requires a GUI interface and cannot be done via Terminal only. Instructions for how to setup NoMachine are on <a href="https://wiki.helpme.engr.scu.edu/index.php/FreeNX">https://wiki.helpme.engr.scu.edu/index.php/FreeNX</a>. Once you set up NoMachine and are able to access the SCU Linux Server you may proceed to the next step to setup your MINIX.




To install and run Minix on the ECC Systems, the quickest route is to use vmware and a provided system image.




Start by setting up VMware




<strong>$ setup vmware</strong>This command prepares vmware to run. You should only need to run it once, until the next time you log into your machine. To obtain a copy of a Minix system image, you can use “minix-get-image”<strong>$ minix-get-image (can tab complete)</strong>Please note that this will COMPLETELY ERASE any old image (including any changes you may have made which are not saved outside the Minix system). You must do this once, the first time you are setting up vmware. After that, you should only do this if you need a new image, such as if a modification you make causes your VM to break and become unresponsive. Next, you should run vmware.

<strong>$ vmware &amp;</strong>

This may take a little while to boot up, so be patient. Don’t assume that it is not working.Once it boots up, if you don’t see the “minix” option on the left, go to:

<ul>

 <li>Open a Virtual Machine -&gt; “vm images” subfolder -&gt; “minix3” subfolder -&gt; minix3.vmx</li>

</ul>

When you launch the minix system, you will eventually be promoted for a username. The username for the minix system is “root” (with no password, at least until you set one).




To copy files between the Minix system (running in the vmware virtual machine), and your local system, you may use FTP.  Inside of the VM, do the following:




If you have not already, type “<strong>passwd</strong>” to give the system a password. Make sure it’s a password you’ll easily remember (ask yourself, how secure does this particular system need to be? What would it take for someone to access it?) (<strong>Note:</strong> If you wipe your minix image, you will need to do this again.)Type the following command (again within the Minix system): <strong>tcpd ftp /usr/bin/in.ftpd &amp;</strong>

This will launch the FTP daemon in the Minix system, allowing the local system to connect to it through FTP.

Type “<strong>ifconfig</strong>” to find out what the IP address for the VM is.Now get out of the VM (with Ctrl+Alt) and open a terminal on the host machine. In that terminal, type:

<strong>ftp &lt;the IP address you got from ifconfig&gt;</strong>

This will launch FTP.

When FTP launches, it will take a few minutes at most to connect, once it connects you’ll see something like this:

(….<em>yourname…)</em>:

<strong>Type in your username and hit enter</strong>, as a reminder your username is root.

Then you’ll be prompted <strong>to type in the password</strong> that you created when you setup you MINIX, if you didn’t prepare a password go back and reread the start of the instructions.




In case you are unfamiliar with FTP commands:

<em>For Remote Navigation </em>

<strong>ls</strong> – show contents of remote directory<strong>pwd</strong> – show current location in VM<strong>cd</strong> – change directory on the VM

<em>For Local Navigation </em>

<strong>lcd</strong> – show current location on host machine<strong>lcd &lt;directory&gt;</strong> – change location to &lt;directory&gt;

<em>File Transfer </em>

<strong>get &lt;file&gt;</strong> – copy &lt;file&gt; from current location in VM to current location on host.<strong>put &lt;file&gt;</strong> – copy &lt;file&gt; from current location on host to current location in VM.

DO NOT work on files inside of the VM. You should use FTP to transfer files from the VM to the host, work on them there, then transfer them back. This is so that you do not lose all of your progress if you should make a mistake which crashes the VM and corrupts the bootable OS.

The files for which you must search in this lab can be found somewhere beneath the /usr/src directory.

The grep utility can be very helpful for finding which files contain particular strings, and should be very helpful in this lab.




Once you have modified a file and wish to see the effects of your changes, do the following:

Return to the /usr/src directory.

Type <strong>make world</strong>. This will recompile Minix, and may take some time, so be patient.

When that finishes, type <strong>reboot</strong>. This will reboot the VM with your modifications in effect.

If your VM freezes/crashes during/after a reboot and you wish to restart with a fresh image and setup, start with the first instructions above to get a fresh copy (and note that it will overwrite your existing copy).




<h5><strong>Alternative Approach: Installing Minix under virtualbox</strong></h5>

To install Minix on your own system, without using the prebuilt image provided, you can follow the instructions below instead. Virtual box is a popular and freely available option, which is Open Source Software under the terms of the GNU General Public License.

<strong> </strong>

<ol>

 <li>Download virtual box from <a href="https://www.virtualbox.org">https://www.virtualbox.org</a> and install on your computer to support virtualization, decompress, run and configure with RAM and hard drive</li>

</ol>




<ol start="2">

 <li>Download Minix (minix_R3.3.0-588a35b.iso.bz2), decompress, and save as a .iso image file</li>

</ol>




<ol start="3">

 <li>Configure your Virtual Machine to boot from the downloaded (ISO image), login as root (no password required), then run the setup script</li>

</ol>




<ol start="4">

 <li>Reboot from the installed Minix on disk (and not the ISO image) and then should be ready for use.</li>

</ol>




<ol start="5">

 <li>When logged in again, install common packages, by typing at the prompt sign the following commands:#<strong>pkgin update</strong></li>

</ol>

<strong>#pkgin_sets</strong>




You may setup a password for the root user and create other users!




<ol start="6">

 <li>Obtain Sources from the Git repository and clone under usr/src directory, by typing at the prompt sign the following commands:<strong># cd /usr</strong><strong># git clone git://git.minix3.org/minix src</strong></li>

</ol>




Important: <strong>Read </strong><strong><em>src/docs/UPDATING</em></strong><strong> </strong>and follow the details




When you are familiar with Minix, demo to the TA your Minix platform, disk size, memory available, utilities and applications, bootup process, etc. Plan your next steps to begin kernel hack and rebuild of a modified kernel: https://wiki.minix3.org/doku.php?id=developersguide:rebuildingsystem




When you modify OS modules (CPU scheduling, memory management, etc.) make sure you make a clean copy of the kernel source, by typing:

<strong>$cp -r /usr/src /usr/src.clean</strong>




In this case, you can retrieve the clean copy at any time.







<strong>Changing the Kernel</strong>

As an example, try to locate the kernel source file that prints out the messages you see at system bootup. For example, the copyright statements that are printed. Then add your own message, and rebuild the kernel, reboot the system, and see whether your changes took effect. Please explore the source code of Minix and familiarize yourself with the main directories under /usr/src. This is your first step into modifying the Minix kernel! Be prepared for the next lab that will involve more hands-on OS programming.




<strong>Additional Resources:</strong>

<ul>

 <li>Minix Wiki: https://en.wikipedia.org/wiki/MINIX</li>

 <li>Minix user guide: https://wiki.minix3.org/doku.php?id=usersguide:start</li>

 <li>Minix installation guide: https://wiki.minix3.org/doku.php?id=usersguide:doinginstallation</li>

</ul>

<a href="#_ftnref1" name="_ftn1"><sup>[1]</sup></a> https://en.wikipedia.org/wiki/MINIX

<a href="#_ftnref2" name="_ftn2"><sup>[2]</sup></a> http://www.minix3.org