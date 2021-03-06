---
title: Alertes de sécurité personnalisées
description: En savoir plus sur les alertes de sécurité personnalisables et les actions de correction recommandées à l’aide des fonctionnalités et du service Defender pour IoT.
services: defender-for-iot
ms.service: defender-for-iot
documentationcenter: na
author: mlottner
manager: rkarlin
editor: ''
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2020
ms.author: mlottner
ms.openlocfilehash: 021b05176da141fad2f4555b0617b5a4a51e453f
ms.sourcegitcommit: 4784fbba18bab59b203734b6e3a4d62d1dadf031
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99809284"
---
# <a name="defender-for-iot-custom-security-alerts"></a>Alertes de sécurité personnalisées Defender pour IoT

Defender pour IoT analyse continuellement votre solution IoT à l’aide d’analyses avancées et d’informations sur les menaces pour vous alerter en cas d’activités malveillantes.

Nous vous encourageons à créer des alertes personnalisées en fonction de votre connaissance du comportement attendu de l’appareil afin de veiller à ce que les alertes servent d'indicateurs efficaces en cas de compromission potentielle au sein du déploiement et du paysage uniques de votre organisation.

Vous pouvez définir les alertes Defender pour IoT suivantes selon le comportement IoT Hub et/ou de l’appareil attendu. Pour plus d’informations sur la personnalisation de chaque alerte, consultez [Créer des alertes personnalisées](quickstart-create-custom-alerts.md).

## <a name="built-in-custom-alerts-in-the-iot-hub"></a>Alertes intégrées et personnalisées dans IoT Hub

| severity | Nom de l’alerte | Source de données | Description | Correction suggérée |
|--|--|--|--|--|
| Faible | Alerte personnalisée : le nombre de messages cloud-à-appareil dans le protocole AMQP est en dehors de la plage autorisée | IoT Hub | Le nombre de messages cloud-à-appareil (protocole AMQP) dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |  |
| Faible | Alerte personnalisée : le nombre de messages cloud-à-appareil rejetés dans le protocole AMQP est en dehors de la plage autorisée | IoT Hub | Le nombre de messages cloud-à-appareil (protocole AMQP) rejetés par l’appareil dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |  |
| Faible | Alerte personnalisée : le nombre de messages appareil-à-cloud dans le protocole AMQP est en dehors de la plage autorisée | IoT Hub | Le nombre de messages appareil-à-cloud (protocole AMQP) dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |  |
| Faible | Alerte personnalisée : le nombre d’appels de méthode directe est en dehors de la plage autorisée | IoT Hub | Le nombre d’appels de méthode directe dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |  |
| Faible | Alerte personnalisée : le nombre de chargements de fichiers est en dehors de la plage autorisée | IoT Hub | Le nombre de nombre de chargements de fichiers dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |  |
| Faible | Alerte personnalisée : le nombre de messages cloud-à-appareil dans le protocole HTTP est en dehors de la plage autorisée | IoT Hub | La quantité de messages cloud-à-appareil (protocole HTTP) dans une fenêtre de temps n’est pas dans la plage autorisée configurée |
| Faible | Alerte personnalisée : le nombre de messages cloud-à-appareil rejetés dans le protocole HTTP est en dehors de la plage autorisée | IoT Hub | Le nombre de messages cloud-à-appareil (protocole HTTP) dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |
| Faible | Alerte personnalisée : le nombre de messages appareil-à-cloud dans le protocole HTTP est en dehors de la plage autorisée | IoT Hub | Le nombre de messages appareil-à-cloud (protocole HTTP) dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |  |
| Faible | Alerte personnalisée : le nombre de messages cloud-à-appareil dans le protocole MQTT est en dehors de la plage autorisée | IoT Hub | Le nombre de messages cloud-à-appareil (protocole MQTT) dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |  |
| Faible | Alerte personnalisée : le nombre de messages cloud-à-appareil rejetés dans le protocole MQTT est en dehors de la plage autorisée | IoT Hub | Le nombre de messages cloud-à-appareil (protocole MQTT) rejetés par l’appareil dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |
| Faible | Alerte personnalisée : le nombre de messages appareil-à-cloud dans le protocole MQTT est en dehors de la plage autorisée | IoT Hub | Le nombre de messages appareil-à-cloud (protocole MQTT) dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |
| Faible | Alerte personnalisée : le nombre de vidages de file d’attente de commandes est en dehors de la plage autorisée | IoT Hub | Le nombre de vidages de file d’attente de commandes dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |  |
| Faible | Alerte personnalisée : le nombre de mises à jour de jumeau de module est en dehors de la plage autorisée | IoT Hub | Le nombre de mises à jour de jumeau de module dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |
| Faible | Alerte personnalisée : le nombre d’opérations non autorisées est en dehors de la plage autorisée | IoT Hub | Le nombre d’opérations non autorisées dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |


