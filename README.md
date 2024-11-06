# 2324_ESE3745_BelliardPriou
> Noms : Oliver BELLIARD & Valérian PRIOU

## 1. Objectifs
A partir d'un hacheur complet et d'une carte Nucleo-STM32G474RE, vous devez :
- Réaliser un shell pour commander le hacheur,
- Réaliser la commande des 4 transistors du hacheur en commande complémentaire décalée,
- Faire l'acquisition des différents capteurs,
- Réaliser l'asservissement en temps réel.
  
Les livrables demandés :
- Tout le projet stm32cubeIDE synchronisé sur un github dès la première séance de TP,
- Un fichier readme du Github reprenant l'ensemble des éléments demandés (nom obligatoire : 2324_ESE3745_<Nom1><Nom2>),
- Une documentation réalisée pour toutes les fonctions écrites avec Doxygen.  
  
Votre projet github doit être public ou partagé avec votre professeur (nicolas.papazoglou@ensea.fr ou alexis.martin@ensea.fr).  
  
L'évaluation aura lieu tout au long des séances de TP sur plusieurs points :
- Avancement dans le sujet,
- Aptitude a réutiliser les notions vue en cours,
- Habilité à aller chercher dans la documentation les informations utiles,
- Qualité de la documentation
- Lisibilité du code et qualité du code (mise en place de fonctions, factorisation du code, choix des noms de variables/fonctions explicites)
- Présence et ponctualité,
  
## 2. Bonnes pratiques

Pour une meilleure lisibilité du code :
- Toutes les variables sont écrites en minuscule avec une majuscule pour les premières lettre à partir du 2eme mot dans le nom de la variable, par exemple : uartRxBuffer
- Les directives (macro avec #define) sont écrites en majuscule, par exemple : #define UART_TX_SIZE
- Aucun nombre magique ne peut exister, par exemple : remplacer if(value == 512) par if(value == VAL_MAX) avec #define VAL_MAX 512
- Si vous écrivez deux fois le même code, il faut écrire une fonction pour "factoriser" votre code.
- Il faut tester vos appels de fonction, les fonctions HAL renvoient pour la pluspart une valeur pour savoir si son éxécution s'est déroulé correctement.
    
## 3. Github et Doxygen
Installer Doxygen et faire une première documentation (https://doxygen.nl/index.html)  
> To launch Doxygen GUI, `doxywizard` must be typed in the terminal.

## 4. PCB
Tout le projet Kicad de la cartes est disponible dans l'archive Inverter_Kicad_Project.  
Inverter Projet Kicad : https://github.com/DBXYD/AAP_ENSEA_Inverter/tree/master

## 5. Console UART

Dans un premier temps nous allons paramétrer la liaison UART de la carte NUCLEO-G474RE.  
  
Plusieurs fonctionnalités sont déjà codées :
- La présence d'un écho pour tous les caractères pour voir ce que l'on envoie.  
- Lorsque le caractère "ENTER" est détecté, traiter la chaine de caractères en la comparant aux commandes connues, pour le moment nous resterons à un nombre limitée de commandes.  
  
Les fonctions déjà présentes fournissent le couple de valeur "argc" "argv[]" communément connu lorsque vous codez sur PC.
Vous allez devoir au cours du TP (pas maintenant), coder les fonctions suivantes et les maintenant à jour :
- help : qui affiche toutes les commandes disponibles,
- start : qui allume l'étage de puissance du moteur (pour l'instant nous ne ferons qu'afficher un message de "power on" dans la console)
- stop : qui éteind l'étage de puissance du moteur (pour l'instant nous ne ferons qu'afficher un message de "power off" dans la console)
- tout autre fonction qui vous semble nécessaire
- toute autre commande renverra un message dans la console "Command not found"

## 6. Séance 1 - Commande MCC basique

Commande de MCC - niveau basique

Objectifs :
- Générer 4 PWM en complémentaire décalée pour contrôler en boucle ouverte le moteur en respectant le cahier des charges,
- Inclure le temps mort,
- Vérifier les signaux de commande à l'oscilloscope,
- Prendre en main le hacheur,
- Faire un premier essai de commande moteur.

### 6.1. Génération de 4 PWM

Générer quatre PWM sur les bras de pont U et V pour controler le hacheur à partir du timer déjà attribué sur ces pins.  

Cahier des charges :
- Fréquence de la PWM : 20kHz
- Temps mort minimum : à voir selon la datasheet des transistors (faire valider la valeur)
- Résolution minimum : 10bits.
  
Pour les tests, fixer le rapport cyclique à 60%.  
Une fois les PWM générées, les afficher sur un oscilloscope et les faire vérifier par votre professeur.  
