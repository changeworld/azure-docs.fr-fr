---
title: Définitions de stratégie intégrées pour Azure Security Center
description: Liste les définitions de stratégie intégrées d’Azure Policy pour Azure Security Center. Ces définitions de stratégie intégrées fournissent des approches courantes pour la gestion de vos ressources Azure.
ms.date: 02/09/2021
ms.topic: reference
author: memildin
ms.author: memildin
ms.service: security-center
ms.custom: subject-policy-reference
ms.openlocfilehash: ab6556bc391eb3136fa8c4ba40f5a5d71da956e7
ms.sourcegitcommit: 24f30b1e8bb797e1609b1c8300871d2391a59ac2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2021
ms.locfileid: "100093038"
---
# <a name="azure-policy-built-in-definitions-for-azure-security-center"></a>Définitions intégrées d’Azure Policy pour Azure Security Center

Cette page est un index des définitions de stratégie intégrées d’[Azure Policy](../governance/policy/overview.md) relatives à Azure Security Center. Les regroupements suivants de définitions de stratégie sont disponibles :

- Le groupe [Initiatives](#azure-security-center-initiatives) répertorie les définitions d’initiative d’Azure Policy dans la catégorie « Security Center ».
- Le groupe [Initiative par défaut](#azure-security-center-initiatives) répertorie toutes les définitions d’Azure Policy qui font partie de l’initiative par défaut de Security Center,[Benchmark de sécurité Azure](../security/benchmarks/introduction.md). Ce benchmark largement respecté créé par Microsoft s’appuie sur les contrôles du [Center for Internet Security (CIS)](https://www.cisecurity.org/benchmark/azure/) et du [National Institute of Standards and Technology (NIST)](https://www.nist.gov/), et se focalise sur la sécurité du cloud.
- Le groupe [Catégorie](#azure-security-center-category) répertorie toutes les définitions d’Azure Policy dans la catégorie « Security Center ».

Pour plus d’informations sur les stratégies de sécurité, consultez [Utilisation des stratégies de sécurité](./tutorial-security-policy.md). Pour obtenir des éléments intégrés supplémentaires d’Azure Policy pour d’autres services, consultez [Définitions intégrées d’Azure Policy](../governance/policy/samples/built-in-policies.md).

Le nom de chaque définition de stratégie intégrée est un lien vers la définition de la stratégie dans le portail Azure. Utilisez le lien figurant dans la colonne **Version** pour voir la source dans le [dépôt GitHub Azure Policy](https://github.com/Azure/azure-policy).

## <a name="azure-security-center-initiatives"></a>Initiatives d’Azure Security Center

Pour plus d’informations sur les initiatives intégrées supervisées par Security Center, consultez le tableau suivant :

[!INCLUDE [azure-policy-reference-policyset-security-center](../../includes/policy/reference/bycat/policysets-security-center.md)]

## <a name="azure-security-center-default-initiative"></a>Initiative par défaut d’Azure Security Center

Pour plus d’informations sur les stratégies intégrées supervisées par Security Center, consultez le tableau suivant :

[!INCLUDE [azure-policy-reference-init-asc](../../includes/policy/reference/custom/init-asc.md)]

## <a name="azure-security-center-category"></a>Catégorie d’Azure Security Center

[!INCLUDE [azure-policy-reference-category-securitycenter](../../includes/policy/reference/bycat/policies-security-center.md)]

## <a name="next-steps"></a>Étapes suivantes

Dans cet article, vous avez découvert les définitions de stratégies de sécurité Azure Policy dans Security Center. Pour en savoir plus, consultez les articles suivants.

- Consultez les définitions intégrées dans le [dépôt Azure Policy de GitHub](https://github.com/Azure/azure-policy).
- Consultez la [Structure de définition Azure Policy](../governance/policy/concepts/definition-structure.md).
- Consultez la page [Compréhension des effets de Policy](../governance/policy/concepts/effects.md).
- [Guide des opérations et de planification d’Azure Security Center](./security-center-planning-and-operations-guide.md) : Découvrez les considérations sur la conception dans Azure Security Center et comment les planifier.
- [Surveillance de l’intégrité de la sécurité dans Azure Security Center](./security-center-monitoring.md) : découvrez comment surveiller l’intégrité de vos ressources Azure.
- [Gestion et résolution des alertes de sécurité dans Azure Security Center](./security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.
- [Surveillance des solutions de partenaire avec Azure Security Center](./security-center-partner-integration.md) : découvrez comment surveiller l’état d’intégrité de vos solutions de partenaire.
- [Azure Policy](../governance/policy/overview.md) : découvrez comment contrôler et gérer vos ressources azurées.
