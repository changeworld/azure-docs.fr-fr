---
title: Mettre à l’échelle des unités réservées Multimédia - CLI
description: Cette rubrique explique comment utiliser la CLI pour la mise à l’échelle du traitement multimédia avec Azure Media Services.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to
ms.date: 09/30/2020
ms.author: inhenkel
ms.openlocfilehash: a07c4a20b854e09daf3b320b8c99757ca99b2578
ms.sourcegitcommit: f7eda3db606407f94c6dc6c3316e0651ee5ca37c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102213808"
---
# <a name="how-to-scale-media-reserved-units"></a>Mise à l'échelle des unités réservées Multimédia

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Cet article explique comment procéder à la mise à l'échelle des unités réservées Multimédia (MRU) afin d'accélérer l'encodage.

## <a name="prerequisites"></a>Prérequis

[Créer un compte Media Services](./create-account-howto.md).

Familiarisez-vous avec les [unités réservées Multimédia](concept-media-reserved-units.md).

## <a name="scale-media-reserved-units-with-cli"></a>Mettre à l’échelle les unités réservées au multimédia avec l’interface CLI

Exécutez la commande `mru`.

La commande [az ams account mru](/cli/azure/ams/account/mru) suivante définit les unités réservées au multimédia sur le compte « amsaccount » à l’aide des paramètres **count** et **type**.

```azurecli
az ams account mru set -n amsaccount -g amsResourceGroup --count 10 --type S3
```

## <a name="billing"></a>Facturation

Vous êtes facturé en fonction du nombre de minutes pendant lesquelles les unités réservées Multimédia sont approvisionnées dans votre compte. Ceci est indépendant d'éventuels travaux en cours d'exécution dans votre compte. Pour plus d’informations, consultez la section FAQ de la page [Tarification Media Services](https://azure.microsoft.com/pricing/details/media-services/).   

## <a name="next-step"></a>Étape suivante

[Analyser des vidéos](analyze-videos-tutorial-with-api.md)

## <a name="see-also"></a>Voir aussi

* [Quotas et limites](limits-quotas-constraints.md)
