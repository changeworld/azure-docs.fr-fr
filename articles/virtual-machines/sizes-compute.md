---
title: Tailles des machines virtuelles Azure – Optimisées pour le calcul | Microsoft Docs
description: Répertorie les différentes tailles optimisées pour le calcul pour les machines virtuelles dans Azure. Répertorie des informations sur le nombre de processeurs virtuels, de disques de données et de cartes réseau, ainsi que sur le débit de stockage et la bande passante réseau pour les tailles disponibles dans cette série.
author: mimckitt
ms.service: virtual-machines
ms.subservice: vm-sizes-compute
ms.topic: conceptual
ms.workload: infrastructure-services
ms.date: 02/03/2020
ms.author: mimckitt
ms.openlocfilehash: 01eba7bff571a8db25591b8bfa5c5e712511588f
ms.sourcegitcommit: 7edadd4bf8f354abca0b253b3af98836212edd93
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2021
ms.locfileid: "102557690"
---
# <a name="compute-optimized-virtual-machine-sizes"></a>Tailles de machine virtuelle à calcul optimisé

Les machines virtuelles optimisées pour le calcul ont un ratio UC/mémoire élevé. Ces tailles conviennent pour les serveurs web au trafic moyen, les appliances réseau, les processus de traitement par lot et les serveurs d’application. Cet article donne des informations sur le nombre de processeurs virtuels, de disques de données et de cartes réseau. Il comprend également des informations relatives au débit de stockage et à la bande passante réseau pour chacune des tailles de ce regroupement.

La [série Fsv2](fsv2-series.md) s’exécute sur les processeurs Intel® Xeon® Platinum 8272CL (Cascade Lake) de seconde génération et les processeurs Intel® Xeon® Platinum 8168 (Skylake). Il est doté d’une fréquence d’horloge turbo tous cœurs prolongée de 3,4 GHz et d’une fréquence turbo monocœur maximale de 3,7 GHz. Les instructions Intel® AVX-512 sont une nouveauté sur les processeurs Intel Scalable. Elles fourniront jusqu’à 2X plus de performances pour les charges de travail de traitement vectoriel pour les opérations en virgule flottante simple ou double précision. En d’autres termes, elles sont très rapides pour les charges de travail de calcul.

Affichant le coût le plus bas par heure, la série Fsv2 offre le meilleur rapport prix-performances de la gamme Azure si l’on considère les unités de calcul Azure (ACU) par processeur virtuel.

## <a name="other-sizes"></a>Autres tailles

- [Usage général](sizes-general.md)
- [Mémoire optimisée](sizes-memory.md)
- [Optimisé pour le stockage](sizes-storage.md)
- [Optimisé pour le GPU](sizes-gpu.md)
- [Calcul haute performance](sizes-hpc.md)
- [Générations précédentes](sizes-previous-gen.md)

## <a name="next-steps"></a>Étapes suivantes

Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.

Pour plus d’informations sur la façon dont Azure nomme ses machines virtuelles, consultez [Conventions de nommage des tailles de machines virtuelles Azure](./vm-naming-conventions.md).