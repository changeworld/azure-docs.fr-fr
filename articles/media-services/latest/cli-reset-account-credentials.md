---
title: Réinitialiser vos informations d’identification de compte - CLI
description: Utilisez le script Azure CLI pour réinitialiser vos informations d’identification de compte et récupérer les paramètres du fichier app.config.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.assetid: ''
ms.service: media-services
ms.devlang: azurecli
ms.topic: troubleshooting
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/31/2020
ms.author: inhenkel
ms.custom: devx-track-azurecli
ms.openlocfilehash: cc605a08147da1d076b302e515a4ebe8d411a782
ms.sourcegitcommit: 97c48e630ec22edc12a0f8e4e592d1676323d7b0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/18/2021
ms.locfileid: "101091851"
---
# <a name="azure-cli-example-reset-the-account-credentials"></a>Exemple Azure CLI : Réinitialiser les informations d’identification

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Le script Azure CLI de cet article vous montre comment réinitialiser vos informations d’identification de compte et récupérer les paramètres du fichier app.config.

## <a name="prerequisites"></a>Prérequis

[Créer un compte Media Services](./create-account-howto.md).

## <a name="example-script"></a>Exemple de script

```azurecli-interactive
# Update the following variables for your own settings:
resourceGroup=amsResourceGroup
amsAccountName=amsmediaaccountname

az ams account sp reset-credentials \
  --account-name $amsAccountName \
  --resource-group $resourceGroup
 ```

## <a name="next-steps"></a>Étapes suivantes

* [az ams](/cli/azure/ams)
* [Réinitialiser les informations d’identification](/cli/azure/ams/account/sp#az-ams-account-sp-reset-credentials)
