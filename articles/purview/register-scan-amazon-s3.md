---
title: Guide pratique pour analyser des compartiments Amazon S3
description: Ce guide pratique explique en détail comment analyser des compartiments Amazon S3.
author: batamig
ms.author: bagol
ms.service: purview
ms.subservice: purview-data-catalog
ms.topic: how-to
ms.date: 03/07/2021
ms.custom: references_regions
ms.openlocfilehash: ddd5c5de85da5ae8cec9d24d33dfd2bf035b5b34
ms.sourcegitcommit: 5bbc00673bd5b86b1ab2b7a31a4b4b066087e8ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2021
ms.locfileid: "102438726"
---
# <a name="azure-purview-connector-for-amazon-s3"></a>Connecteur Azure Purview pour Amazon S3

Ce guide pratique explique comment utiliser Azure Purview pour analyser vos données non structurées actuellement stockées dans des compartiments Amazon S3 standard et découvrir les types d’informations sensibles qui existent dans vos données. Ce guide explique également comment identifier les compartiments Amazon S3 où les données sont actuellement stockées pour faciliter la protection des informations et la conformité des données.

Pour ce service, Purview vous permet de fournir un compte Microsoft avec un accès sécurisé à AWS, où doit s’exécuter le scanneur Purview. Le scanneur Purview utilise cet accès à vos compartiments Amazon S3 pour lire vos données, puis rapporte à Azure les résultats de l’analyse, qui comprennent seulement les métadonnées et la classification. Utilisez les rapports de classification et d’étiquetage Purview pour analyser et examiner vos résultats d’analyse de données.

Dans ce guide pratique, vous apprenez à ajouter des compartiments Amazon S3 sous forme de ressources Purview et à créer une analyse pour vos données Amazon S3.

## <a name="purview-scope-for-amazon-s3"></a>Étendue Purview pour Amazon S3

L’étendue suivante est spécifique pour inscrire et analyser des compartiments Amazon S3 comme sources de données Purview.

