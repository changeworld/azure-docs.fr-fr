---
title: Comparaison des exemples de migration de Media Services v2 et v3
description: Ensemble d’exemples pour vous aider à comparer les différences de code entre Azure Media Services v2 et v3.
services: media-services
author: IngridAtMicrosoft
manager: femila
ms.service: media-services
ms.topic: conceptual
ms.workload: media
ms.date: 1/14/2021
ms.author: inhenkel
ms.openlocfilehash: 640b9b40295ae9b9aea865f7b6159da6ff4a3251
ms.sourcegitcommit: 100390fefd8f1c48173c51b71650c8ca1b26f711
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "98898305"
---
# <a name="media-services-migration-code-sample-comparison"></a>Comparaison des exemples de code de migration de Media Services

![logo du guide de migration](./media/migration-guide/azure-media-services-logo-migration-guide.svg)

<hr color="#5ea0ef" size="10">

Vous pouvez utiliser certains de nos exemples de code pour comparer le fonctionnement des SDK.

## <a name="samples-for-comparison"></a>Exemples à comparer

Le tableau suivant est une liste d’exemples qui permet de comparer v2 et v3 dans les scénarios courants.

|Scénario|API V2|API V3|
|---|---|---|
|Créer une ressource et charger un fichier |[Exemple .NET v2](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L113)|[Exemple .NET v3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L169)|
|Soumettre un travail|[Exemple .NET v2](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L146)|[Exemple .NET v3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L298)<br/><br/>Montre comment créer au préalable une transformation, puis soumettre un travail.|
|Publier une ressource avec chiffrement AES |1. Créez `ContentKeyAuthorizationPolicyOption`.<br/>2. Créez `ContentKeyAuthorizationPolicy`.<br/>3. Créez `AssetDeliveryPolicy`.<br/>4. Créer `Asset` et charger du contenu OU soumettre `Job` et utiliser `OutputAsset`<br/>5. Associer `AssetDeliveryPolicy` à `Asset`<br/>6. Créez `ContentKey`.<br/>7. Joindre `ContentKey` à `Asset`<br/>8. Créez `AccessPolicy`.<br/>9. Créez `Locator`.<br/><br/>[Exemple .NET v2](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L64)|1. Créez `ContentKeyPolicy`.<br/>2. Créez `Asset`.<br/>3. Télécharger du contenu ou utiliser `Asset` en tant que `JobOutput`<br/>4. Créez `StreamingLocator`.<br/><br/>[Exemple .NET v3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/EncryptWithAES/Program.cs#L105)|
|Obtenir des détails de travaux et gérer des travaux |[Gérer des travaux avec v2](../previous/media-services-dotnet-manage-entities.md#get-a-job-reference) |[Gérer des travaux avec v3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L546)|

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [migration guide next steps](./includes/migration-guide-next-steps.md)]
