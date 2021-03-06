---
title: Connecter des fonctions à d’autres services Azure
description: Découvrez comment ajouter des liaisons qui se connectent à d’autres services Azure à une fonction existante dans votre projet Azure Functions.
ms.topic: how-to
ms.date: 04/29/2020
ms.openlocfilehash: d1c6f5bb8ca5fcf995b8a8d326abbec96f1d2e35
ms.sourcegitcommit: d49bd223e44ade094264b4c58f7192a57729bada
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99258199"
---
# <a name="connect-functions-to-azure-services-using-bindings"></a>Connecter des fonctions à des services Azure à l’aide de liaisons

Lorsque vous créez une fonction, un code déclencheur spécifique à une langue est ajouté à votre projet à partir d’un ensemble de modèles de déclencheurs. Si vous souhaitez connecter votre fonction à d’autres services à l’aide de liaisons d’entrée ou de sortie, vous devez ajouter des définitions de liaison spécifiques à votre fonction. Pour en savoir plus sur les liaisons, consultez [Concepts des déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md).

## <a name="local-development"></a>Développement local       

Lorsque vous développez des fonctions localement, vous devez mettre à jour le code de fonction pour ajouter des liaisons. L’utilisation de Visual Studio Code peut faciliter l’ajout de liaisons à une fonction.  

### <a name="visual-studio-code"></a>Visual Studio Code

Lorsque vous utilisez Visual Studio Code pour développer votre fonction et que votre fonction utilise un fichier function.json, l’extension Azure Functions peut ajouter automatiquement une liaison à un fichier function.json existant. Pour en savoir plus, consultez [Ajouter des liaisons d’entrée et de sortie](functions-develop-vs-code.md#add-input-and-output-bindings).   

### <a name="manually-add-bindings-based-on-examples"></a>Ajouter manuellement des liaisons basées sur des exemples

Lorsque vous ajoutez une liaison à une fonction existante, vous devez mettre à jour le code de la fonction et le fichier de configuration function.json, s’ils sont utilisés par votre langage. La bibliothèque de classes .NET et les fonctions Java utilisent des attributs au lieu de function.json. Vous devrez donc plutôt la mettre à jour.

Utilisez le tableau suivant pour rechercher des exemples de types de liaison spécifiques que vous pouvez utiliser pour vous guider dans la mise à jour d’une fonction existante. Tout d’abord, choisissez l’onglet du langage qui correspond à votre projet. 

[!INCLUDE [functions-bindings-code-example-chooser](../../includes/functions-bindings-code-example-chooser.md)]

## <a name="azure-portal"></a>Portail Azure

Lorsque vous développez vos fonctions dans le [portail Azure](https://portal.azure.com), vous ajoutez des liaisons d’entrée et de sortie sous l’onglet **intégrer** pour une fonction donnée. Les nouvelles liaisons sont ajoutées au fichier function.json ou aux attributs de la méthode, en fonction de votre langage. Les articles suivants présentent des exemples d’ajout de liaisons à une fonction existante sur le portail :

+ [Liaison de sortie de stockage de file d’attente](functions-integrate-storage-queue-output-binding.md)
+ [Liaison de sortie Azure Cosmos DB](functions-integrate-store-unstructured-data-cosmosdb.md)

## <a name="next-steps"></a>Étapes suivantes

+ [Concepts des déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md)
