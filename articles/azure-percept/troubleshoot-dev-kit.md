---
title: Résoudre les problèmes généraux liés au DK Azure Percept et à IoT Edge
description: Découvrez des conseils pour le dépannage pour certains des problèmes les plus courants rencontrés lors de l’expérience d’intégration
author: mimcco
ms.author: mimcco
ms.service: azure-percept
ms.topic: how-to
ms.date: 02/18/2021
ms.custom: template-how-to
ms.openlocfilehash: c8027b62c0c463e134817f589ba3e1957cea5b39
ms.sourcegitcommit: b4647f06c0953435af3cb24baaf6d15a5a761a9c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2021
ms.locfileid: "101678373"
---
# <a name="azure-percept-dk-dev-kit-troubleshooting"></a>Dépannage du DK (kit de développement) Azure Percept

Consultez les conseils ci-dessous pour obtenir des conseils généraux de dépannage pour le DK Azure Percept.

## <a name="general-troubleshooting-commands"></a>Commandes de dépannage générales

Pour exécuter ces commandes : 
1. Connectez-vous à l’[AP Wi-Fi du kit de développement](./quickstart-percept-dk-set-up.md)
1. [Établissez une session SSH avec le kit de développement](./how-to-ssh-into-percept-dk.md)
1. Entrez les commandes dans le terminal SSH.

Pour rediriger une sortie vers un fichier .txt de façon à l’analyser de façon plus approfondie, utilisez la syntaxe suivante :

```console
[command] > [file name].txt
```

Après avoir redirigé la sortie vers un fichier .txt, copiez le fichier sur votre PC hôte via SCP :

```console
scp [remote username]@[IP address]:[remote file path]/[file name].txt [local host file path]
```

```[local host file path]``` fait référence à l’emplacement sur votre PC hôte où vous voulez copier le fichier .txt. ```[remote username]``` est le nom d’utilisateur SSH choisi lors de l’[expérience de configuration](./quickstart-percept-dk-set-up.md). Si vous n’avez pas configuré une connexion SSH lors de l’expérience OOBE, votre nom d’utilisateur distant est ```root```.

