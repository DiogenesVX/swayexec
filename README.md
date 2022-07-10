# swayexec
A small utility to run GUI applications as root (e.g. Gparted, Etherape etc.).
This is a small utility which allows you to run GUI applications as root on Sway just like pkexec on Xorg.
The idea was born due to polkit-gnome-authentication-agent-1 crashes on Sway and I had to look for other ways of running GUI applications which require root access. I had a choice to either go with a different polkit agent like lxpolkit (which actually works but only with Xwayland) or I had to create something myself. Whenever there is a choice between using a ready-made solution or creation and, I have got a little of free time, I always go with the process of creation. I created it for myself to use with Sway on Debian. If someone finds it useful for his/her situation, I'd be happy :).
Of course this can run basically on any distro and desktop environment.

# Features
   1. Get a visual authentication prompt when running a GUI application.

# Screenshot
   ![Alt text](https://github.com/DiogenesVX/swayexec/blob/main/swayexec.png)

# Usage for Sway (step-by-step for new users)
   1. Download the archive, extract it, open a terminal, navigate to the extracted folder and run:

          chmod +x swayexec
          chmod +x yadaskpass
          sudo cp swayexec /usr/local/bin
          sudo cp yadaskpass /usr/local/bin

   2. Run the applications as follows (examples):
       
## NOTE: Before you run any application with swayexec, close and re-open the terminal, otherwise the sudo timeout will keep your password active for a few minutes and the applications opened with swayexec will open without any password prompt.
   
          swayexec <your app name>
          swayexec /usr/sbin/gparted
          swayexec gedit /etc/sysctl.conf

   3. The best way would actually be to create a local .desktop launcher for the desired application, for instance this is how you modify the gparted launcher to run with swayexec by default:

          cp /usr/share/applications/gparted.desktop ~/.local/share/applications
          gedit ~/.local/share/applications/gparted.desktop

Find the line that reads: "Exec=/usr/sbin/gparted %f" and just add swayexec like this: "Exec=swayexec /usr/sbin/gparted %f" save and exit. Now whenever you launch Gparted from the menu, it will open with swayexec.
   
   4. Make sure you have the following packages installed:
 
          yad
          sudo
          coreutils
          policykit-1
          libnotify-bin
