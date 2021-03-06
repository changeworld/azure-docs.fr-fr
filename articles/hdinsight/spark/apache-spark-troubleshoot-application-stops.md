---
title: L’application de streaming Apache Spark s’arrête au bout de 24 jours dans Azure HDInsight
description: Une application de diffusion en continu Apache Spark s’arrête après 24 jours d'exécution sans erreurs dans les fichiers journaux.
ms.service: hdinsight
ms.topic: troubleshooting
ms.date: 07/29/2019
ms.openlocfilehash: b702cbf915e4991df4c202564677ea7e0a02f9c4
ms.sourcegitcommit: 2f9f306fa5224595fa5f8ec6af498a0df4de08a8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2021
ms.locfileid: "98929467"
---
# <a name="scenario-apache-spark-streaming-application-stops-after-executing-for-24-days-in-azure-hdinsight"></a>Scénario : L’application de diffusion en continu Apache Spark s’arrête après 24 jours d'exécution dans Azure HDInsight

Cet article décrit la procédure à suivre pour résoudre les problèmes rencontrés lors de l’utilisation de composants Apache Spark dans des clusters Azure HDInsight.

## <a name="issue"></a>Problème

Une application de diffusion en continu Apache Spark s’arrête après 24 jours d'exécution sans erreurs dans les fichiers journaux.

## <a name="cause"></a>Cause

La valeur `livy.server.session.timeout` contrôle le laps de temps durant lequel Apache Livy doit attendre la fin d’une session. Une fois la valeur `session.timeout` atteinte, la session Livy et l'application sont automatiquement supprimées.

## <a name="resolution"></a>Résolution

Pour les travaux de longue durée, augmentez la valeur de `livy.server.session.timeout` à l’aide de l’interface utilisateur Ambari. Vous pouvez accéder à la configuration Livy à partir de l’interface utilisateur Ambari en utilisant l’URL `https://<yourclustername>.azurehdinsight.net/#/main/services/LIVY/configs`.

Remplacez `<yourclustername>` par le nom de votre cluster HDInsight tel qu'indiqué dans le portail.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [troubleshooting next steps](../../../includes/hdinsight-troubleshooting-next-steps.md)]