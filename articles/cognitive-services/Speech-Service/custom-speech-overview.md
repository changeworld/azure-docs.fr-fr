---
title: Vue d’ensemble de Custom Speech - Service Speech
titleSuffix: Azure Cognitive Services
description: Custom Speech est un ensemble d’outils en ligne qui vous permettent d’évaluer et d’améliorer l’exactitude de la reconnaissance vocale de Microsoft pour vos applications, outils et produits.
services: cognitive-services
author: trevorbye
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 02/12/2021
ms.author: trbye
ms.custom: contperf-fy21q2; references_regions
ms.openlocfilehash: 39370659e71a7d281914b360eea83eb0b68b25ba
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101716565"
---
# <a name="what-is-custom-speech"></a>Qu’est-ce que Custom Speech ?

[Custom Speech](https://aka.ms/customspeech) est un ensemble d’outils basés sur une IU, qui vous permettent d’évaluer et d’améliorer l’exactitude de la reconnaissance vocale de Microsoft pour vos applications, outils et produits. Pour bien démarrer, il vous suffit de quelques fichiers audio de test. Suivez les liens fournis dans cet article pour commencer à créer une expérience de reconnaissance vocale personnalisée.

## <a name="whats-in-custom-speech"></a>Qu’y a-t-il dans Custom Speech ?

Pour pouvoir tirer parti de Custom Speech, vous avez besoin d’un compte Azure et d’un abonnement au service Speech. Une fois que vous disposez d’un compte, vous pouvez préparer vos données, effectuer l’apprentissage de vos modèles et les tester, inspecter la qualité de la reconnaissance, évaluer l’exactitude et en dernier lieu déployer et utiliser le modèle de reconnaissance vocale personnalisé.

Ce diagramme met en évidence les éléments qui composent la [zone Custom Speech de Speech Studio](https://aka.ms/customspeech). Utilisez les liens ci-dessous pour en savoir plus sur chaque étape.

![Diagramme qui met en évidence les composants de la zone Custom Speech de Speech Studio.](./media/custom-speech/custom-speech-overview.png)

1. [Abonnez-vous et créez un projet](#set-up-your-azure-account). Créez un compte Azure et abonnez-vous au service Speech. Cet abonnement unifié vous donne accès à la conversion de parole en texte, à la conversion de texte par synthèse vocale, à la traduction vocale et à [Speech Studio](https://speech.microsoft.com/customspeech). Ensuite, servez-vous de votre abonnement au service Speech pour créer votre premier projet Custom Speech.

1. [Charger des données de test](./how-to-custom-speech-test-and-train.md). Chargez des données de test (fichiers audio) pour évaluer l’offre de reconnaissance vocale de Microsoft pour vos applications, outils et produits.

1. [Inspecter la qualité de la reconnaissance](how-to-custom-speech-inspect-data.md). Utilisez [Speech Studio](https://speech.microsoft.com/customspeech) pour lire le contenu audio chargé et inspecter la qualité de la reconnaissance vocale de vos données de test. Pour effectuer des mesures quantitatives, consultez [Inspecter des données](how-to-custom-speech-inspect-data.md).

1. [Évaluer et améliorer l’exactitude](how-to-custom-speech-evaluate-data.md). Évaluez et améliorez l’exactitude du modèle de reconnaissance vocale. [Speech Studio](https://speech.microsoft.com/customspeech) indique un *taux d’erreur de mots*, qui vous permet de déterminer si un entraînement supplémentaire est nécessaire. Si le résultat vous paraît suffisamment juste, vous pouvez directement utiliser les API du service Speech. Si vous souhaitez améliorer l’exactitude de 5 à 20 % en moyenne relative, utilisez l’onglet **Formation** du portail pour charger des données d’entraînement supplémentaires, comme des transcriptions étiquetées à la main et le texte associé.

1. [Effectuer l’apprentissage d’un modèle et le déployer](how-to-custom-speech-train-model.md). Améliorez l’exactitude de votre modèle de reconnaissance vocale en joignant des transcriptions écrites (entre 10 et 1 000 heures) et un texte associé (< 200 Mo) à vos données de test audio. Ces données vous aident à entraîner le modèle de reconnaissance vocale. Après l’apprentissage, retestez. Si vous êtes satisfait du résultat, vous pouvez déployer votre modèle sur un point de terminaison personnalisé.

## <a name="set-up-your-azure-account"></a>Configurer votre compte Azure

Vous avez besoin d’un compte Azure et d’un abonnement au service Speech pour pouvoir créer un modèle personnalisé à partir de [Speech Studio](https://speech.microsoft.com/customspeech). Si vous n’avez pas de compte et d’abonnement, [essayez le service Speech gratuitement](overview.md#try-the-speech-service-for-free).

> [!NOTE]
> Veillez à créer un abonnement standard (S0). Les abonnements gratuits (F0) ne sont pas pris en charge.

Si vous comptez effectuer l’entraînement d’un modèle personnalisé avec des **données audio**, choisissez l’une des régions suivantes. Elles disposent d’un matériel dédié à l’entraînement. Cela réduira le temps nécessaire à l’apprentissage d’un modèle, et vous permettra d’utiliser plus de données audio pour l’apprentissage. Dans ces régions, le service Speech utilisera jusqu’à 20 heures d’audio pour l’apprentissage. Dans d’autres, il utilisera moins de 8 heures.

* Australie Est
* Centre du Canada
* Inde centrale
* USA Est
* USA Est 2
* Centre-Nord des États-Unis
* Europe Nord
* États-Unis - partie centrale méridionale
* Asie Sud-Est
* Sud du Royaume-Uni
* Gouvernement des États-Unis – Arizona
* Gouvernement américain - Virginie
* Europe Ouest
* USA Ouest 2

Une fois que vous avez créé un compte Azure et un abonnement au service Speech, vous devez vous connecter à [Speech Studio](https://speech.microsoft.com/customspeech) et connecter votre abonnement.

1. Connectez-vous à [Speech Studio](https://aka.ms/custom-speech).
1. Sélectionnez l’abonnement dans lequel vous devez travailler, puis créez un projet Speech.
1. Si vous souhaitez modifier votre abonnement, sélectionnez le bouton en forme de rouage dans le menu supérieur.

## <a name="how-to-create-a-project"></a>Comment créer un projet

Les contenus tels que les données, les modèles, les tests et les points de terminaison sont organisés en *projets* dans [Speech Studio](https://speech.microsoft.com/customspeech). Chaque projet est propre à un domaine et à un pays/langue. Par exemple, vous pourriez créer un projet pour des centres d’appel utilisant l’anglais aux États-Unis.

Pour créer votre premier projet, sélectionnez **Speech-to-text/Custom speech**, puis **Nouveau projet**. Suivez les instructions fournies par l’Assistant pour créer votre projet. Une fois le projet créé, vous devriez voir quatre onglets : **Data**, **Testing**, **Training** et **Deployment**. Utilisez les liens fournis dans [Étapes suivantes](#next-steps) pour savoir comment utiliser chaque onglet.

> [!IMPORTANT]
> [Speech Studio](https://aka.ms/custom-speech), qui s’appelait « portail Custom Speech », a été récemment mis à jour ! Si vous avez créé antérieurement des données, modèles, tests et points de terminaison publiés sur le portail CRIS.ai ou à l’aide d’API, vous devez créer un projet sur le nouveau portail pour vous connecter à ces anciennes entités.

## <a name="model-lifecycle"></a>Cycle de vie du modèle

Custom Speech utilise des *modèles de base* et des *modèles personnalisés*. Chaque langue comporte un ou plusieurs modèles de base. En règle générale, quand un nouveau modèle vocal est mis à disposition dans le service Speech standard, il est également importé dans le service Custom Speech en tant que nouveau modèle de base. Les modèles sont mis à jour tous les 3 à 6 mois. Les modèles plus anciens deviennent généralement de moins en moins utiles au fil du temps, car le modèle le plus récent est généralement d’une plus grande exactitude.

En revanche, vous créez des modèles personnalisés en choisissant un modèle de base et en l’adaptant à un scénario client particulier. Si vous disposez d’un modèle personnalisé répondant à vos besoins, vous pouvez continuer à utiliser pendant une longue période. Toutefois, nous vous recommandons de mettre régulièrement à jour le modèle de base le plus récent et de réeffectuer son apprentissage au fil du temps avec des données supplémentaires. 

Voici d’autres termes clés liés au cycle de vie du modèle :

* **Adaptation** : personnalisation d’un modèle de base en fonction de votre domaine/scénario à l’aide de données texte et/ou audio.
* **Décodage** : utilisation d’un modèle et exécution d’une reconnaissance vocale (décodage d’audio en texte).
* **Point de terminaison** : déploiement spécifique d’un utilisateur d’un modèle de base ou d’un modèle personnalisé *uniquement* pour un utilisateur donné.

### <a name="expiration-timeline"></a>Chronologie d’expiration

Au fur et à mesure que de nouveaux modèles et de nouvelles fonctionnalités deviennent disponibles et que les anciens modèles, moins justes, sont mis hors service, consultez les chronologies suivantes pour connaître l’expiration des modèles et des points de terminaison :

**Modèles de base** 

* Adaptation : disponible pendant un an. Une fois le modèle importé, il est disponible pendant un an pour créer des modèles personnalisés. Après un an, de nouveaux modèles personnalisés doivent être créés à partir d’une version plus récente du modèle de base.  
* Décodage : disponible pendant deux ans après l’importation. Vous pouvez ainsi créer un point de terminaison et utiliser une transcription par lots pendant deux ans avec ce modèle. 
* Points de terminaison : disponibles sur la même chronologie que le décodage.

**Modèles personnalisés**

* Décodage : disponible pendant deux ans après la création du modèle. Vous pouvez ainsi utiliser le modèle personnalisé pendant deux ans (traitement par lots/temps réel/tests) après sa création. Après deux ans, *vous devez réeffectuer l’apprentissage de votre modèle*, car le modèle de base est généralement déconseillé pour l’adaptation.  
* Points de terminaison : disponibles sur la même chronologie que le décodage.

Quand un modèle de base ou un modèle personnalisé expire, il revient toujours à la *version la plus récente du modèle de base*. Ainsi, votre implémentation ne sera jamais interrompue mais pourrait devenir moins précise pour *vos données spécifiques* si les modèles personnalisés arrivent à expiration. Vous pouvez voir les détails relatifs à l’expiration d’un modèle aux emplacements suivants dans la zone Custom Speech de Speech Studio :

* Récapitulatif de l’entraînement du modèle
* Détail de l’entraînement du modèle
* Résumé du déploiement
* Détail du déploiement

Vous pouvez également vérifier les dates d’expiration via les API [`GetModel`](https://westus.dev.cognitive.microsoft.com/docs/services/speech-to-text-api-v3-0/operations/GetModel) et [`GetBaseModel`](https://westus.dev.cognitive.microsoft.com/docs/services/speech-to-text-api-v3-0/operations/GetBaseModel) de Custom Speech sous la propriété `deprecationDates` dans la réponse JSON.

Notez que vous pouvez mettre à niveau le modèle sur un point de terminaison Custom Speech sans temps d’arrêt en changeant le modèle utilisé par le point de terminaison dans la section de déploiement de Speech Studio ou via l’API Custom Speech.

## <a name="next-steps"></a>Étapes suivantes

* [Préparer et tester les données](./how-to-custom-speech-test-and-train.md)
* [Inspecter les données](how-to-custom-speech-inspect-data.md)
* [Évaluer et améliorer la justesse du modèle](how-to-custom-speech-evaluate-data.md)
* [Entraîner et déployer un modèle](how-to-custom-speech-train-model.md)
