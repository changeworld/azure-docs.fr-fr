---
title: Utiliser les Watchlists Azure Sentinel
description: Cet article explique comment utiliser les Watchlists Azure Sentinel, examiner les menaces, importer des données métiers, créer des listes d’autorisation et enrichir les données d’événement.
services: sentinel
author: yelevin
ms.author: yelevin
ms.assetid: 1721d0da-c91e-4c96-82de-5c7458df566b
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.topic: conceptual
ms.custom: mvc
ms.date: 09/06/2020
ms.openlocfilehash: 97509b878fb5e0cb28bddc5d1b58c21b32c34675
ms.sourcegitcommit: f82e290076298b25a85e979a101753f9f16b720c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/04/2021
ms.locfileid: "99555639"
---
# <a name="use-azure-sentinel-watchlists"></a>Utiliser les Watchlists Azure Sentinel

> [!IMPORTANT]
> La fonctionnalité Watchlists est actuellement en **PRÉVERSION**. Consultez l’[Avenant aux conditions d’utilisation pour les préversions de Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) pour connaître les conditions juridiques supplémentaires s’appliquant aux fonctionnalités Azure sont en version bêta, en préversion ou non encore en disponibilité générale.

Les Watchlists Azure Sentinel activent la collecte de données à partir de sources de données externes pour la corrélation avec les événements dans votre environnement Azure Sentinel. Une fois créées, vous pouvez utiliser les Watchlists dans vos playbooks de recherche, de détection, de recherche de menace et de réponse. Les Watchlists sont stockées dans votre espace de travail Azure Sentinel en tant que paires nom-valeur et sont mis en cache pour des performances de requête optimales et une faible latence.

Les scénarios courants pour l’utilisation des Watchlists sont notamment les suivants :

- **L’examen des menaces** et la réponse rapide aux incidents avec l’importation rapide d’adresses IP, de hachages de fichiers et d’autres données à partir de fichiers CSV. Une fois importées, vous pouvez utiliser des paires nom-valeur de Watchlist pour les jointures et les filtres dans les règles d’alerte, la recherche de menaces, les classeurs, les notebook et les requêtes générales.

- **Importation de données métier** en tant que Watchlist. Par exemple, importez des listes d’utilisateurs avec un accès privilégié au système, ou des employés arrêtés, puis utilisez la Watchlist pour créer des listes d’autorisation et de refus utilisées pour détecter ou empêcher ces utilisateurs de se connecter au réseau.

- **Réduction de fatigue des alertes**. Créer des listes d’autorisation pour supprimer des alertes d’un groupe d’utilisateurs, tels que les utilisateurs d’adresses IP autorisées qui effectuent des tâches qui déclencheraient normalement l’alerte, et empêchent les événements bénins de devenir des alertes.

- **Enrichissement des données d'événement**. Utilisez les Watchlists pour enrichir vos données d’événement avec des combinaisons nom-valeur dérivées de sources de données externes.

## <a name="create-a-new-watchlist"></a>Création d’une nouvelle Watchlist

1. À partir du Portail Azure, accédez à **Azure Sentinel** > **Configuration** > **Watchlist**, puis sélectionnez **Ajouter une nouvelle**.

    > [!div class="mx-imgBorder"]
    > ![nouvelle Watchlist](./media/watchlists/sentinel-watchlist-new.png)

1. Dans la page **Général**, indiquez le nom, la description et l’alias de la Watchlist, puis sélectionnez **Suivant**.

    > [!div class="mx-imgBorder"]
    > ![page général de la Watchlist](./media/watchlists/sentinel-watchlist-general.png)

1. Dans la page **Source**, sélectionnez le type de jeu de données, chargez un fichier, puis sélectionnez **Suivant**.

    :::image type="content" source="./media/watchlists/sentinel-watchlist-source.png" alt-text="page source de la Watchlist" lightbox="./media/watchlists/sentinel-watchlist-source.png":::

    > [!NOTE]
    >
    > Les chargements de fichiers sont actuellement limités à des fichiers d’une taille maximale de 3,8 Mo.

1. Passez en revue les informations, vérifiez qu’elles sont correctes, puis sélectionnez **Créer**.

    > [!div class="mx-imgBorder"]
    > ![page de vérification de la Watchlist](./media/watchlists/sentinel-watchlist-review.png)

    Une notification s’affiche une fois que la Watchlist est créée.

    :::image type="content" source="./media/watchlists/sentinel-watchlist-complete.png" alt-text="notification de création réussie de la Watchlist" lightbox="./media/watchlists/sentinel-watchlist-complete.png":::

