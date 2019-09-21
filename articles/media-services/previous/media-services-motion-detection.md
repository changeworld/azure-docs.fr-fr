---
title: Détecter les mouvements avec Azure Media Analytics | Microsoft Docs
description: Le processeur multimédia Azure Media Motion Detector vous permet d’identifier efficacement les passages intéressants dans une vidéo qui, autrement, serait longue et monotone.
services: media-services
documentationcenter: ''
author: juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/19/2019
ms.author: juliako
ms.reviewer: milanga
ms.openlocfilehash: c053e4dfc38fc0f055ec91a6622ef7f767c13a86
ms.sourcegitcommit: a6873b710ca07eb956d45596d4ec2c1d5dc57353
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/16/2019
ms.locfileid: "69015335"
---
# <a name="detect-motions-with-azure-media-analytics"></a>Détecter les mouvements avec Azure Media Analytics
## <a name="overview"></a>Vue d'ensemble
Le processeur multimédia **Azure Media Motion Detector** vous permet d’identifier efficacement les passages intéressants dans une vidéo qui, autrement, serait longue et monotone. La détection de mouvement peut être utilisée sur des séquences d’une caméra fixe pour identifier les passages de la vidéo où un mouvement se produit. Elle génère un fichier JSON contenant des métadonnées avec des horodateurs et le cadre de limitation de la vidéo où s’est produit l’événement.

Ciblant les vidéos de surveillance, cette technologie est en mesure de classer les mouvements en événements pertinents et en faux positifs, tels que les ombres et les variations d’éclairage. Cela vous permet de générer des alertes de sécurité à partir de séquences vidéo sans perdre de temps avec d’innombrables faux positifs, et tout en accédant rapidement aux moments clés dans des vidéos de surveillance longues.

Le processeur multimédia **Azure Media Motion Detector** est uniquement disponible en version préliminaire.

Cet article fournit des informations détaillées sur **Azure Media Motion Detector** et illustre son utilisation avec le SDK Media Services pour .NET

## <a name="motion-detector-input-files"></a>Fichiers d’entrée du détecteur de mouvement
Fichiers vidéo. Actuellement, les formats suivants sont pris en charge : MP4, MOV et WMV.

## <a name="task-configuration-preset"></a>Configuration de la tâche (préconfiguration)
Lors de la création d’une tâche de vidéo **Azure Media Motion Detector**, vous devez spécifier une présélection de configuration. 

### <a name="parameters"></a>parameters
Vous pouvez utiliser les paramètres suivants :

| Nom | Options | Description | Default |
| --- | --- | --- | --- |
| sensitivityLevel |String : « low », « medium », « high » |Définit le niveau de sensibilité auquel les mouvements sont signalés. Réglez cette option pour ajuster le nombre de faux positifs. |« medium » |
| frameSamplingValue |Entier positif |Définit la fréquence d’exécution de l’algorithme. 1 = chaque trame, 2 = toutes les 2 trames, etc. |1 |
| detectLightChange |Boolean : « True », « False » |Définit si des changements d’éclairage sont signalés dans les résultats. |« False » |
| mergeTimeThreshold |Xs-time : hh:mm:ss<br/>Exemple : 00:00:03 |Spécifie la fenêtre de temps entre les événements de mouvement lorsque 2 événements sont combinés et signalés comme 1. |00:00:00 |
| detectionZones |Tableau de zones de détection :<br/>- Zone de détection est un tableau de 3 points ou plus<br/>- Point est une coordonnée x et y de 0 à 1. |Décrit la liste des zones de détection polygonale à utiliser.<br/>Les résultats sont signalés avec les zones en tant qu’ID, la première étant « id » :0 |Zone unique, couvrant la trame entière. |

### <a name="json-example"></a>Exemple JSON

```json
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }
```

## <a name="motion-detector-output-files"></a>Fichiers de sortie du détecteur de mouvement
Une tâche de détection de mouvement renvoie un fichier JSON dans l’élément multimédia de sortie qui décrit les alertes de mouvement et leurs catégories dans la vidéo. Le fichier contient des informations sur l’heure et la durée du mouvement détecté dans la vidéo.

