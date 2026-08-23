# Firmware Test MCU PCB controle ASUQTR
**Réalisé par Louis Lavallée**

## Contexte du projet
Ce projet fut réalisé dans le câdre du développement continu du sous-marin autonome du club étudiant [ASUQTR](https://oraprdnt.uqtr.uquebec.ca/portail/gscw031?owa_no_site=8035). L'objectif du club ASUQTR est de participer à la compétition internationale [Robosub](https://robosub.org/) où chaque équipe doit concevoir un sous-marin et lui faire accomplir des tâches et missions de manière entièrement autonome.

## Objectif
Les code présentés ici sont destinés à tester le bon fonctionnement du PCB de contrôle réalisé lors du projet de [conception du PCB de contrôle](https://github.com/resistor56k/Conception_PCB_controle_ASUQTR). Ce PCB a été conçu autour du STM32G474VET6, un microcontrôleur sensé convertir des signaux analogiques au format numérique par ses ADC, générer des PWM pour commander les moteurs du sous-marin, lire et commander des GPIO ainsi que communiquer via des bus UART et I2C avec le Jetson Xavier AGX et des capteurs. Deux codes ont été créés pour ce test. L'un est destiné au microcontrôleur du PCB (le STM32G474VET6) et l'autre à la carte Nucleo-F446RE (cette carte utilise le microcontrôleur STM32F446RE). Le code du G474 permet de tester les capacités du PCB de contrôle et le F446 sert d'esclave I2C pour tester l'échange de données.

### Sous-objectifs:
- ***Communication I2C :*** Un bus de communication I2C a été établi entre le microcontrôleur du PCB et la carte Nucleo. Cette dernière doit remplacer le Jetson Xavier AGX avec lequel il faudra échanger les données des capteurs et les commandes des moteurs. Les tests ont été effectués avec des messages de 31 bytes (32 byte avec l'adresse de l'esclave) afin de mesurer le temps maximum pour un échange de données.\
- ***Communication UART :*** Ce bus UART sert à communiquer avec un écran NX4024K032_011 de la marque Nextion. Il permet d'afficher les données échangées sur le bus I2C, les tensions converties par les ADC et le temps d'exécution et la fréquence de la boucle principale dans le main.c. L'utilisation de l'écran Nextion permet aussi de démontrer le bon fonctionnement du bus UART.\
- ***Lecture des ADC :*** Les tensions fournies aux ADC proviennent de potentiomètres. Une fois dans le sous-marin, ces ADC permettront de mesurer les courants consommés par les moteurs.\
- ***Génération des PWM :*** Ces PWM sont transmis à des petits servomoteurs pour simuler le contrôle des moteurs du sous-marin. Dans ce code, les largeurs d'impulsions des PWM sont déduites des mesures de tension des ADC.\
- ***Utilisation du DMA :*** Le DMA (Direct Memory access) a été utilisé pour la plupart des modules employés dans ce code, soit les ADC, le I2C et le UART. L'objectif est d'accélérer les échanges entre les registre et d'alléger la boucle principale du main.c afin de l'accélérer.\
- ***Réduction du temps d'exécution :*** La boucle principale du main.c doit s'exécuter le plus rapidement possible afin d'approvisionner en données capteurs la boucle d'asservissement du sous-marin et transmettre les commandes vers les moteurs à une fréquence suffisante. Si la boucle du microcontrôleur est trop lente, celle de l'asservissement fera ses calculs avec des données périmées ou produira des commandes qui n'arriveront pas aux moteurs.\

## Documentation
**Mapping des pins du MCU avec** ***STM32CubeMX***\
**Programmation des registres du MCU avec** ***STM32CubeProgrammer***\
**Programmation du MCU avec** ***STM32CubeIDE***

Fichier main.c du G474 du PCB: [main.c G474](main_g474.c)\
Fichier main.c de la carte nucleo-F446RE: [main.c F446](main_f446.c)
