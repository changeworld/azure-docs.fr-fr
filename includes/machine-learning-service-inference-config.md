---
author: Blackmist
ms.service: machine-learning
ms.topic: include
ms.date: 01/28/2020
ms.author: larryfr
ms.openlocfilehash: a03f71adc99063fee4374b1436b08adf5bab783d
ms.sourcegitcommit: 15d27661c1c03bf84d3974a675c7bd11a0e086e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/09/2021
ms.locfileid: "102510985"
---
Les entrées du mappage de document `inferenceconfig.json` correspondent aux paramètres de la classe [InferenceConfig](/python/api/azureml-core/azureml.core.model.inferenceconfig). Le tableau suivant décrit le mappage entre les entités dans le document JSON et les paramètres de la méthode :

| Entité JSON | Paramètre de méthode | Description |
| ----- | ----- | ----- |
| `entryScript` | `entry_script` | Chemin vers un fichier local contenant le code à exécuter pour l’image. |
| `sourceDirectory` | `source_directory` | Facultatif. Chemin vers des dossiers contenant tous les fichiers pour créer l’image, ce qui facilite l’accès à tous les fichiers de ce dossier ou sous-dossier. Vous pouvez charger un dossier entier à partir de votre ordinateur local en tant que dépendances pour le service web. Remarque : vos chemins d'accès entry_script, conda_file et extra_docker_file_steps sont des chemins d'accès relatifs au chemin source_directory. |
| `environment` | `environment` | Facultatif.  [Environnement](/python/api/azureml-core/azureml.core.environment.environment) Azure Machine Learning.|

Vous pouvez inclure les spécifications complètes d’un [environnement](/python/api/azureml-core/azureml.core.environment.environment) Azure Machine Learning dans le fichier de configuration d’inférence. Si cet environnement n’existe pas dans votre espace de travail, Azure Machine Learning le crée. Dans le cas contraire, Azure Machine Learning met à jour l’environnement, si nécessaire. L’extrait JSON ci-dessous est un exemple :

```json
{
    "entryScript": "score.py",
    "environment": {
        "docker": {
            "arguments": [],
            "baseDockerfile": null,
            "baseImage": "mcr.microsoft.com/azureml/base:intelmpi2018.3-ubuntu16.04",
            "enabled": false,
            "sharedVolumes": true,
            "shmSize": null
        },
        "environmentVariables": {
            "EXAMPLE_ENV_VAR": "EXAMPLE_VALUE"
        },
        "name": "my-deploy-env",
        "python": {
            "baseCondaEnvironment": null,
            "condaDependencies": {
                "channels": [
                    "conda-forge"
                ],
                "dependencies": [
                    "python=3.6.2",
                    {
                        "pip": [
                            "azureml-defaults",
                            "azureml-telemetry",
                            "scikit-learn==0.22.1",
                            "inference-schema[numpy-support]"
                        ]
                    }
                ],
                "name": "project_environment"
            },
            "condaDependenciesFile": null,
            "interpreterPath": "python",
            "userManagedDependencies": false
        },
        "version": "1"
    }
}
```

Vous pouvez également utiliser un environnement Azure Machine Learning [existant](/python/api/azureml-core/azureml.core.environment.environment) dans des paramètres CLI distincts et supprimer la clé d'environnement du fichier de configuration d’inférence. Utilisez -e pour le nom de l’environnement, et --ev pour la version de l’environnement. À défaut d'indiquer --ev, la version la plus récente est utilisée. L'exemple suivant illustre un fichier de configuration d'inférence :

```json
{
    "entryScript": "score.py",
    "sourceDirectory": null
}
```

La commande suivante montre comment déployer un modèle à l’aide du fichier de configuration d’inférence précédent (nommé myInferenceConfig.json). 

Elle utilise également la version la plus récente d’un environnement Azure Machine Learning [existant](/python/api/azureml-core/azureml.core.environment.environment) (nommé AzureML-Minimal).

```azurecli-interactive
az ml model deploy -m mymodel:1 --ic myInferenceConfig.json -e AzureML-Minimal --dc deploymentconfig.json
```