L’API de détecteur de mouvement indique lorsqu’un mouvement a été détecté dans une vidéo d’arrière-plan fixe (par exemple, une vidéo de surveillance). Le détecteur de mouvement est optimisé pour réduire au minimum les fausses alertes, telles que les ombres et les variations d’éclairage. Les limitations actuelles des algorithmes incluent les vidéos en vision nocturne, les objets semi-transparents et les petits objets.

### <a id="output_elements"></a>Éléments du fichier de sortie JSON
> [!NOTE]
> Dans la dernière version, le format de sortie JSON a été modifié et peut représenter une rupture pour certains clients.
> 
> 

Le tableau suivant décrit les éléments du fichier de sortie JSON.

| Élément | Description |
| --- | --- |
| version |Cela vaut pour la version de l’API vidéo. La version actuelle est 2. |
| timescale |« Cycles » par seconde de la vidéo. |
| offset |Le décalage des horodatages en « cycles ». Cette valeur sera toujours 0 dans la version 1.0 des API vidéo. Cette valeur est susceptible d’être modifiée dans les scénarios pris en charge ultérieurement. |
| taux de trames |Images par seconde de la vidéo. |
| largeur, hauteur |Fait référence à la largeur et à la hauteur de la vidéo en pixels. |
| start |L’horodatage de début en « cycles ». |
| duration |La durée de l’événement en « cycles ». |
| interval |L’intervalle de chaque entrée dans l’événement en « cycles ». |
| événements |Chaque fragment d’événement contient le mouvement détecté pendant cette durée. |
| Type |Dans la version actuelle, cette valeur est toujours de « 2 » pour le mouvement générique. Ce libellé permet aux API vidéo de classer le mouvement dans les versions ultérieures. |
| regionId |Comme expliqué ci-dessus, cette valeur sera toujours « 0 » dans la présente version. Ce libellé permet aux API vidéo de détecter du mouvement dans différentes régions dans les versions ultérieures. |
| regions |Fait référence à la zone dans la vidéo où un mouvement est susceptible de vous intéresser. <br/><br/>-« id » représente la zone de la région ; dans cette version, la seule valeur existante est ID 0. <br/>-« type » représente la forme de la région où un mouvement est susceptible de vous intéresser. Pour l’instant, seules « rectangle » et « polygone » sont prises en charge.<br/> Si vous avez indiqué « rectangle », les dimensions de la région sont X, Y, Width et Height. Les coordonnées X et Y représentent les coordonnées XY de l’angle supérieur gauche de la région sur une échelle normalisée de 0,0 à 1,0. La largeur et la hauteur représentent la taille de la région sur une échelle normalisée de 0,0 à 1,0. Dans la version actuelle, X, Y, Width et Height sont toujours fixés à 0, 0 et 1, 1. <br/>Si vous avez indiqué « polygone », les dimensions de la région sont en points. <br/> |
| fragments |Les métadonnées sont mémorisées dans différents segments appelés fragments. Chaque fragment contient des valeurs de début (start), de durée (duration), un numéro d’intervalle et des événements (event). Un fragment sans aucun événement signifie qu’aucun mouvement n’a été détecté pendant cette heure de début et la durée. |
| crochets [] |Chaque crochet représente un intervalle dans l’événement. Les crochets vides pour cet intervalle signifient qu’aucun mouvement n’a été détecté. |
| emplacements |Cette nouvelle entrée sous les événements répertorie l’emplacement dans lequel le mouvement s’est produit. Cette entrée est plus précise que les zones de détection. |

L’exemple JSON ci-après illustre la sortie obtenue :

```json
    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],
```

## <a name="limitations"></a>Limites
* Les formats de fichier vidéo d’entrée pris en charge incluent WMV, MOV et MP4.
* La détection de mouvement est optimisée pour les vidéos dont l’arrière-plan est fixe. L’algorithme est axé sur la réduction des fausses alertes, telles que les variations d’éclairage et les ombres.
* Certains mouvements peuvent ne pas être détectés en raison de défis techniques ; par exemple, des vidéos en vision nocturne, les objets semi-transparents et les petits objets.

