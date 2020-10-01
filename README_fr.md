# leagueoflegends-archlinux


ceci est un référentiel pour vous aider à installer league of legends sur votre Linux, avec des captures d'écran.


<h1 align="center">
  <img src="leagueoflegends.png" alt="LOL">
  <br />
  League of Legends
</h1>

<p align="center"><b>C'est le claquement pour leagueoflegends</b>, <i>"leagueoflegends est un jeu MOBA développé par Riot Games"</i>.</p>




**Remarque:** Pour archlinux uniquement, avec snapd
## Dépendances

    sudo pacman -S lib32-gnutls lib32-libldap lib32-libpulse lib32-openal wget wine-lol winetricks

 Ou
    
    yay lib32-gnutls lib32-libldap lib32-libpulse lib32-openal wget wine-lol winetricks


## Installer Snap


Tout d'abord, vous devez installer snap : 
` git clone https://aur.archlinux.org/snapd.git
  cd snapd
  makepkg -si ` 
  
  
  Une fois installée, l'unité systemd qui gère la prise de communication snap principale doit être activée:
  
 ` sudo systemctl enable --now snapd.socket ` 
 
 
Pour activer la prise en charge de l'accrochage classique, entrez ce qui suit pour créer un lien symbolique entre / var / lib / snapd / snap et / snap:
 
 ` sudo ln -s /var/lib/snapd/snap /snap`
 

## Installer LeagueOfLegends

    snap install --edge leagueoflegends
    snap refresh --candidate wine-platform-runtime
    snap refresh --candidate wine-platform-5-staging
	  snap refresh --beta wine-platform-runtime

Maintenant, snap install --edge sur league ne fonctionne pas, utilise : snap remove leagueoflegends && snap install --devmode --edge leagueoflegends

* Vous devez utiliser ([script](https://github.com/Knackie/leagueoflegends-archlinux/blob/master/launchhelper.sh)) avant de vous connecter au lanceur.

`   chmod +x launchhelper.sh`

Et avant de vous connecter : 
` ./launchhelper.sh` 

 ## Problèmes connus et correctifs pour eux:
 
 ### Le jeu ne démarre pas (Exception non gérée et MIDIMAP_drvOpen in lol ver 9.21):
 Problèmes avec le nouveau lanceur. Vous pouvez le désactiver temporairement de cette façon:
1. Laissez le jeu s'installer et se mettre à jour complètement.
2. Assurez-vous que le client n'est pas en cours d'exécution.
3. Lorsque vous avez complètement mis à jour le jeu, exécutez cette commande sur le terminal pour empêcher le nouveau lanceur de s'exécuter.
4. Après cette commande, lancez le jeu comme d'habitude. Je ne sais pas combien de temps cette méthode fonctionnera.
REMARQUE: avant d'exécuter cette commande, assurez-vous que le lanceur a installé la nouvelle mise à jour du lanceur.
`for f in RiotClientServices.exe RiotClientCrashHandler.exe; do sudo chmod 0 "$HOME/snap/leagueoflegends/common/.wine/drive_c/Riot Games/Riot Client/$f"; sudo chown root:root "$HOME/snap/leagueoflegends/common/.wine/drive_c/Riot Games/Riot Client/$f"; done`

### Le jeu plante après la sélection du personnage(lol ver 9.20):
Actualisez le runtime wine-platform-avec:

    snap refresh --candidate wine-platform-runtime

Finalement, réinstallez le jeu et le jeu-snap avec:

	snap remove leagueoflegends && snap install --devmode --edge leagueoflegends
    
### Le jeu ne s'installe pas (et se bloque à la place):
La version émulée de Windows est probablement définie sur Win7 dans wine (elle reviendra à Win7 après la réinstallation du snap de la ligue). Changez-le en Win XP en exécutant:

    leagueoflegends.winecfg


## La source
Pour cela, j'ai utilisé ce référentiel : https://github.com/mmtrt/leagueoflegends & ce post reddit : https://www.reddit.com/r/leagueoflinux/comments/j07yrg/starting_the_client_script/

Je n'ai pas fait ce repos pour prendre du crédit, juste pour avoir accès à tout sur une seule page.
