---
title: Erreurs d’état du connecteur dans le tableau de bord d’ITSMC
description: En savoir plus sur les erreurs courantes qui existent dans le tableau de bord de Connecteur de gestion des services informatiques.
ms.topic: conceptual
author: nolavime
ms.author: nolavime
ms.date: 01/18/2021
ms.openlocfilehash: 5cc3c4a07cc698f3592a2ff2fd76e9f4bbef441b
ms.sourcegitcommit: f3ec73fb5f8de72fe483995bd4bbad9b74a9cc9f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "102036450"
---
# <a name="connector-status-errors-in-the-itsmc-dashboard"></a>Erreurs d’état du connecteur dans le tableau de bord d’ITSMC

Le tableau de bord de Connecteur de gestion des services informatiques (ITSMC) présente des erreurs qui peuvent vous aider à corriger des problèmes dans votre connecteur.

Les sections suivantes décrivent les erreurs courantes qui apparaissent dans la section du tableau de bord relative à l’état des connecteurs et la manière dont vous pouvez les résoudre.

## <a name="unexpected-response"></a>Réponse inattendue

**Erreur** : « Réponse inattendue de ServiceNow avec le code d’état de réussite. Response: { "import_set": "{import_set_id}", "staging_table": "x_mioms_microsoft_oms_incident", "result": [ { "transform_map": "OMS Incident", "table": "incident", "status": "error", "error_message": "{enregistrement cible introuvable|Table non valide|Table intermédiaire non valide" }"

**Cause** : ServiceNow retourne cette erreur dans les cas suivants :

* Un script personnalisé déployé dans une instance de ServiceNow a pour effet que des incidents sont ignorés.
* Le code de l’« application OMS Integrator » a été modifié côté ServiceNow (par exemple, via le script `onBefore`).

**Résolution** : Désactivez les scripts personnalisés ou les modifications de code.

## <a name="exception-update-failure"></a>Échec de la mise à jour des exceptions

**Erreur**: "{"erreur":{"message":"Échec de l’opération","détail":"Échec de la mise à jour de l’exception ACL en raison des contraintes de sécurité "}"

**Cause** : Les autorisations ServiceNow sont mal configurées.

**Résolution** : Vérifiez que tous les rôles sont correctement attribués comme [spécifié](itsmc-connections-servicenow.md#install-the-user-app-and-create-the-user-role).

## <a name="problem-sending-a-request"></a>Problème lors de l’envoi d’une demande

**Erreur** : « Une erreur s’est produite lors de l’envoi de la demande. »

**Cause** : Une instance de ServiceNow n’est pas disponible.

**Résolution** : Vérifiez votre instance dans ServiceNow. Elle est peut-être supprimée ou non disponible.

## <a name="servicenow-rate-problem"></a>Problème de débit de ServiceNow

**Erreur** : « ServiceDeskHttpBadRequestException: StatusCode=429 »

**Cause** : Les limites de débit de ServiceNow sont trop élevées ou trop basses.

**Résolution** : Augmentez ou annulez les limites de débit dans l’instance de ServiceNow comme expliqué dans la [documentation de ServiceNow](https://docs.servicenow.com/bundle/london-application-development/page/integrate/inbound-rest/task/investigate-rate-limit-violations.html).

## <a name="invalid-refresh-token"></a>Jeton d’actualisation non valide

**Erreur** : 
  * « AccessToken et RefreshToken non valides. L’utilisateur doit s’authentifier à nouveau. »
  * « Impossible de synchroniser la configuration des modèles pour les événements, alertes et incidents. Pour plus d’informations, consultez le message d’exception. »

**Cause** : Un jeton d’actualisation a expiré.

**Résolution** : Synchronisez ITSMC pour générer un nouveau jeton d’actualisation, comme expliqué dans [Comment corriger manuellement les problèmes de synchronisation](./itsmc-resync-servicenow.md).

## <a name="missing-connector"></a>Connecteur manquant

**Erreur** : « Impossible de créer/mettre à jour l’élément de travail pour l’alerte {alertName}. Le connecteur ITSM {connectionIdentifier} n’existe pas ou a été supprimé. »

**Cause** : ITSMC a été supprimé.

**Résolution** : ITSMC a été supprimé, mais les groupes d’actions Gestion des services informatiques (ITSM) définis y sont toujours associés. Il existe trois options pour résoudre ce problème :

* Recherchez, puis désactivez ou supprimez ces groupes d’actions.
* [Reconfigurez les groupes d’actions](./itsmc-definition.md#create-itsm-work-items-from-azure-alerts) pour utiliser une instance d’ITSMC existante.
* [Créez une nouvelle instance d’ITSMC](./itsmc-definition.md#create-an-itsm-connection) et [reconfigurez les groupes d’actions pour l’utiliser](itsmc-definition.md#create-itsm-work-items-from-azure-alerts).

## <a name="lack-of-connection-details"></a>Absence d’informations de connexion

**Erreur**: « Un problème est survenu. Impossible d’accéder aux détails de la connexion. » Cette erreur apparaît lorsque vous définissez un groupe d’actions ITSM.

**Cause** : Une telle erreur s’affiche dans l’une ou l’autre des situations suivantes :

* Une instance de connecteur ITSM nouvellement créée n’a pas encore terminé la synchronisation initiale.
* Le connecteur n’a pas été correctement défini.

**Résolution** : 

* Quand une nouvelle instance d’ITSMC est créée, elle démarre la synchronisation des informations à partir du système ITSM, telles que des modèles d’élément de travail et des éléments de travail. [Synchronisez ITSMC pour générer un nouveau jeton d’actualisation](./itsmc-resync-servicenow.md).
* [Passez en revue les détails de votre connexion dans ITSMC](./itsmc-connections-servicenow.md#create-a-connection) et vérifiez qu’ITSMC peut [se synchroniser](./itsmc-resync-servicenow.md).
