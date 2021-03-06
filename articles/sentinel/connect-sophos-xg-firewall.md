---
title: Connecter des données Sophos XG Firewall à Azure Sentinel | Microsoft Docs
description: Découvrez comment connecter des données Sophos XG Firewall à Azure Sentinel.
services: sentinel
documentationcenter: na
author: yelevin
manager: rkarlin
editor: ''
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.devlang: na
ms.topic: how-to
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2020
ms.author: yelevin
ms.openlocfilehash: 0b8b6247a735bceaf98029740bf9d4f7e233069d
ms.sourcegitcommit: 24f30b1e8bb797e1609b1c8300871d2391a59ac2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2021
ms.locfileid: "100097566"
---
# <a name="connect-your-sophos-xg-firewall-to-azure-sentinel"></a>Connecter Sophos XG Firewall à Azure Sentinel

> [!IMPORTANT]
> Le connecteur de données Sophos XG Firewall dans Azure Sentinel est en préversion publique.
> Cette fonctionnalité est fournie sans contrat de niveau de service et est déconseillée pour les charges de travail de production. Certaines fonctionnalités peuvent être limitées ou non prises en charge. Pour plus d’informations, consultez [Conditions d’Utilisation Supplémentaires relatives aux Évaluations Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Cet article explique comment connecter votre appliance [Sophos XG Firewall](https://www.sophos.com/products/next-gen-firewall.aspx) à Azure Sentinel. Le connecteur de données Sophos XG Firewall vous permet de connecter facilement vos journaux Sophos XG Firewall à Azure Sentinel, de consulter des tableaux de bord, de créer des alertes personnalisées et d’améliorer les enquêtes. L’intégration entre Sophos XG Firewall et Azure Sentinel utilise Syslog.

> [!NOTE]
> Les données seront stockées dans l’emplacement géographique de l’espace de travail sur lequel vous exécutez Azure Sentinel.

## <a name="forward-sophos-xg-firewall-logs-to-the-syslog-agent"></a>Transférer les journaux Sophos XG Firewall à l’agent Syslog  

Configurez Sophos XG Firewall pour transférer les messages Syslog à votre espace de travail Azure par le biais de l’agent Syslog.

1. Dans le portail Azure Sentinel, cliquez sur **Connecteurs de données** et sélectionnez le connecteur **Sophos XG Firewall**.

1. Sélectionnez **Ouvrir la page du connecteur**.

1. Suivez les instructions de la page **Sophos XG Firewall**.

## <a name="find-your-data"></a>Recherche de données

Une fois la connexion correctement établie, les données apparaissent dans l’espace de travail Log Analytics sous Syslog.

## <a name="validate-connectivity"></a>Valider la connectivité

Jusqu’à 20 minutes peuvent être nécessaires avant que vos journaux ne commencent à apparaître dans Log Analytics.

## <a name="next-steps"></a>Étapes suivantes

Dans ce document, vous avez appris à connecter Sophos XG Firewall à Azure Sentinel. Pour en savoir plus sur Azure Sentinel, voir les articles suivants :

- Découvrez comment [avoir une visibilité sur vos données et les menaces potentielles](quickstart-get-visibility.md).
- Prise en main de la [détection des menaces avec Azure Sentinel](tutorial-detect-threats-built-in.md).
- [Utilisez des classeurs](tutorial-monitor-your-data.md) pour superviser vos données.