## <a name="net-sample-code"></a>Exemple de code .NET

Le programme suivant montre comment effectuer les tâches suivantes :

1. Créer un élément multimédia et charger un fichier multimédia dans l’élément multimédia.
2. Créer un travail avec une tâche de détection du mouvement vidéo basée sur un fichier de configuration qui contient la présélection json suivante : 
   
    ```json
            {
            "Version": "1.0",
            "Options": {
                "SensitivityLevel": "medium",
                "FrameSamplingValue": 1,
                "DetectLightChange": "False",
                "MergeTimeThreshold":
                "00:00:02",
                "DetectionZones": [
                [
                    {"x": 0, "y": 0},
                    {"x": 0.5, "y": 0},
                    {"x": 0, "y": 1}
                ],
                [
                    {"x": 0.3, "y": 0.3},
                    {"x": 0.55, "y": 0.3},
                    {"x": 0.8, "y": 0.3},
                    {"x": 0.8, "y": 0.55},
                    {"x": 0.8, "y": 0.8},
                    {"x": 0.55, "y": 0.8},
                    {"x": 0.3, "y": 0.8},
                    {"x": 0.3, "y": 0.55}
                ]
                ]
            }
            }
    ```

3. Télécharger les fichiers JSON de sortie. 

#### <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Exemples

```csharp

using System;
using System.Configuration;
using System.IO;
using System.Linq;
using Microsoft.WindowsAzure.MediaServices.Client;
using System.Threading;
using System.Threading.Tasks;

namespace VideoMotionDetection
{
    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AMSAADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];
        private static readonly string _AMSClientId =
            ConfigurationManager.AppSettings["AMSClientId"];
        private static readonly string _AMSClientSecret =
            ConfigurationManager.AppSettings["AMSClientSecret"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            AzureAdTokenCredentials tokenCredentials =
                new AzureAdTokenCredentials(_AADTenantDomain,
                    new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                    AzureEnvironments.AzureCloudEnvironment);

            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Run the VideoMotionDetection job.
            var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                        @"C:\supportFiles\VideoMotionDetection\config.json");

            // Download the job output asset.
            DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
        }

        static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload the input media file to storage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                "My Video Motion Detection Input Asset",
                AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Video Motion Detection Job");

            // Get a reference to Azure Media Motion Detector.
            string MediaProcessorName = "Azure Media Motion Detector";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from the specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify the input asset.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("My Video Motion Detection Output Asset", AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, the event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                Console.WriteLine(string.Format("Error: {0}. {1}",
                                                error.Code,
                                                error.Message));
                return null;
            }

            return job.OutputMediaAssets[0];
        }

        static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
        {
            IAsset asset = _context.Assets.Create(assetName, options);

            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);

            return asset;
        }

        static void DownloadAsset(IAsset asset, string outputDirectory)
        {
            foreach (IAssetFile file in asset.AssetFiles)
            {
                file.Download(Path.Combine(outputDirectory, file.Name));
            }
        }

        static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors
                .Where(p => p.Name == mediaProcessorName)
                .ToList()
                .OrderBy(p => new Version(p.Version))
                .LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor",
                                                           mediaProcessorName));

            return processor;
        }

        static private void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("Job is finished.");
                    Console.WriteLine();
                    break;
                case JobState.Canceling:
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    Console.WriteLine("Please wait...\n");
                    break;
                case JobState.Canceled:
                case JobState.Error:
                    // Cast sender as a job.
                    IJob job = (IJob)sender;
                    // Display or log error details as needed.
                    // LogJobStop(job.Id);
                    break;
                default:
                    break;
            }
        }
    }
}
```

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Liens connexes
[Blog Azure Media Services Motion Detector](https://azure.microsoft.com/blog/motion-detector-update/)

[Vue d’ensemble d’Azure Media Services Analytics](media-services-analytics-overview.md)

[Démonstrations Azure Media Analytics](https://azuremedialabs.azurewebsites.net/demos/Analytics.html)

