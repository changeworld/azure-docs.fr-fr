---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 03/18/2020
ms.author: glenga
ms.openlocfilehash: 9d5bae1aedbd031a0a3c08ba5141aebc22f1c674
ms.sourcegitcommit: 740698a63c485390ebdd5e58bc41929ec0e4ed2d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99493377"
---
À présent, vous pouvez utiliser le nouveau paramètre `msg` pour écrire dans la liaison de sortie à partir de votre code de fonction. Ajoutez la ligne de code suivante avant la réponse de réussite pour ajouter la valeur de `name` à la liaison de sortie `msg`.

:::code language="java" source="~/functions-quickstart-java/functions-add-output-binding-storage-queue/src/main/java/com/function/Function.java" range="34":::

Lorsque vous utilisez une liaison de sortie, vous n’avez pas besoin de recourir au code du Kit de développement logiciel (SDK) Stockage Azure pour l’authentification, l’obtention d’une référence de file d’attente ou l’écriture de données. La liaison de sortie de file d’attente et le runtime Functions effectuent ces tâches.

Votre méthode `run` doit maintenant ressembler à l’exemple suivant :

:::code language="java" source="~/functions-quickstart-java/functions-add-output-binding-storage-queue/src/main/java/com/function/Function.java" range="16-38":::