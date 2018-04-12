
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


*Features:

    Accelerated direct HW rendering/viewing is low on cpu cycles compared to many options.

    Raspbian based so should work on all the pi's.
    
    Good for standalone or private lan use.








***Note: This runs as a service so you will not have keyboard input to the omxplayer/framebuffer. I recommend starting ssh using ssh to test your ip cam. This way you can restart and modify your service config file as needed without having to reboot/stop service and restart.