## <a name="use-watchlists-in-queries"></a>Utilisation des Watchlists dans les requêtes

1. Dans le Portail Azure, accédez à **Azure Sentinel** > **Configuration** > **Watchlist**, sélectionnez la Watchlist que vous voulez utiliser, puis sélectionnez **Afficher dans Log Analytics**.

    :::image type="content" source="./media/watchlists/sentinel-watchlist-queries-list.png" alt-text="utilisation des Watchlists dans les requêtes" lightbox="./media/watchlists/sentinel-watchlist-queries-list.png":::

1. Les éléments de votre Watchlist sont automatiquement extraits pour votre requête et s’affichent sous l’onglet **Résultats**. L’exemple ci-dessous montre les résultats de l’extraction des champs **ServerName** et **IpAddress**.

    > [!NOTE]
    > Le timestamp de vos requêtes sera ignoré à la fois dans l’interface utilisateur de la requête et dans les alertes planifiées.

    :::image type="content" source="./media/watchlists/sentinel-watchlist-queries-fields.png" alt-text="requêtes avec les champs de la Watchlist" lightbox="./media/watchlists/sentinel-watchlist-queries-fields.png":::
    
1. Vous pouvez comparer les données de n’importe quelle table avec celles d’une Watchlist en traitant la Watchlist comme une table pour les jointures et les recherches.

    ```kusto
    Heartbeat
    | lookup kind=leftouter _GetWatchlist('IPlist') 
     on $left.ComputerIP == $right.IPAddress
    ```
    :::image type="content" source="./media/watchlists/sentinel-watchlist-queries-join.png" alt-text="requêtes par rapport à la Watchlist en tant que recherche":::

## <a name="use-watchlists-in-analytics-rules"></a>Utilisation des Watchlists dans les règles d’analyse

Pour utiliser des Watchlists dans les règles d’analyse, à partir du Portail Azure, accédez à **Azure Sentinel** > **Configuration** > **Analytics**, puis créez une règle à l’aide de la fonction `_GetWatchlist('<watchlist>')` de la requête.

1. Dans cet exemple, créez une Watchlist appelée « ipwatchlist » avec les valeurs suivantes :

    :::image type="content" source="./media/watchlists/create-watchlist.png" alt-text="liste de quatre éléments pour Watchlist":::

    :::image type="content" source="./media/watchlists/sentinel-watchlist-new-2.png" alt-text="créer une Watchlist avec quatre éléments":::

1. Ensuite, créez la règle d’analyse.  Dans cet exemple, nous incluons uniquement les événements des adresses IP figurant dans la Watchlist :

    ```kusto
    //Watchlist as a variable
    let watchlist = (_GetWatchlist('ipwatchlist') | project IPAddress);
    Heartbeat
    | where ComputerIP in (watchlist)
    ```
    ```kusto
    //Watchlist inline with the query
    Heartbeat
    | where ComputerIP in ( 
        (_GetWatchlist('ipwatchlist')
        | project IPAddress)
    )
    ```

:::image type="content" source="./media/watchlists/sentinel-watchlist-analytics-rule-2.png" alt-text="utilisation des Watchlists dans les règles d’analyse":::

## <a name="view-list-of-watchlists-aliases"></a>Afficher la liste des alias de Watchlists

Pour obtenir un liste d’alias de Watchlist, à partir du Portail Azure, accédez à **Azure Sentinel** > **Général** > **Journaux**, puis exécutez la requête suivante : `_GetWatchlistAlias`. Vous pouvez voir la liste des alias dans l’onglet **Résultats**.

> [!div class="mx-imgBorder"]
> ![liste de Watchlists](./media/watchlists/sentinel-watchlist-alias.png)

## <a name="next-steps"></a>Étapes suivantes
Dans ce document, vous avez appris à utiliser les Watchlists dans Azure Sentinel pour enrichir les données et améliorer les investigations. Pour en savoir plus sur Azure Sentinel, voir les articles suivants :
- Découvrez comment [avoir une visibilité sur vos données et les menaces potentielles](quickstart-get-visibility.md).
- Prise en main de la [détection des menaces avec Azure Sentinel](./tutorial-detect-threats-built-in.md).
- [Utilisez des classeurs](tutorial-monitor-your-data.md) pour superviser vos données.
