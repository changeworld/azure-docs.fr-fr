---
title: Réponse rapide Azure DDoS
description: Découvrez comment faire appel à des experts DDoS pendant une attaque active en vue d’un support spécialisé.
services: ddos-protection
documentationcenter: na
author: yitoh
ms.service: ddos-protection
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/28/2020
ms.author: yitoh
ms.openlocfilehash: 8e860bf47420f2b58c44df695da7761bcc2aa0ce
ms.sourcegitcommit: 27d616319a4f57eb8188d1b9d9d793a14baadbc3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/15/2021
ms.locfileid: "100521779"
---
# <a name="azure-ddos-rapid-response"></a>Réponse rapide Azure DDoS

Lors d’un accès actif, les clients Azure DDoS Protection Standard ont accès à l’équipe de réponse rapide DDoS (DRR), qui peut aider à faire des recherches sur une attaque au cours d’une attaque et une analyse après l’attaque.

## <a name="prerequisites"></a>Prérequis

- Avant de pouvoir exécuter la procédure de ce tutoriel, vous devez créer un [plan de protection Azure DDoS Standard](manage-ddos-protection.md).

## <a name="when-to-engage-drr"></a>Quand faire appel à DRR

Vous ne devez faire appel à DRR que dans les cas suivants : 

- Au cours d’une attaque DDoS, vous constatez que les performances de la ressource protégée sont considérablement altérées ou que la ressource n’est pas disponible. 
- Vous pensez que votre ressource fait l’objet d’une attaque DDoS, mais le service de protection DDoS n’atténue pas efficacement l’attaque.
- Vous planifiez un événement viral qui peut accroître considérablement votre trafic réseau.
- Pour les attaques qui ont un impact critique sur l’activité.

## <a name="engage-drr-during-an-active-attack"></a>Faire appel à DRR pendant une attaque active

1. Sur le portail Azure lors de la création d’une nouvelle demande de support, choisissez le **Type de problème** Technique.
2. Choisissez la **Protection DDOS** **Service**.
3. Choisissez une ressource dans le menu déroulant des ressources. _Vous devez sélectionner un plan DDoS lié au réseau virtuel protégé par la protection DDoS standard pour faire appel à DRR._

    ![Choisissez Ressource](./media/ddos-rapid-response/choose-resource.png)

4. Sur la page suivante **Problème**, sélectionnez la **gravité** A - Impact critique et le **Type de problème** « Attaque en cours ».

    ![Gravité et type de problème](./media/ddos-rapid-response/severity-and-problem-type.png)

5. Complétez les détails supplémentaires et envoyez la demande de support.

DRR suit le modèle de support Azure Rapid Response. Pour plus d’informations sur Rapid Response, consultez [Étendue du support et réactivité](https://azure.microsoft.com/en-us/support/plans/response/).

Pour en savoir plus, lisez la [Documentation Azure DDoS Protection Standard](./ddos-protection-overview.md).

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment [tester à l’aide de simulations](test-through-simulations.md).
- Découvrez comment [consulter et configurer la télémétrie de la protection DDoS](telemetry.md).
- Découvrez comment [afficher et configurer la journalisation des diagnostics DDoS](diagnostic-logging.md).
