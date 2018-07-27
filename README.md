
omxplayercamviewsvc-raspbian-lite is a raspbian-lite fork(respin) of the git project RPI-Distro/pi-gen, rebuilt from stage2
with omxplayercamview.service installed.


Usage:

Install/Setup/Configure with:

1) Git clone/build or Download latest img from sf here:


    https://sourceforge.net/projects/omxplayercamviewsvc-rpi-lite/files/latest/download

    and write to sd card.
    

2) After install and reboot, login using :
````
  pi
  raspberry
````
  
   
   a) Go ahead and change your password for the pi account. Safer to do this since you should enable openssh server to
        manage remotely.
   
         
            ````passwd pi````   \enter your new pw twice
     
   b) Enable/start ssh server            
      
      ````sudo systemctl enable ssh````    
      
      ````sudo systemctl start ssh````
        
       
   Note:If you dont enable ssh server and you setup your camera as kiosk, you may find it difficult to resetup another camera view unless you disconnect from network/ or reboot, this is due to the nature of a persistent service, with no exit hooks, yet.

3) Required Edit, change line #18 to your camera's ip/port 

   ````$sudo edit /etc/systemd/system/omxplayercamview.service````

      *if you dont know/like vi, replace "edit" with "nano",TIPS: in nano, use "ctrl-o" to save file and 
        use "ctrl-x" when done to exit file.

    Recommended:
     
        *adjust 15 second timeout/after testing increase this to whatever works for you. I use 300 seconds generally after confirmation its working at 15 second intervals. You can set it to 300 from start if you want as well, a 15 second refresh is just the default,low as it may be.
      
      Optional:
      
        *adjust 3 second up as needed @ Restart=on-failure value near end of file


4) Enable service

   ````$sudo systemctl enable omxplayercamview.service````


5) Start service

   ````$sudo systemctl start omxplayercamview.service````


6) Reboot

   ````$sudo reboot````



*If you get the error 
````
"COMXVideo::Decode timeout"
````
Increase your gpu_mem=X var,  try appending "gpu_mem=128" to /boot/config.txt 
or use raspi-config/dialog to change.





*Features:

    Accelerated direct HW rendering/viewing is low on cpu cycles compared to many options.

    Raspbian based so should work on all the pi's.
    
    Good for standalone or private lan use.

*Known Problems

    Though omxplayer is a ffmpeg derivative of good quaility, omxplayer is not near as reliable as ffmpeg proper. 
    Eg. it will crash/timeout more often than ffmpeg/ffplay or vlc/mplayer, but systemd keeps it running in this setup. 
    *But note you will have timeouts using omxplayer no matter how you use it, im my experience. If i were to replace the omxplayer with one of the formentioned programs, this script would run very reliable and likely timeout a lot less. However, it would require a complete rework of this and im not ready to do that at this time. 






***Note: This runs as a service so you will not have keyboard input to the omxplayer/framebuffer. I recommend starting ssh using ssh to test your ip cam. This way you can restart and modify your service config file as needed without having to reboot/stop service and restart.





