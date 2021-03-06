---
title: 'Démarrage rapide : Exploration de texte à l’aide de la bibliothèque de client Analyse de texte'
titleSuffix: Azure Cognitive Services
description: Suivez ce guide de démarrage rapide pour effectuer notamment une analyse de sentiments à l’aide de l’API Analyse de texte d’Azure Cognitive Services.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: text-analytics
ms.topic: quickstart
ms.date: 01/20/2021
ms.author: aahi
keywords: exploration de texte, analyse de sentiments, analyse de texte
ms.custom: devx-track-python, devx-track-js, devx-track-csharp, cog-serv-seo-aug-2020
zone_pivot_groups: programming-languages-text-analytics
ms.openlocfilehash: 78d2f0a7b247ac6a9b7bdf5f4fc8b6c7b5ef6eea
ms.sourcegitcommit: b4e6b2627842a1183fce78bce6c6c7e088d6157b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99090708"
---
# <a name="quickstart-use-the-text-analytics-client-library-and-rest-api"></a>Démarrage rapide : Utiliser la bibliothèque de client et l’API REST Analyse de texte

Consultez cet article pour savoir comment utiliser la bibliothèque de client et l’API REST Analyse de texte. Effectuez les étapes suivantes afin de tester les exemples de code pour une exploration de texte :

* analyse de sentiments
* Exploration des opinions
* Détection de la langue
* Reconnaissance d’entité
* Reconnaissance des informations d’identification personnelle
* Extraction d’expressions clés


::: zone pivot="programming-language-csharp"

> [!IMPORTANT]
> * La dernière version stable de l’API Analyse de texte est la version `3.0`.
>    * Veillez à suivre uniquement les instructions concernant la version que vous utilisez.
> * Le code indiqué dans cet article utilise des méthodes synchrones et un stockage d’informations d’identification non sécurisé pour des raisons de simplicité. Pour les scénarios de production, nous vous recommandons d’utiliser les méthodes asynchrones par lots afin d’optimiser les performances et l’extensibilité. Consultez la documentation de référence ci-dessous.
> * Si vous voulez utiliser Analyse de texte pour la santé ou des opérations asynchrones, consultez les exemples sur GitHub pour [C#](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/textanalytics/Azure.AI.TextAnalytics), [Python](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/textanalytics/azure-ai-textanalytics/) ou [Java](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/textanalytics/azure-ai-textanalytics)

[!INCLUDE [C# quickstart](../includes/quickstarts/csharp-sdk.md)]

::: zone-end

::: zone pivot="programming-language-java"

> [!IMPORTANT]
> * La dernière version stable de l’API Analyse de texte est la version `3.0`.
> * Le code indiqué dans cet article utilise des méthodes synchrones et un stockage d’informations d’identification non sécurisé pour des raisons de simplicité. Pour les scénarios de production, nous vous recommandons d’utiliser les méthodes asynchrones par lots afin d’optimiser les performances et l’extensibilité. Consultez la documentation de référence ci-dessous.
Si vous voulez utiliser Analyse de texte pour la santé ou des opérations asynchrones, consultez les exemples sur GitHub pour [C#](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/textanalytics/Azure.AI.TextAnalytics), [Python](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/textanalytics/azure-ai-textanalytics/) ou [Java](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/textanalytics/azure-ai-textanalytics)

[!INCLUDE [Java quickstart](../includes/quickstarts/java-sdk.md)]

::: zone-end

::: zone pivot="programming-language-javascript"

> [!IMPORTANT]
> * La dernière version stable de l’API Analyse de texte est la version `3.0`.
>    * Veillez à suivre uniquement les instructions concernant la version que vous utilisez.
> * Le code indiqué dans cet article utilise des méthodes synchrones et un stockage d’informations d’identification non sécurisé pour des raisons de simplicité. Pour les scénarios de production, nous vous recommandons d’utiliser les méthodes asynchrones par lots afin d’optimiser les performances et l’extensibilité. Consultez la documentation de référence ci-dessous.
> * Vous pouvez également exécuter cette version de la bibliothèque de client Analyse de texte [dans votre navigateur](https://github.com/Azure/azure-sdk-for-js/blob/master/documentation/Bundling.md).

[!INCLUDE [NodeJS quickstart](../includes/quickstarts/nodejs-sdk.md)]

::: zone-end

::: zone pivot="programming-language-python"

> [!IMPORTANT]
> * La dernière version stable de l’API Analyse de texte est la version `3.0`.
>    * Veillez à suivre uniquement les instructions concernant la version que vous utilisez.
> * Le code indiqué dans cet article utilise des méthodes synchrones et un stockage d’informations d’identification non sécurisé pour des raisons de simplicité. Pour les scénarios de production, nous vous recommandons d’utiliser les méthodes asynchrones par lots afin d’optimiser les performances et l’extensibilité. Consultez la documentation de référence ci-dessous. Si vous voulez utiliser Analyse de texte pour la santé ou des opérations asynchrones, consultez les exemples sur GitHub pour [C#](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/textanalytics/Azure.AI.TextAnalytics), [Python](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/textanalytics/azure-ai-textanalytics/) ou [Java](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/textanalytics/azure-ai-textanalytics)

[!INCLUDE [Python quickstart](../includes/quickstarts/python-sdk.md)]

::: zone-end

::: zone pivot="rest-api"

> [!IMPORTANT]
> * La dernière version stable de l’API Analyse de texte est la version `3.0`.
>    * Veillez à suivre uniquement les instructions concernant la version que vous utilisez.

[!INCLUDE [REST API quickstart](../includes/quickstarts/rest-api.md)]

::: zone-end

## <a name="clean-up-resources"></a>Nettoyer les ressources

Si vous souhaitez nettoyer et supprimer un abonnement Cognitive Services, vous pouvez supprimer la ressource ou le groupe de ressources. La suppression du groupe de ressources efface également les autres ressources qui y sont associées.

* [Portail](../../cognitive-services-apis-create-account.md#clean-up-resources)
* [Azure CLI](../../cognitive-services-apis-create-account-cli.md#clean-up-resources)

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Explorer une solution](../text-analytics-user-scenarios.md#analyze-recorded-inbound-customer-calls)

* [Vue d’ensemble d’Analyse de texte](../overview.md)
* [Analyse des sentiments](../how-tos/text-analytics-how-to-sentiment-analysis.md)
* [Reconnaissance d’entités](../how-tos/text-analytics-how-to-entity-linking.md)
* [Détecter la langue](../how-tos/text-analytics-how-to-keyword-extraction.md)
* [Reconnaissance de la langue](../how-tos/text-analytics-how-to-language-detection.md)