## <a name="agent-based-security-custom-alerts"></a>Alertes de sécurité personnalisées basées sur des agents

| severity | Nom de l’alerte | Source de données | Description | Correction suggérée |
|--|--|--|--|--|
| Faible | Alerte personnalisée : le nombre de connexions actives est en dehors de la plage autorisée | Module de sécurité classique, Azure RTOS | Le nombre de connexions actives dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. | Examinez les journaux de l’appareil. Découvrez l’origine de la connexion et déterminez si elle est inoffensive ou malveillante. Si cela elle est malveillante, supprimez les programmes malveillants et identifiez la source. Si elles est inoffensive, ajoutez la source à la liste des connexions autorisées. |
| Faible | Alerte personnalisée : la connexion sortante vers une adresse IP non autorisée a été créée | Module de sécurité classique, Azure RTOS | Une connexion sortante a été créée à une adresse IP qui ne figure pas dans votre liste d’adresses IP autorisées. | Examinez les journaux de l’appareil. Découvrez l’origine de la connexion et déterminez si elle est inoffensive ou malveillante. Si cela elle est malveillante, supprimez les programmes malveillants et identifiez la source. Si elles est inoffensive, ajoutez la source à la liste des adresses IP autorisées. |
| Faible | Alerte personnalisée : le nombre de connexions locales ayant échoué est en dehors de la plage autorisée | Module de sécurité classique, Azure RTOS | Le nombre de nombre de connexions locales ayant échoué dans une fenêtre de temps spécifique est en dehors de la plage autorisée actuellement configurée. |  |
| Faible | Alerte personnalisée : connexion d’un utilisateur ne figurant pas sur la liste des utilisateurs autorisés | Module de sécurité classique, Azure RTOS | Un utilisateur local ne figurant pas sur la liste des utilisateurs autorisés s’est connecté à l’appareil. | Si vous enregistrez des données brutes, accédez à votre compte Log Analytics et utilisez les données pour examiner l’appareil, identifier la source, puis corriger la liste verte ou rouge pour ces paramètres. Si vous n’enregistrez pas actuellement de données brutes, accédez à l’appareil, puis corrigez la liste verte ou rouge pour ces paramètres. |
| Faible | Alerte personnalisée : un processus non autorisé a été exécuté | Module de sécurité classique, Azure RTOS | Un processus non autorisé a été exécuté sur l’appareil. | Si vous enregistrez des données brutes, accédez à votre compte Log Analytics et utilisez les données pour examiner l’appareil, identifier la source, puis corriger la liste verte ou rouge pour ces paramètres. Si vous n’enregistrez pas actuellement de données brutes, accédez à l’appareil, puis corrigez la liste verte ou rouge pour ces paramètres. |
|

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment [personnaliser une alerte](quickstart-create-custom-alerts.md)
- [Vue d’ensemble](overview.md) du service Defender pour IoT
- Découvrez comment [accéder à vos données de sécurité](how-to-security-data-access.md)
- En savoir plus sur [l’examen d’un appareil](how-to-investigate-device.md)
