Installation Instructions
==========================

Note: these binaries are for Jetson 4.6.4, and the corresponding kernel  

E.g.:  

`cat /etc/nv_tegra_release`  
`# R32 (release), REVISION: 7.4, GCID: 33514132, BOARD: t210ref, EABI: aarch64, DATE: Fri Jun  9 04:25:08 UTC 2023`  

`uname -a`  
`Linux ubuntu 4.9.337-tegra #1 SMP PREEMPT Thu Jun 8 21:19:14 PDT 2023 aarch64 aarch64 aarch64 GNU/Linux`  


Step 0:  
---------------------  
Flash the device tree.  

Copy the DTB file to NVidia SDK tree.  
For Jetson Nano targets this should be:  

`nvidia_sdk/JetPack_4.6.4_Linux_JETSON_NANO_TARGETS/Linux_for_Tegra/kernel/dtb/tegra210-p3448-0002-p3449-0000-b00.dtb`  

Step 1:  
---------------------  
Copy the kernel module to the target:  

`scp ./tc358743.ko nvidia@192.168.55.1:/home/nvidia`  

Step 2:  
---------------------  

Load the driver on the target  
 
`sudo insmod ~/tc358743.ko`  

Step 3:  
---------------------  

Check that streaming works with GStreamer:  

`gst-launch-1.0 -vvvvv v4l2src ! "video/x-raw, width=1920, height=1080, framerate=60/1,format=UYVY"  ! nvvidconv ! omxh264enc ! mpegtsmux ! filesink location=test.ts`  
