---
title: Redimensionner un cluster Azure Stream Analytics
description: Découvrez comment augmenter ou réduire la taille d’un cluster Azure Stream Analytics.
author: sidramadoss
ms.author: sidram
ms.service: stream-analytics
ms.topic: overview
ms.custom: mvc
ms.date: 09/22/2020
ms.openlocfilehash: e469e9bfd13bf8d89084b66e954cb51b27c2ebc2
ms.sourcegitcommit: 42a4d0e8fa84609bec0f6c241abe1c20036b9575
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98020024"
---
# <a name="resize-an-azure-stream-analytics-cluster"></a>Redimensionner un cluster Azure Stream Analytics

La capacité d’un cluster Stream Analytics est mesurée en unités de streaming (SU). Plusieurs travaux peuvent s’exécuter en parallèle au sein du même cluster, à condition que la somme des SU attribuées à tous les travaux en cours d’exécution ne dépasse pas la capacité du cluster.

La capacité du cluster peut faire l’objet d’un scale-up ou d’un scale-down pour correspondre à la taille de vos charges de travail de diffusion en continu. La mise à l’échelle d’un cluster prend du temps et une mise à l’échelle fréquente n’est pas prévue. Nous vous recommandons de planifier et d’approvisionner un cluster avec le nombre précis de SU que vous envisagez de consommer.

## <a name="change-the-scale-of-your-cluster"></a>Modifier l'échelle de votre cluster

1. Sur le portail Azure, recherchez et sélectionnez votre cluster Stream Analytics.

1. Dans la section **Vue d’ensemble**, sélectionnez **Mettre à l'échelle**. Vous pouvez voir combien de SU sont attribuées à votre cluster. Utilisez le sélecteur pour augmenter ou diminuer les SU selon vos besoins.

   ![Mettre le cluster à l’échelle](./media/scale-cluster/scale-cluster.png)

L’opération de mise à l’échelle n’affecte pas les travaux en cours d’exécution.

## <a name="next-steps"></a>Étapes suivantes

Vous savez désormais comment mettre à l’échelle vos clusters Stream Analytics. Découvrez maintenant comment gérer les points de terminaison privés et mettre automatiquement à l’échelle vos travaux :

* [Gérer les points de terminaison privés dans un cluster Azure Stream Analytics](private-endpoints.md)
* [Gérer les travaux dans un cluster Azure Stream Analytics](manage-jobs-cluster.md)
