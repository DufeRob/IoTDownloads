# IoTDownloads
Downloads for the IoT Learning  Initiative Book, big downloads that can't be uploaded there

Yocto-EDison Headers:
-----------------------------------------------------------
Taken from:
https://communities.intel.com/thread/62873?start=0&tstart=0

Here the correct procedure to compile drivers to be used with 3.10.17-poky-edison+ (same procedure can be used for different/future versions of Poky).<br>
<b>1.</b> Download Poky Headers<br>
<b>2.</b> Copy it on Edison where you prefer (following procedure assume you are using your home: /home/root aka ~/)<br>
<b>3.</b> Extract the DEB file with ar command:<br><b>ar x linux-headers-3.10.17-poky-edison_3.10.17-poky-edison-1_i386.deb</b><br>
<b>4.</b> deflate data.tar.gz with tar command:
<br><b>tar x -f data.tar.gz<br></b>
<b>5.</b> 2 new directory are created: <br><b>~/usr and ~/lib.<br></b>
<b>6.</b> You need to solve the '+' issue (the kernel is "3.10.17-poky-edison+" while the Poky Header is "3.10.17-poky-edison")
edit the header file: <br><b>~/usr/src/linux-headers-3.10.17-poky-edison/include/generated/utsrelease.h</b>
change the line:<br><b> #define UTS_RELEASE "3.10.17-poky-Edison" with #define UTS_RELEASE "3.10.17-poky-Edison+"</b><br>
<b>7.</b> now you need to link you kernel directory with the "build" directory where the make command can find the Poky headers (make look for '/lib/modules/3.10.17-poky-Edison+/build'):
<br><b>cd /lib/modules/3.10.17-poky-edison+</b><br>Oance there create a sym link like this:
<br><b>ln -s /home/root/usr/src/linux-headers-3.10.17-poky-edison build</b> (<-- this create the link '/lib/modules/3.10.17-poky-Edison+/build' that point to the Linux-headres directory)<br>
<b>8.</b> Compile your driver: simply copy the driver files into a folder in Edison, cd to the folder and run make<br>
<b>9.</b> The compiler should output a <filename>.ko that is the compiled driver with the magic signature '3.10.17-poky-edison+' so you will be able to load it!<br>
<b>10.</b> load the driver: insmod <filename>.ko<br>
