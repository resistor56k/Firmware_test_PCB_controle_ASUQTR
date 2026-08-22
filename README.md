# Firmware Test MCU PCB controle ASUQTR
**Réalisé par Louis Lavallée**

## Contexte du projet
Ce projet fut réalisé dans le câdre du développement continu du sous-marin autonome du club étudiant [ASUQTR](https://oraprdnt.uqtr.uquebec.ca/portail/gscw031?owa_no_site=8035). L'objectif du club ASUQTR est de participer à la compétition internationale [Robosub](https://robosub.org/) où chaque équipe doit concevoir un sous-marin et lui faire accomplir des tâches et missions de manière entièrement autonome.

## Objectif
Les code présentés ici sont destinés à tester le bon fonctionnement du PCB de contrôle réalisé lors du projet de [conception_du PCB_de contrôle](https://github.com/resistor56k/Conception_PCB_controle_ASUQTR). Ce PCB a été conçu autour du STM32G474VET6, un microcontrôleur destiné à convertir des signaux analogiques au format numérique par ses ADC, générer des PWM pour commander les moteurs du sous-marin, lire et commander des GPIO ainsi que communiquer via des bus UART et I2C avec le Jetson Xavier AGX et des capteurs.

### Sous-objectifs:


## Documentation
**Mapping des pins du MCU avec** ***STM32CubeMX***\
**Programmation des registres du MCU avec** ***STM32CubeProgrammer***\
**Programmation du MCU avec** ***STM32CubeIDE***

Fichier main.c du G474 du PCB: [main.c G474](main_g474.c)
Fichier main.c de la carte nucleo-F446RE: [main.c F446](main_f446.c)
