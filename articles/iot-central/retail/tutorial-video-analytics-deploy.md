---
title: 'Tutoriel : Comment déployer le modèle d’application d’analytique vidéo pour la détection d’objets et de mouvements Azure IoT Central'
description: Tutoriel - Ce guide résume les étapes de déploiement d’une application Azure IoT Central à l’aide du modèle d’application d’analytique vidéo pour la détection d’objets et de mouvements.
services: iot-central
ms.service: iot-central
ms.subservice: iot-central-retail
ms.topic: tutorial
ms.author: nandab
author: KishorIoT
ms.date: 07/31/2020
ms.openlocfilehash: c578da7e83a39f84e72b550038bd87dde3c61d28
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101727462"
---
# <a name="tutorial-how-to-deploy-an-iot-central-application-using-the-video-analytics---object-and-motion-detection-application-template"></a>Tutoriel : Comment déployer une application IoT Central à l’aide du modèle d’application d’analytique vidéo pour la détection d’objets et de mouvements

Pour obtenir une vue d’ensemble des composants d’application clés d’*analytique vidéo pour la détection d’objets et de mouvements*, consultez l’[architecture de l’application d’analytique vidéo pour la détection d’objets et de mouvements](architecture-video-analytics.md).

La vidéo suivante fournit une procédure pas à pas sur l’utilisation du _modèle d’application d’analytique vidéo – détection d’objets et de mouvements_ pour déployer une solution IoT Central :

> [!VIDEO https://www.youtube.com/embed/Bo3FziU9bSA]

Dans cet ensemble de tutoriels, vous découvrez comment :

> [!div class="checklist"]
> * Déployer l’application
> * Déployer une instance IoT Edge qui se connecte à l’application
> * Superviser et gérer l’application

## <a name="prerequisites"></a>Prérequis

Un abonnement Azure est recommandé. Vous pouvez également utiliser une version d’évaluation gratuite pendant 7 jours. Si vous n’avez pas d’abonnement Azure, vous pouvez en créer un sur la [page d’inscription à Azure](https://aka.ms/createazuresubscription).

## <a name="deploy-the-application"></a>Déployer l’application

Procédez comme suit pour déployer une application IoT Central à l’aide du modèle d’application d’analytique vidéo :

1. Suivez le tutoriel [Créer une application d’analytique vidéo dans Azure IoT Central (YOLO v3)](tutorial-video-analytics-create-app-yolo-v3.md) ou [Créer une analytique vidéo dans Azure IoT Central (OpenVINO&trade;)](tutorial-video-analytics-create-app-openvino.md) pour :
    - Créer un compte Azure Media Services.
    - Créer l’application IoT Central à partir du modèle d’application d’analytique vidéo pour la détection d’objets et de mouvements.
    - Configurer un appareil de passerelle dans l’application IoT Central. La passerelle permet aux caméras de se connecter à l’application.

1. Suivez le tutoriel [Créer une instance IoT Edge pour l’analytique vidéo (machine virtuelle Linux)](tutorial-video-analytics-iot-edge-vm.md) ou [Tutoriel : Créer une instance IoT Edge pour l’analytique vidéo (Intel NUC)](tutorial-video-analytics-iot-edge-nuc.md) pour :
    - Créer une machine virtuelle Azure sur laquelle est installé le runtime Azure IoT Edge. Préparer l’installation IoT Edge pour héberger le module d’analytique vidéo.
    - Connecter l’appareil IoT Edge à votre application IoT Central.

1. Effectuez le tutoriel [Superviser et gérer une application d’analytique vidéo](tutorial-video-analytics-manage.md) pour :
    - Ajouter des caméras de détection d’objet et de mouvement à la passerelle dans votre application IoT Central.
    - Démarrer le traitement de la caméra.
    - Installer un lecteur multimédia local pour afficher la vidéo capturée dans AMS.
    - Afficher la vidéo capturée qui montre les objets détectés.
    - Nettoyer.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Une fois que vous en avez terminé avec l’application, vous pouvez supprimer toutes les ressources que vous avez créées de la façon suivante :

1. Dans l’application IoT Central, dans la section **Administration**, accédez à la page **Votre application** . Puis sélectionnez **Supprimer**.
1. Dans le portail Azure, supprimez le groupe de ressources **lva-rg**.
1. Sur votre ordinateur local, arrêtez le conteneur Docker **amp-Viewer**.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous disposez d’une vue d’ensemble des étapes de déploiement et de l’utilisation du modèle d’application d’analytique vidéo, consultez :

> [!div class="nextstepaction"]
> [Créer une application d’analytique vidéo dans Azure IoT Central (YOLO v3)](tutorial-video-analytics-create-app-yolo-v3.md) ou

> [!div class="nextstepaction"]
> [Créer une application d’analytique vidéo dans Azure IoT Central (OpenVINO&trade;)](tutorial-video-analytics-create-app-openvino.md).