Pour plus d’informations sur les commandes Azure IoT Edge, consultez la [documentation sur la résolution des problèmes liés aux appareils Azure IoT Edge](https://docs.microsoft.com/azure/iot-edge/troubleshoot).

|Catégorie :         |Commande :                    |Fonction :                  |
|------------------|----------------------------|---------------------------|
|Système d’exploitation                |```cat /etc/os-release```         |vérifier la version de l’image de Mariner |
|Système d’exploitation                |```cat /etc/os-subrelease```      |vérifier la version de l’image dérivée |
|Système d’exploitation                |```cat /etc/adu-version```        |vérifier la version d’ADU |
|Température       |```cat /sys/class/thermal/thermal_zone0/temp``` |vérifier la température de kit de développement |
|Wi-Fi             |```journalctl -u hostapd.service``` |vérifier les journaux SoftAP|
|Wi-Fi             |```journalctl -u wpa_supplicant.service``` |vérifier les journaux des services Wi-Fi |
|Wi-Fi             |```journalctl -u ztpd.service```  |vérifier journaux du service de provisionnement Wi-Fi Zero Touch |
|Wi-Fi             |```journalctl -u systemd-networkd``` |vérifier les journaux de la pile réseau de Mariner |
|Wi-Fi             |```/data/misc/wifi/hostapd_virtual.conf``` |vérifier les détails de la configuration du point d’accès Wi-Fi |
|OOBE              |```journalctl -u oobe -b```       |vérifier les journaux OOBE |
|Télémétrie         |```azure-device-health-id```      |rechercher le HW_ID de télémétrie unique |
|Azure IoT Edge          |```sudo iotedge check```          |exécuter des vérifications de configuration et de connectivité pour les problèmes courants |
|Azure IoT Edge          |```sudo iotedge logs [container name]``` |vérifier les journaux des conteneurs, comme les modules de reconnaissance vocale et de vision |
|Azure IoT Edge          |```sudo iotedge support-bundle --since 1h``` |collecter les journaux des modules, les journaux du gestionnaire de sécurité Azure IoT Edge, les journaux du moteur de conteneurs, la sortie JSON de ```iotedge check``` et d’autres informations de débogage utiles au cours de la dernière heure |
|Azure IoT Edge          |```sudo journalctl -u iotedge -f``` |visualiser les journaux du gestionnaire de sécurité Azure IoT Edge |
|Azure IoT Edge          |```sudo systemctl restart iotedge``` |redémarrer le démon de sécurité Azure IoT Edge |
|Azure IoT Edge          |```sudo iotedge list```           |lister les modules Azure IoT Edge déployés |
|Autres             |```df [option] [file]```          |afficher des informations sur l’espace disponible/total dans le ou les systèmes de fichiers spécifiés |
|Autres             |```ip route get 1.1.1.1```        |afficher des informations sur l’interface et l’adresse IP des appareils |
|Autres             |```ip route get 1.1.1.1 \| awk '{print $7}'``` <br> ```ifconfig [interface]``` |afficher seulement l’adresse IP des appareils |


Les commandes Wi-Fi ```journalctl``` peuvent être combinées dans la commande suivante :

```console
journalctl -u hostapd.service -u wpa_supplicant.service -u ztpd.service -u systemd-networkd -b
```

## <a name="docker-troubleshooting-commands"></a>Commandes de dépannage de Docker

|Commande :                        |Fonction :                  |
|--------------------------------|---------------------------|
|```docker ps``` |[montre les conteneurs en cours d’exécution](https://docs.docker.com/engine/reference/commandline/ps/) |
|```docker images``` |[montre les images qui se trouvent sur l’appareil](https://docs.docker.com/engine/reference/commandline/images/)|
|```docker rmi [image id] -f``` |[supprime une image de l’appareil](https://docs.docker.com/engine/reference/commandline/rmi/) |
|```docker logs -f edgeAgent``` <br> ```docker logs -f [module_name]``` |[prend les journaux des conteneurs du module spécifié](https://docs.docker.com/engine/reference/commandline/logs/) |
|```docker image prune``` |[supprime toutes les images sans étiquette](https://docs.docker.com/engine/reference/commandline/image_prune/) |
|```watch docker ps``` <br> ```watch ifconfig [interface]``` |vérifier l’état du téléchargement du conteneur Docker |

## <a name="usb-updating"></a>Mise à jour USB

|Erreur :                                    |Solution :                                               |
|------------------------------------------|--------------------------------------------------------|
|LIBUSB_ERROR_XXX pendant la mise à jour flash USB via UUU |Cette erreur est le résultat d’un échec de connexion USB lors de la mise à jour UUU. Si le câble USB n’est pas connecté correctement aux ports USB sur le PC ou le PE-10X, une erreur de ce type se produit. Essayez en débranchant et en reconnectant les deux extrémités du câble USB, et en secouant légèrement le câble pour garantir une connexion sécurisée. Ceci résout presque toujours le problème. |

## <a name="azure-percept-dk-carrier-board-led-states"></a>États des LED de la carte mère du DK Azure Percept

Il y a trois petites LED en haut du support de la carte mère. Une icône de nuage figure à côté de la LED 1, une icône de Wi-Fi figure à côté de la LED 2 et une icône de point d’exclamation figure à côté de la LED 3. Pour plus d’informations sur chaque LED d’état, consultez le tableau ci-dessous.

|LED             |State      |Description                      |
|----------------|-----------|---------------------------------|
|LED 1 (IoT Hub) |Activé (allumée en continu) |L’appareil est connecté à un hub IoT. |
|LED 2 (Wi-Fi)   |Clignotement lent |L’authentification de l’appareil est en cours. |
|LED 2 (Wi-Fi)   |Clignotement rapide |L’authentification a réussi, l’association de l’appareil est en cours. |
|LED 2 (Wi-Fi)   |Activé (allumée en continu) |L’authentification et l’association ont réussi ; l’appareil est connecté à un réseau Wi-Fi. |
|LED 3           |N/D         |LED non utilisée. |


