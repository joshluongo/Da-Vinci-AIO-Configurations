# Bienvenue sur le Github de Eylen-Corporation

Cette page est destinée aux particuliers possédant une imprimante 3D **"Da Vinci 1.0 AIO"** modifié avec le [Repetier-Firmware-0.92.10](https://github.com/luc-github/Repetier-Firmware-0.92/tree/devt).

## ATTENTION: Je ne serai en aucun cas responsable de ce que vous faites avec votre imprimante. Vous risquez d'endommager votre machine ou d'annuler la garantie, pour la Da Vinci 1.0 AIO il n'y à aucun retour possible au Firmware Officiel et le Scanner 3D n'est pas pris en charge pour le moment (29/07/16). Soyez donc averti et conscient des risques que vous prennez.

![](https://images-na.ssl-images-amazon.com/images/I/61yCScw0nyL._SL1000_.jpg)

# Pourquoi ais-je changé de Firmware ?

Aprés plusieurs essais avec les logiciels officiels je me suis forgé une experience de premiére main (Imprimante sécurisée et autonome), mais j'ai voulu augmenter le contrôle de ma machine pour obtenir un paramétrage très détaillé. J'ai aussi remarqué que mon extrudeur, en fin d'impression, avait un gros problème pour retourner à sa position initiale. En effet celui-ci forçais en Y- et ne bougeais pas en X, donc risque de casse. Repetier à corrigé ce problème.

Les avantages du [Repetier-Firmware-0.92.10](https://github.com/luc-github/Repetier-Firmware-0.92/tree/devt): 
- Un contrôle complet de ma machine (Vitesses, Températures, hauteurs de couches, logiciel de contrôle, etc...).
- Du filament choisis par mes soins.
- Un programme Gcode que j'ai configuré pour faciliter mes impressions (Début) et (Fin).
- Et j'en oublie surement.

Pour changer de Firmware j'ai suivis ce tutoriel très complet "[Repetier-Firmware-0.92.10](https://github.com/luc-github/Repetier-Firmware-0.92/tree/devt)".

Fichiers Utiles.

[EEPROM Modifié](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/EEPRom-Eylen-CorporationV2.0.epr)
- Amélioration des points de palpage pour Autoleveling (G32 S2)

## Gcode pour Slicer

# Debut

;*****************************************************************

;**                     EYLEN CORPORATION                       **

;**     Programme d'impression 3D par Eylen Corporation         **

;*****************************************************************

M117 EYLEN CORPORATION ;Afficher un Message LCD

G28 ; home all axes

G1 Z5 F5000 ; lift nozzle

G28 ; home all axis

M117 PALPAGE DU PLATEAU Z0

G32 S2 ; Palpage sur 3 points pour mise a niveau du plateau

G1 F5000 X-3

G1 F5000 Y100

G1 F5000 X5

M117 ;Désactivation message affichage temps d'impression


# Fin

M104 S0 ; Désactivation des températures

M106 S255 ; Refroidissement par ventilateur

M117 VEUILLEZ ATTENDRE LA FIN DU REFROIDISSEMENT

G90

G0 X-10

G0 Y100

M109 S40 ; Attente refroidissement

G28 X0  ; home X axis

G28 Y0  ; home Y axis

M106 S0 ; Ventilateur désactivé

M117

M84     ; Désactivation des moteurs

