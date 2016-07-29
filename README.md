# Eylen Corporation (Ajustements Da Vinci 1.0 Aio)

 ![](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/eylen.jpg?raw=true) ![](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/eylen.jpg?raw=true) ![](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/eylen.jpg?raw=true) ![](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/eylen.jpg?raw=true)


Cette page est destinée aux particuliers possédant une imprimante 3D **"Da Vinci 1.0 AIO"** modifié avec le [Repetier-Firmware-0.92.10](https://github.com/luc-github/Repetier-Firmware-0.92/tree/devt).

## ATTENTION: Je ne serai en aucun cas responsable de ce que vous faites avec votre imprimante. Vous risquez d'endommager votre machine et d'annuler la garantie, pour la Da Vinci 1.0 AIO il n'y à aucun retour possible au Firmware Officiel et le Scanner 3D n'est pas pris en charge pour le moment (29/07/16). Soyez donc averti et conscient des risques que vous prennez.

![](https://images-na.ssl-images-amazon.com/images/I/61yCScw0nyL._SL1000_.jpg)

# Pourquoi ais-je changé de Firmware ?

Aprés plusieurs essais avec les logiciels officiels je me suis forgé une experience de premiére main (Imprimante sécurisée et autonome), mais j'ai voulu augmenter le contrôle de ma machine pour obtenir un paramétrage très détaillé. J'ai aussi remarqué que mon extrudeur, en fin d'impression, avait un gros problème pour retourner à sa position initiale. En effet celui-ci forçait en Y- et ne bougeait pas en X, donc risque de casse. Ce Firmware à corrigé le problème grace a quelques modifications Gcode en fin de programme.

Les avantages du [Repetier-Firmware-0.92.10](https://github.com/luc-github/Repetier-Firmware-0.92/tree/devt): 
- Un contrôle complet de ma machine (Vitesses, Températures, hauteurs de couches, logiciel de contrôle, etc...).
- Du filament choisis par mes soins.
- Un programme Gcode que j'ai configuré pour faciliter mes impressions (Début) et (Fin).
- Et j'en oublie surement.

Pour changer de Firmware j'ai suivis ce tutoriel très complet. (En Anglais) "[Repetier-Firmware-0.92.10](https://github.com/luc-github/Repetier-Firmware-0.92/tree/devt)".

# Fichiers Utiles

[EEPROM Modifié](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/EEPRom-Eylen-CorporationV2.0.epr) "Amélioration des points de palpage pour Autoleveling (G32 S2)".

# Gcode pour Slicer

## Debut

;*****************************************************************

;**                     EYLEN CORPORATION                       **

;**     Programme d'impression 3D par Eylen Corporation         **

;*****************************************************************

G28 ; Position Initiale des axes XYZ

G1 Z5 F5000 ; Dégagement de la buse a 5mm du plateau

G28 ; Position Initiale des axes XYZ

G32 S2 ; Palpage sur 3 points pour mise à niveau du plateau MAJ du Z0 (compensation automatique du défaut de planéité)

G1 F5000 X-3

G1 F5000 Y100

G1 F5000 X5


## Fin

M104 S0 ; Désactivation des températures

M106 S255 ; Refroidissement par ventilateur

G90

G0 X-10

G0 Y100

M109 S40 ; Attente refroidissement

G28 X0  ; Position Initiale de l'axe X

G28 Y0  ; Position Initiale de l'axe Y

M106 S0 ; Ventilateur désactivé

M84     ; Désactivation des moteurs et fin de programme


# Détails

Pour le début de programme l'une des découverte qui a vraiement changé ma façon de régler l'imprimante c'est le G32 S2.
Voici ce qu'explique le Wiki de RepRap

## G32: Palpage Z et calcul de la planéité

###Utilisation

    - G32 
    - G32 Snnn
 

###Parametres

    Snnn (Stockage de la matrice transformée aprés Palpage) 


###Examples

    G32 
    G32 S2 (S2 => Stockage de toutes les donées vers EEPROM)


Palpe le plateau chauffant sur 3 ou plusieurs points prédéfinit (voir M557) et met a jour la transformation de matrice pour la compensation de la plaque chauffante.

RepRapFirmware execute le fichier macro bed.g

### Notes

    - S0 Valeur par défaut. La matrice calculée est mise a jour dans la RAM mais n'est pas stocké dans l'EEPROM. 
    La hauteur Z n'est pas calculée.

    - S1 La matrice calculée est mise a jour dans la RAM mais n'est pas stocké dans l'EEPROM. L'imprimante 
    bouge immédiatement à sa position Z maximale (Capteur Z max requis), et calcule la nouvelle hauteur Z.
    Vous devez utiliser en premier G28 pour mettre la machine en position initiale avant d'utiliser
    G32 Snnn pour que cela marche correctement, ou alors la hauteur Z sera invalide.

    - S2 similaire à S1, excepté la transformation de la matrice et la hauteur Z sont stockés dans l'EEPROM. 

    - S3 La matrice transformée est stockée dans l'EEPROM. La hauteur Z l'est pas calculée. 

C'est tout pour le moment, des mises a jours seront effectués prochainement.