|Étendue  |Description  |
|---------|---------|
|**Limites de données**     |    Le service de scanneur Purview prend actuellement en charge l’analyse des compartiments Amazon S3 avec jusqu’à 100 Go de données par locataire.     |
|**Types de fichier**     | Le service de scanneur Purview prend actuellement en charge les types de fichiers suivants : <br><br>.avro, .csv, .doc, .docm, .docx, .dot, .json, .odp, .ods, .odt, .orc, .parquet, .pdf, .pot, .pps, .ppsx, .ppt, .pptm, .pptx, .psv, .ssv, .tsv, .txt, .xlc, .xls, .xlsb, .xlsm, .xlsx, .xlt, .xml        |
|**Régions**     | Le connecteur Purview pour le service Amazon S3 est actuellement déployé uniquement dans les régions **AWS USA Est (Ohio)** et **Europe (Francfort)** . <br><br>Pour plus d’informations, consultez [Régions de stockage et d’analyse](#storage-and-scanning-regions).   |
|     |         |

Pour plus d’informations, consultez les limites Purview documentées sur :

- [Gestion et augmentation des quotas de ressources avec Azure Purview](how-to-manage-quotas.md)
- [Sources de données et types de fichiers pris en charge dans Azure Purview](sources-and-scans.md)
### <a name="storage-and-scanning-regions"></a>Régions de stockage et d’analyse

Le tableau suivant mappe les régions où sont stockées vos données à la région où elles doivent être analysées par Azure Purview.

> [!IMPORTANT]
> Les clients sont facturés de tous les frais de transfert de données associés en fonction de la région de leur compartiment.
>

| Région de stockage | Région d’analyse |
| ------------------------------- | ------------------------------------- |
| USA Est (Ohio)                  | USA Est (Ohio)                        |
| USA Est (Virginie Nord)           | USA Est (Ohio)                        |
| USA Ouest (Californie Nord)         | USA Est (Ohio)                        |
| USA Ouest (Oregon)                | USA Est (Ohio)                        |
| Afrique (Le Cap)              | Europe (Francfort)                    |
| Asie-Pacifique (Hong Kong)        | Europe (Francfort)                    |
| Asie-Pacifique (Mumbai)           | Europe (Francfort)                    |
| Asie-Pacifique (Osaka-local)      | Europe (Francfort)                    |
| Asie-Pacifique (Séoul)            | Europe (Francfort)                    |
| Asie-Pacifique (Singapour)        | Europe (Francfort)                    |
| Asie-Pacifique (Sydney)           | Europe (Francfort)                    |
| Asie-Pacifique (Tokyo)            | Europe (Francfort)                    |
| Canada (Centre)                | USA Est (Ohio)                        |
| Chine (Beijing)                 | Non pris en charge                    |
| Chine (Ningxia)                 | Non pris en charge                   |
| Europe (Francfort)              | Europe (Francfort)                    |
| Europe (Irlande)                | Europe (Francfort)                    |
| Europe (Londres)                 | Europe (Francfort)                    |
| Europe (Milan)                  | Europe (Francfort)                    |
| Europe (Paris)                  | Europe (Francfort)                    |
| Europe (Stockholm)              | Europe (Francfort)                    |
| Moyen-Orient (Bahreïn)           | Europe (Francfort)                    |
| Amérique du Sud (São Paulo)       | USA Est (Ohio)                        |
| | |
## <a name="prerequisites"></a>Prérequis

Vérifiez que vous avez exécuté les prérequis suivants avant d’ajouter vos compartiments Amazon S3 comme sources de données Purview et d’analyser vos données S3.

- Vous devez être administrateur de la source de données Azure Purview.

- Quand vous ajoutez vos compartiments comme ressources Purview, vous avez besoin des valeurs de votre [ARN AWS](#retrieve-your-new-role-arn), de votre [nom de compartiment](#retrieve-your-amazon-s3-bucket-name) et, parfois, de votre [ID de compte AWS](#locate-your-aws-account-id).

### <a name="create-a-purview-account"></a>Créer un compte Purview

- **Si vous avez déjà un compte Purview,** vous pouvez passer aux configurations nécessaires pour la prise en charge d’AWS S3. Commencez par [Créer des informations d’identification Purview pour votre analyse de compartiment AWS](#create-a-purview-credential-for-your-aws-bucket-scan).

- **Si vous devez créer un compte Purview,** suivez les instructions de la section [Créer une instance de compte Azure Purview](create-catalog-portal.md). Une fois votre compte créé, revenez ici pour effectuer la configuration et commencer à utiliser le connecteur Purview pour Amazon S3.

### <a name="create-a-purview-credential-for-your-aws-bucket-scan"></a>Créer des informations d’identification Purview pour votre analyse de compartiment AWS

Cette procédure décrit comment créer des informations d’identification Purview à utiliser pour l’analyse de vos compartiments AWS.

> [!TIP]
> Vous pouvez également créer des informations d’identification au milieu du processus, pendant la [configuration de votre analyse](#create-a-scan-for-your-amazon-s3-bucket). Dans ce cas, dans le champ **Informations d’identification**, sélectionnez **Nouveau**.
>

1. Dans Purview, accédez au **Centre de gestion** et, sous **Sécurité et accès**, sélectionnez **Informations d’identification**.

1. Sélectionnez **Nouveau**, puis dans le volet **Nouvelles informations d’identification** qui s’affiche à droite, utilisez les champs suivants pour créer vos informations d’identification Purview :

    |Champ |Description  |
    |---------|---------|
    |**Nom**     |Entrez un nom explicite pour ces informations d’identification ou utilisez celui par défaut.        |
    |**Description**     |Entrez une description facultative pour ces informations d’identification, par exemple, `Used to scan the tutorial S3 buckets`         |
    |**Méthode d’authentification**     |Sélectionnez **Rôle ARN**, car vous utilisez un rôle ARN pour accéder à votre compartiment.         |
    |**ID de compte Microsoft**     |Cliquez pour copier cette valeur dans le Presse-papiers. Utilisez cette valeur comme **ID de compte Microsoft** pendant la [création de votre rôle ARN dans AWS](#create-a-new-aws-role-for-purview).           |
    |**ID externe**     |Cliquez pour copier cette valeur dans le Presse-papiers. Utilisez cette valeur comme **ID externe** pendant la [création de votre rôle ARN dans AWS](#create-a-new-aws-role-for-purview).        |
    |**Role ARN**     | Une fois que vous avez [créé votre rôle Amazon IAM](#create-a-new-aws-role-for-purview), accédez à votre rôle dans la zone IAM, copiez la valeur **ARN du rôle** et entrez-la ici. Par exemple : `arn:aws:iam::284759281674:role/S3Role`. <br><br>Pour plus d’informations, consultez [Récupérer votre nouveau rôle ARN](#retrieve-your-new-role-arn). |
    | | |

    Sélectionnez **Créer** une fois vos informations d’identification créées.

Pour plus d’informations sur les informations d’identification Purview, consultez la [documentation de la préversion publique d’Azure Purview](manage-credentials.md).

### <a name="create-a-new-aws-role-for-purview"></a>Créer un rôle AWS pour Purview

1.  Ouvrez votre console **Amazon Web Services**, sous **Security, Identity, and Compliance** (Sécurité, identité et conformité), sélectionnez **IAM**.

1. Sélectionnez **Roles** (Rôles) et **Create role** (Créer un rôle).

1. Sélectionnez **Another AWS account** (Autre compte AWS), puis entrez les valeurs suivantes :

    |Champ  |Description  |
    |---------|---------|
    |**ID de compte**     |    Entrez votre ID de compte Microsoft. Par exemple : `615019938638`     |
    |**ID externe**     |   Sous les options, sélectionnez **Require external ID...** (Exiger un ID externe...), puis entrez votre ID externe dans le champ désigné. <br>Par exemple : `e7e2b8a3-0a9f-414f-a065-afaf4ac6d994`    <br><br>Vous pouvez trouver cet ID externe quand vous .  |
    | | |

    > [!NOTE]
    > Vous pouvez trouver les valeurs de l’**ID de compte Microsoft** et de l’**ID externe** dans la zone de Purview **Centre de gestion** > **Informations d’identification**, où vous avez [créé vos informations d’identification Purview](#create-a-purview-credential-for-your-aws-bucket-scan).
    >

    Par exemple :

    ![Ajoutez l’ID de compte Microsoft à votre compte AWS.](./media/register-scan-amazon-s3/aws-create-role-amazon-s3.png)

1. Dans la zone **Create role > Attach permissions policies** (Créer un rôle > Attacher des stratégies d’autorisation), filtrez les autorisations affichées sur **S3**. Sélectionnez **AmazonS3ReadOnlyAccess**, puis **Next: Tags** (Suivant : Étiquettes).

    ![Sélectionnez la stratégie ReadOnlyAccess pour le nouveau rôle d’analyse Amazon S3.](./media/register-scan-amazon-s3/aws-permission-role-amazon-s3.png)

1. Dans la zone **Add tags (optional)** (Ajouter des étiquettes (facultatif)), vous pouvez éventuellement choisir de créer une étiquette explicite pour ce nouveau rôle. Des étiquettes utiles vous permettent d’organiser, de suivre et de contrôler l’accès de chaque rôle que vous créez.

    Entrez une nouvelle clé et une valeur pour votre étiquette, si nécessaire. Une fois que vous avez terminé ou si vous voulez ignorer cette étape, sélectionnez **Next: Review** (Suivant : Vérifier) pour passer en revue les détails du rôle et terminer la création du rôle.

    ![Ajoutez une étiquette explicite pour organiser, suivre ou contrôler l’accès de votre nouveau rôle.](./media/register-scan-amazon-s3/add-tag-new-role.png)

1. Dans la zone **Review** (Vérifier), procédez comme suit :

    - Dans le champ **Role name** (Nom du rôle), entrez un nom explicite pour votre rôle
    - Dans la zone **Role description** (Description du rôle), entrez une description facultative pour identifier l’objectif du rôle
    - Dans la section **Policies** (Stratégies), vérifiez que la stratégie appropriée (**AmazonS3ReadOnlyAccess**) est attachée au rôle.

    Sélectionnez **Create role** (Créer le rôle) pour terminer le processus.

    Par exemple :

    ![Vérifiez les détails avant de créer votre rôle.](./media/register-scan-amazon-s3/review-role.png)


### <a name="configure-scanning-for-encrypted-amazon-s3-buckets"></a>Configurer l’analyse de compartiments Amazon S3 chiffrés

Les compartiments AWS prennent en charge plusieurs types de chiffrement. Pour les compartiments qui utilisent le chiffrement **AWS-KMS**, une configuration spéciale est nécessaire pour activer l’analyse.

> [!NOTE]
> Pour les compartiments qui n’utilisent pas de chiffrement, AES-256 ou le chiffrement AWS-KMS S3, ignorez cette section et passez à l’étape [Récupérer le nom de votre compartiment Amazon S3](#retrieve-your-amazon-s3-bucket-name).
>

**Pour vérifier le type de chiffrement utilisé dans vos compartiments Amazon S3 :**

1. Dans AWS, accédez à **Storage** > **S3** > (Stockage > S3) et sélectionnez **Buckets** (Compartiments) dans le menu de gauche.

    ![Sélectionnez l’onglet Amazon S3 Buckets (Compartiments Amazon S3).](./media/register-scan-amazon-s3/check-encryption-type-buckets.png)

1. Sélectionnez le compartiment à vérifier. Dans la page de détails du compartiment, sélectionnez l’onglet **Properties** (Propriétés) et faites défiler jusqu’à la zone **Default encryption** (Chiffrement par défaut).

    - Si le compartiment que vous avez sélectionné est configuré pour tous les chiffrements sauf **AWS-KMS** ou si le chiffrement par défaut de votre compartiment est **Désactivé**, ignorez le reste de cette procédure et passez à l’étape [Récupérer le nom de votre compartiment Amazon S3](#retrieve-your-amazon-s3-bucket-name).

    - Si le compartiment sélectionné est configuré pour le chiffrement **AWS-KMS**, continuez comme décrit ci-dessous pour ajouter une nouvelle stratégie permettant d’analyser un compartiment avec un chiffrement **AWS-KMS** personnalisé.

    Par exemple :

    ![Voir un compartiment Amazon S3 configuré avec le chiffrement AWS-KMS](./media/register-scan-amazon-s3/default-encryption-buckets.png)

**Pour ajouter une nouvelle stratégie permettant d’analyser un compartiment avec un chiffrement AWS-KMS personnalisé :**

1. Dans AWS, accédez à **Services** >  **IAM** >  **Policies** (Stratégies), puis sélectionnez **Create policy** (Créer une stratégie).

1. Sous l’onglet **Create policy** > **Visual editor** (éditeur visuel), définissez votre stratégie avec les valeurs suivantes :

    |Champ  |Description  |
    |---------|---------|
    |**Service**     |  Entrez et sélectionnez **KMS**.       |
    |**Actions**     | Sous **Access level** (Niveau d’accès), sélectionnez **Write** (Écrire) pour développer la section **Write**.<br>Une fois la section développée, sélectionnez uniquement l’option **Decrypt** (Déchiffrer).        |
    |**Ressources**     |Sélectionnez une ressource spécifique ou **All resources** (Toutes les ressources).         |
    | | |

    Une fois que vous avez terminé, sélectionnez **Review policy** (Vérifier la stratégie) pour continuer.

    ![Créez une stratégie pour analyser un compartiment avec le chiffrement AWS-KMS.](./media/register-scan-amazon-s3/create-policy-kms.png)

1. Dans la page **Review policy**, entrez un nom explicite pour votre stratégie et une description facultative, puis sélectionnez **Create policy**.

    La stratégie nouvellement créée est ajoutée à votre liste de stratégies.

1. Attachez votre nouvelle stratégie au rôle que vous avez ajouté pour l’analyse.

    1. Revenez à la page **IAM** > **Roles**, puis sélectionnez le rôle que vous avez ajouté [précédemment](#create-a-new-aws-role-for-purview).

    1. Sous l’onglet **Permissions** (Autorisations), sélectionnez **Attach policies** (Attacher des stratégies).

        ![Sous l’onglet Permissions de votre rôle, sélectionnez Attach policies.](./media/register-scan-amazon-s3/iam-attach-policies.png)

    1. Dans la page **Attach Permissions** (Attacher des autorisations), recherchez et sélectionnez la nouvelle stratégie créée ci-dessus. Sélectionnez **Attach policy** pour attacher votre stratégie au rôle.

        La page **Summary** (Récapitulatif) est mise à jour avec votre nouvelle stratégie attachée à votre rôle.

        ![Consultez une page récapitulative mise à jour avec la nouvelle stratégie attachée à votre rôle.](./media/register-scan-amazon-s3/attach-policy-role.png)

### <a name="retrieve-your-new-role-arn"></a>Récupérer votre nouveau rôle ARN

Vous devez enregistrer votre rôle AWS ARN et le copier dans Purview pendant la [création d’une analyse pour votre compartiment Amazon S3](#create-a-scan-for-your-amazon-s3-bucket).

**Pour récupérer votre rôle ARN :**

1. Dans la zone AWS **Identity and Access Management (IAM)**  > **Roles** (Gestion des identités et des accès (IAM) > Rôles), recherchez et sélectionnez le nouveau rôle que vous avez [créé pour Purview](#create-a-purview-credential-for-your-aws-bucket-scan).

1. Dans la page **Summary** du rôle, cliquez sur le bouton **Copy to clipboard** (Copier dans le Presse-papiers) à droite de la valeur **Role ARN**.

    ![Copiez la valeur du rôle ARN dans le Presse-papiers.](./media/register-scan-amazon-s3/aws-copy-role-purview.png)

1. Collez cette valeur dans un emplacement sécurisé afin de l’utiliser par la suite lors de la [création d’une analyse pour votre compartiment Amazon S3](#create-a-scan-for-your-amazon-s3-bucket).

### <a name="retrieve-your-amazon-s3-bucket-name"></a>Récupérer le nom de votre compartiment Amazon S3

Vous avez besoin du nom de votre compartiment Amazon S3 pour le copier dans Purview pendant la [création d’une analyse pour votre compartiment Amazon S3](#create-a-scan-for-your-amazon-s3-bucket)

**Pour récupérer le nom de votre compartiment :**

1. Dans AWS, accédez à **Storage** > **S3** > (Stockage > S3) et sélectionnez **Buckets** (Compartiments) dans le menu de gauche.

    ![Consultez l’onglet Amazon S3 Buckets (Compartiments Amazon S3).](./media/register-scan-amazon-s3/check-encryption-type-buckets.png)

1. Recherchez et sélectionnez votre compartiment pour voir la page de détails du compartiment, puis copiez le nom du compartiment dans le Presse-papiers.

    Par exemple :

    ![Récupérez et copiez l’URL du compartiment S3.](./media/register-scan-amazon-s3/retrieve-bucket-url-amazon.png)

    Collez le nom de votre compartiment dans un fichier sécurisé et ajoutez-lui un préfixe `s3://` pour créer la valeur à entrer pendant la configuration de votre compartiment comme ressource Purview.

    Par exemple : `s3://purview-tutorial-bucket`

> [!NOTE]
> Seul le niveau racine de votre compartiment est pris en charge comme source de données Purview. Par exemple, l’URL suivante, qui comprend un sous-dossier, n’est *pas* prise en charge : `s3://purview-tutorial-bucket/view-data`
>

### <a name="locate-your-aws-account-id"></a>Localiser votre ID de compte AWS

Vous avez besoin de votre ID de compte AWS pour inscrire votre compte AWS comme source de données Purview, ainsi que tous ses compartiments.

Votre ID de compte AWS est l’ID que vous utilisez pour vous connecter à la console AWS. Vous pouvez également le trouver après vous être connecté au tableau de bord IAM, en haut à gauche sous les options de navigation : il s’agit de la partie numérique de votre URL de connexion :

Par exemple :

![Récupérez votre ID de compte AWS.](./media/register-scan-amazon-s3/aws-locate-account-id.png)


## <a name="add-a-single-amazon-s3-bucket-as-a-purview-resource"></a>Ajouter un seul compartiment Amazon S3 comme ressource Purview

Utilisez cette procédure si vous avez seulement un compartiment S3 à inscrire dans Purview comme source de données ou si vous avez plusieurs compartiments dans votre compte AWS, mais que vous ne voulez pas tous les inscrire dans Purview.

1. Lancez le portail Purview à l’aide de l’URL du connecteur Purview dédié pour Amazon S3. Cette URL vous a été fournie par l’équipe de gestion de produit du connecteur Amazon S3 Purview.

    ![Lancez le portail Purview.](./media/register-scan-amazon-s3/purview-portal-amazon-s3.png)

1. Accédez à la page **Sources** d’Azure Purview et sélectionnez **Inscrire** ![icône Inscrire.](./media/register-scan-amazon-s3/register-button.png) > **Amazon S3** > **Continuer**.

    ![Ajoutez un compartiment Amazon AWS comme source de données Purview.](./media/register-scan-amazon-s3/add-s3-datasource-to-purview.png)

    > [!TIP]
    > Si vous avez plusieurs [collections](manage-data-sources.md#manage-collections) et que vous voulez ajouter votre Amazon S3 à une collection spécifique, sélectionnez la **Vue cartographique** en haut à droite, puis sélectionnez le bouton **Inscrire** ![icône Inscrire.](./media/register-scan-amazon-s3/register-button.png) dans votre collection.
    >

1. Dans le volet **Inscrire des sources (Amazon S3)** qui s’ouvre, entrez les informations suivantes :

    |Champ  |Description  |
    |---------|---------|
    |**Nom**     |Entrez un nom explicite ou utilisez le nom fourni par défaut.         |
    |**URL du compartiment**     | Entrez l’URL de votre compartiment AWS en utilisant la syntaxe suivante :   `s3://<bucketName>`     <br><br>**Remarque** : Veillez à utiliser uniquement le niveau racine de votre compartiment, sans sous-dossier. Pour plus d’informations, consultez [Récupérer le nom de votre compartiment Amazon S3](#retrieve-your-amazon-s3-bucket-name). |
    |**Sélectionner une collection** |Si vous avez choisi d’inscrire une source de données à partir d’une collection, cette collection est déjà listée. <br><br>Sélectionnez une autre collection selon vos besoins, **Aucune** pour ne pas attribuer de collection ou **Nouveau** pour créer une collection maintenant. <br><br>Pour plus d’informations sur les collections Purview, consultez [Gérer les sources de données dans Azure Purview](manage-data-sources.md#manage-collections).|
    | | |

    Une fois que vous avez terminé, sélectionnez **Terminer** pour terminer l’inscription.

Passez à l’étape [Créer une analyse pour votre compartiment Amazon S3.](#create-a-scan-for-your-amazon-s3-bucket).

## <a name="add-all-of-your-amazon-s3-buckets-as-purview-resources"></a>Ajouter tous vos compartiments Amazon S3 comme ressources Purview

Utilisez cette procédure si vous avez plusieurs compartiments S3 dans votre compte Amazon et voulez tous les inscrire comme sources de données Purview.

1. Lancez le portail Purview à l’aide de l’URL du connecteur Purview dédié pour Amazon S3. Cette URL vous a été fournie par l’équipe de gestion de produit du connecteur Amazon S3 Purview.

    ![Lancer le portail Purview dédié au connecteur pour Amazon S3](./media/register-scan-amazon-s3/purview-portal-amazon-s3.png)

1. Accédez à la page **Sources** d’Azure Purview et sélectionnez **Inscrire** ![icône Inscrire.](./media/register-scan-amazon-s3/register-button.png) > **Comptes Amazon** > **Continuer**.

    ![Ajoutez un compte Amazon comme source de données Purview.](./media/register-scan-amazon-s3/add-s3-account-to-purview.png)

    > [!TIP]
    > Si vous avez plusieurs [collections](manage-data-sources.md#manage-collections) et que vous voulez ajouter votre Amazon S3 à une collection spécifique, sélectionnez la **Vue cartographique** en haut à droite, puis sélectionnez le bouton **Inscrire** ![icône Inscrire.](./media/register-scan-amazon-s3/register-button.png) dans votre collection.
    >

1. Dans le volet **Inscrire des sources (Amazon S3)** qui s’ouvre, entrez les informations suivantes :

    |Champ  |Description  |
    |---------|---------|
    |**Nom**     |Entrez un nom explicite ou utilisez le nom fourni par défaut.         |
    |**ID de compte AWS**     | Entrez votre ID de compte AWS. Pour plus d’informations, consultez [Localiser votre ID de compte AWS](#locate-your-aws-account-id)|
    |**Sélectionner une collection** |Si vous avez choisi d’inscrire une source de données à partir d’une collection, cette collection est déjà listée. <br><br>Sélectionnez une autre collection selon vos besoins, **Aucune** pour ne pas attribuer de collection ou **Nouveau** pour créer une collection maintenant. <br><br>Pour plus d’informations sur les collections Purview, consultez [Gérer les sources de données dans Azure Purview](manage-data-sources.md#manage-collections).|
    | | |

    Une fois que vous avez terminé, sélectionnez **Terminer** pour terminer l’inscription.

Passez à l’étape [Créer une analyse pour votre compartiment Amazon S3](#create-a-scan-for-your-amazon-s3-bucket).

## <a name="create-a-scan-for-your-amazon-s3-bucket"></a>Créer une analyse pour votre compartiment Amazon S3

Une fois que vous avez ajouté vos compartiments comme sources de données Purview, vous pouvez configurer une analyse à exécuter à intervalles planifiés ou immédiatement.

1. Accédez à la zone **Sources** d’Azure Purview, puis effectuez l’une des opérations suivantes :

    - Dans la **Vue cartographique**, sélectionnez **Nouvelle analyse** ![icône Nouvelle analyse.](./media/register-scan-amazon-s3/new-scan-button.png) dans votre zone de source de données.
    - En **mode liste**, pointez sur la ligne de votre source de données et sélectionnez **Nouvelle analyse** ![icône Nouvelle analyse.](./media/register-scan-amazon-s3/new-scan-button.png)

1. Dans le volet **Analyser...** qui s’ouvre à droite, définissez les champs suivants et sélectionnez **Continuer** :

    |Champ  |Description  |
    |---------|---------|
    |**Nom**     |  Entrez un nom explicite pour votre analyse ou utilisez le nom par défaut.       |
    |**Type** |S’affiche uniquement si vous avez ajouté votre compte AWS avec tous les compartiments inclus. <br><br>Les options actuelles comprennent uniquement **Tout** > **Amazon S3**. De nouvelles options seront disponibles avec le développement de la matrice de prise en charge de Purview. |
    |**Informations d'identification**     |  Sélectionnez des informations d’identification Purview avec votre rôle ARN. <br><br>**Conseil** : Si vous voulez créer des informations d’identification à cette étape, sélectionnez **Nouveau**. Pour plus d’informations, consultez [Créer des informations d’identification Purview pour votre analyse de compartiment AWS](#create-a-purview-credential-for-your-aws-bucket-scan).     |
    |     |         |

    Purview vérifie automatiquement que le rôle ARN est valide, et que le compartiment et l’objet dans le compartiment sont accessibles, puis continue si la connexion est établie.

    > [!TIP]
    > Pour entrer des valeurs différentes et tester la connexion vous-même avant de continuer, sélectionnez **Tester la connexion** en bas à droite avant de sélectionner **Continuer**.
    >

1. Dans le volet **Sélectionner un ensemble de règles d’analyse**, sélectionnez l’ensemble de règles par défaut **AmazonS3** ou sélectionnez **Nouvel ensemble de règles d’analyse** pour en créer un personnalisé. Une fois que vous avez choisi votre ensemble de règles, sélectionnez **Continuer**.

    Si vous choisissez de créer un ensemble de règles d’analyse personnalisé, utilisez l’Assistant pour définir les paramètres suivants :

    |Volet  |Description  |
    |---------|---------|
    |**Nouvel ensemble de règles d’analyse** /<br>**Description de la règle d’analyse**    |   Entrer un nom explicite et une description facultative pour votre ensemble de règles      |
    |**Sélectionner des types de fichier**     | Sélectionnez tous les types de fichier à inclure dans l’analyse, puis sélectionnez **Continuer**.<br><br>Pour ajouter un nouveau type de fichier, sélectionnez **Nouveau type de fichier** et définissez les éléments suivants : <br>- L’extension de fichier à ajouter <br>- Une description facultative  <br>- Indiquez si le contenu du fichier a un délimiteur personnalisé ou s’il s’agit d’un type de fichier système. Entrez ensuite votre délimiteur personnalisé ou sélectionnez votre type de fichier système. <br><br>Sélectionnez **Créer** pour créer votre type de fichier personnalisé.     |
    |**Sélectionner des règles de classification**     |   Accédez aux règles de classification et sélectionnez celles que vous voulez exécuter sur votre jeu de données.      |
    |     |         |

    Sélectionnez **Créer** une fois vous avez terminé de créer votre ensemble de règles.

1. Dans le volet **Définir un déclencheur d’analyse**, sélectionnez l’une des options suivantes et cliquez sur **Continuer** :

    - **Périodique** pour configurer une planification pour une analyse périodique
    - **Une fois** pour configurer une analyse qui démarre immédiatement

1. Dans le volet **Vérifier votre analyse**, vérifiez les détails de l’analyse pour confirmer qu’ils sont corrects, puis sélectionnez **Enregistrer** ou **Enregistrer et exécuter** si vous avez sélectionné **Une fois** dans le volet précédent.

    > [!NOTE]
    > Une fois démarrée, l’analyse peut prendre jusqu’à 24 heures. Vous pouvez consulter vos **Rapports d’insights** et rechercher dans le catalogue 24 heures après avoir démarré l’analyse.
    >

Pour plus d’informations, consultez [Explorer les résultats d’analyse Purview](#explore-purview-scanning-results).

## <a name="explore-purview-scanning-results"></a>Explorer les résultats d’analyse Purview

Une fois l’analyse Purview terminée sur vos compartiments Amazon S3, explorez en détail la zone **Sources** de Purview pour voir l’historique d’analyse.

Sélectionnez une source de données pour voir ses détails, puis sélectionnez l’onglet **Analyses** pour voir les analyses en cours d’exécution ou terminées.
Si vous avez ajouté un compte AWS avec plusieurs compartiments, l’historique d’analyse de chaque compartiment s’affiche sous le compte.

Par exemple :

![Affichez les analyses de compartiment AWS S3 sous votre source de compte AWS.](./media/register-scan-amazon-s3/account-scan-history.png)

Utilisez les autres zones de Purview pour en savoir plus sur le contenu de votre parc de données, notamment vos compartiments Amazon S3 :

- **Recherchez dans le catalogue de données Purview** et filtrez sur un compartiment spécifique. Par exemple :

    ![Recherchez des ressources AWS S3 dans le catalogue.](./media/register-scan-amazon-s3/search-catalog-screen-aws.png)

- **Consultez les rapports d’insights** pour voir des statistiques sur la classification, les étiquettes de confidentialité, les types de fichier et d’autres détails sur votre contenu.

    Tous les rapports d’insights de Purview comprennent les résultats d’analyse Amazon S3, ainsi que les autres résultats de vos sources de données Azure. Le cas échéant, un type de ressource **Amazon S3** supplémentaire est ajouté aux options de filtrage de rapport.

    Pour plus d’informations, consultez [Présentation des insights dans Azure Purview](concept-insights.md).

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur les rapports d’insights Azure Purview :

> [!div class="nextstepaction"]
> [Présentation des insights dans Azure Purview](concept-insights.md)
