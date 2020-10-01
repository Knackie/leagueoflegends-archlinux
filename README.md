# leagueoflegends-archlinux


this is a repos to help you in the installation of league of legends on your linux, with snap.


<h1 align="center">
  <img src="snap/gui/leagueoflegends.png" alt="Project">
  <br />
  League of Legends
</h1>

<p align="center"><b>This is the snap for leagueoflegends</b>, <i>"leagueoflegends is a MOBA game developed by Riot Games"</i>.</p>


**Note:** For archlinux only, with snapd

## Dependencies 

    sudo pacman -S lib32-gnutls lib32-libldap lib32-libpulse lib32-openal wget wine-lol winetricks

  Or
    
    yay lib32-gnutls lib32-libldap lib32-libpulse lib32-openal wget wine-lol winetricks


## Install Snap


First, you need to install snap : 
` git clone https://aur.archlinux.org/snapd.git
  cd snapd
  makepkg -si ` 
  
  
  Once installed, the systemd unit that manages the main snap communication socket needs to be enabled:
  
 ` sudo systemctl enable --now snapd.socket ` 
 
 To enable classic snap support, enter the following to create a symbolic link between /var/lib/snapd/snap and /snap:
 
 ` sudo ln -s /var/lib/snapd/snap /snap`
 

## Install LeagueOfLegends

    snap install --edge leagueoflegends
    snap refresh --candidate wine-platform-runtime
    snap refresh --candidate wine-platform-5-staging
	  snap refresh --beta wine-platform-runtime

Now, snap install --edge on league don't work, use : 	snap remove leagueoflegends && snap install --devmode --edge leagueoflegends

* You have to use ([script](https://github.com/Knackie/leagueoflegends-archlinux/blob/master/launchhelper.sh)) before login in new launcher.

 ## Known Issues and fixes for them:
 
 ### Game not starting (Unhandled exception and MIDIMAP_drvOpen in lol ver 9.21):
 Issues with the new launcher. You can temporarily disable it this way:
1. Let the game fully install and update.
2. Make sure client is not running.
3. When you have fully updated game then run this command on terminal to block new launcher from executing.
4. After this command launch game as usual. I'm not sure how longer this method will work.
NOTE: Before executing this command make sure launcher has installed new launcher update.
`for f in RiotClientServices.exe RiotClientCrashHandler.exe; do sudo chmod 0 "$HOME/snap/leagueoflegends/common/.wine/drive_c/Riot Games/Riot Client/$f"; sudo chown root:root "$HOME/snap/leagueoflegends/common/.wine/drive_c/Riot Games/Riot Client/$f"; done`

### Game crashing after character select (lol ver 9.20):
Refresh the wine-platform-runtime with:

    snap refresh --candidate wine-platform-runtime
    
Eventually reinstall the game and the game-snap with:

	snap remove leagueoflegends && snap install --devmode --edge leagueoflegends
    
### Game won't install (and will crash instead):
The emulated version of Windows is probably set to Win7 in wine (it will change back to Win7 after reinstallation of the league snap). Change it to Win XP by running:

    leagueoflegends.winecfg


## Source 

For this, i've use this repos : https://github.com/mmtrt/leagueoflegends & this reddit post : https://www.reddit.com/r/leagueoflinux/comments/j07yrg/starting_the_client_script/

I didn't do this repos to take credit, just to have access to all on one page.
