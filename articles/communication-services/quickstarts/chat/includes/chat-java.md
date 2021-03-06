---
title: Fichier Include
description: Fichier include
services: azure-communication-services
author: mikben
manager: mikben
ms.service: azure-communication-services
ms.subservice: azure-communication-services
ms.date: 9/1/2020
ms.topic: include
ms.custom: include file
ms.author: mikben
ms.openlocfilehash: 192970540f21905b624ce3f6e3558baa935a4d7a
ms.sourcegitcommit: 8d1b97c3777684bd98f2cfbc9d440b1299a02e8f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/09/2021
ms.locfileid: "102489734"
---
## <a name="prerequisites"></a>Prérequis

- Compte Azure avec un abonnement actif. [Créez un compte gratuitement](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Java Development Kit (JDK)](/java/azure/jdk/) version 8 ou ultérieure.
- [Apache Maven](https://maven.apache.org/download.cgi).
- Chaîne de connexion et ressource Communication Services déployée. [Créez une ressource Communication Services](../../create-communication-resource.md).
- [Jeton d’accès utilisateur](../../access-tokens.md). Veillez à définir l’étendue sur « chat » (conversation) et notez la chaîne token ainsi que la chaîne userId.


## <a name="setting-up"></a>Configuration

### <a name="create-a-new-java-application"></a>Créer une application Java

Ouvrez votre terminal ou votre fenêtre Commande, puis accédez au répertoire dans lequel vous souhaitez créer votre application Java. Exécutez la commande ci-dessous pour générer le projet Java à partir du modèle maven-archetype-quickstart.

```console
mvn archetype:generate -DgroupId=com.communication.quickstart -DartifactId=communication-quickstart -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
```

Vous remarquerez que l’objectif « generate » a créé un répertoire portant le même nom que l’artifactId. Sous ce répertoire, `src/main/java directory` contient le code source du projet, le répertoire `src/test/java` contient la source de test et le fichier pom.xml est le modèle objet du projet, ou [POM](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html).

Mettez à jour le fichier POM de votre application pour utiliser Java 8 ou version ultérieure :

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
</properties>
```

### <a name="add-the-package-references-for-the-chat-client-library"></a>Ajouter les références de package pour la bibliothèque de client de conversation

Dans votre fichier POM, référencez le package `azure-communication-chat` avec les API de conversation (Chat) :

```xml
<dependency>
    <groupId>com.azure</groupId>
    <artifactId>azure-communication-chat</artifactId>
    <version>1.0.0-beta.4</version> 
</dependency>
```

Pour l’authentification, votre client doit référencer le package `azure-communication-common` :

```xml
<dependency>
    <groupId>com.azure</groupId>
    <artifactId>azure-communication-common</artifactId>
    <version>1.0.0</version> 
</dependency>
```

## <a name="object-model"></a>Modèle objet

Les classes et interfaces suivantes gèrent quelques-unes des principales fonctionnalités de la bibliothèque de client Azure Communication Services Chat pour Java.

| Nom                                  | Description                                                  |
| ------------------------------------- | ------------------------------------------------------------ |
| ChatClient | Cette classe est nécessaire à la fonctionnalité de conversation (Chat). Vous l’instanciez avec vos informations d’abonnement et l’utilisez pour créer, obtenir et supprimer des fils de conversation. |
| ChatAsyncClient | Cette classe est nécessaire à la fonctionnalité de conversation (Chat) asynchrone. Vous l’instanciez avec vos informations d’abonnement et l’utilisez pour créer, obtenir et supprimer des fils de conversation. |
| ChatThreadClient | Cette classe est nécessaire à la fonctionnalité de fil de conversation (Chat Thread). Vous obtenez une instance via ChatClient et l’utilisez pour envoyer/recevoir/mettre à jour/supprimer des messages, ajouter/supprimer/obtenir des utilisateurs, envoyer des notifications de saisie et des accusés de lecture. |
| ChatThreadAsyncClient | Cette classe est nécessaire à la fonctionnalité de fil de conversation (Chat Thread) asynchrone. Vous obtenez une instance via ChatAsyncClient et l’utilisez pour envoyer/recevoir/mettre à jour/supprimer des messages, ajouter/supprimer/obtenir des utilisateurs, envoyer des notifications de saisie et des accusés de lecture. |

## <a name="create-a-chat-client"></a>Créer un client de conversation
Pour créer un client de conversation, vous allez utiliser le point de terminaison Communication Services ainsi que le jeton d’accès qui a été généré au cours des étapes prérequises. Les jetons d’accès utilisateur vous permettent de créer des applications clientes qui s’authentifient directement auprès d’Azure Communication Services. Une fois que vous avez généré ces jetons sur votre serveur, transmettez-les en retour à un appareil client. Vous devez utiliser la classe CommunicationTokenCredential de la bibliothèque de client commune pour passer le jeton à votre client de conversation. 

En savoir plus sur l’[Architecture de conversation](../../../concepts/chat/concepts.md)

Si vous devez ajouter des instructions d’importation, veillez à ajouter uniquement des importations des espaces de noms com.azure.communication.chat et com.azure.communication.chat.models, et non de l’espace de noms com.azure.communication.chat.implementation. Dans le fichier App.java qui a été généré via Maven, vous pouvez commencer avec le code suivant :

```Java
import com.azure.communication.chat.*;
import com.azure.communication.chat.models.*;
import com.azure.communication.common.*;
import com.azure.core.http.HttpClient;

import java.io.*;

public class App
{
    public static void main( String[] args ) throws IOException
    {
        System.out.println("Azure Communication Services - Chat Quickstart");
        
        // Your unique Azure Communication service endpoint
        String endpoint = "https://<RESOURCE_NAME>.communication.azure.com";

        // Create an HttpClient builder of your choice and customize it
        // Use com.azure.core.http.netty.NettyAsyncHttpClientBuilder if that suits your needs
        NettyAsyncHttpClientBuilder yourHttpClientBuilder = new NettyAsyncHttpClientBuilder();
        HttpClient httpClient = yourHttpClientBuilder.build();

        // User access token fetched from your trusted service
        String userAccessToken = "<USER_ACCESS_TOKEN>";

        // Create a CommunicationTokenCredential with the given access token, which is only valid until the token is valid
        CommunicationTokenCredential userCredential = new CommunicationTokenCredential(userAccessToken);

        // Initialize the chat client
        final ChatClientBuilder builder = new ChatClientBuilder();
        builder.endpoint(endpoint)
            .credential(userCredential)
            .httpClient(httpClient);
        ChatClient chatClient = builder.buildClient();
    }
}
```


## <a name="start-a-chat-thread"></a>Démarrer un fil de conversation

Utilisez la méthode `createChatThread` pour créer un fil de conversation.
`createChatThreadOptions` est utilisé pour décrire la demande de fil.

- Utilisez `topic` pour attribuer un sujet à cette conversation ; le sujet peut être mis à jour après que le fil de conversation a été créé à l’aide de la fonction `UpdateThread`.
- Utilisez `participants` pour lister les participants au fil à ajouter à la conversation. `ChatParticipant` prend l’utilisateur que vous avez créé dans le démarrage rapide [Jeton d’accès utilisateur](../../access-tokens.md).

La réponse `chatThreadClient` est utilisée pour effectuer les opérations sur le fil de conversation créé : ajout de participants au fil de conversation, envoi d’un message, suppression d’un message, etc. Elle contient une propriété `chatThreadId` qui est l’ID unique du fil de conversation. La propriété est accessible par la méthode publique .getChatThreadId().

```Java
List<ChatParticipant> participants = new ArrayList<ChatParticipant>();

ChatParticipant firstThreadParticipant = new ChatParticipant()
    .setCommunicationIdentifier(firstUser)
    .setDisplayName("Participant Display Name 1");
    
ChatParticipant secondThreadParticipant = new ChatParticipant()
    .setCommunicationIdentifier(secondUser)
    .setDisplayName("Participant Display Name 2");

participants.add(firstThreadParticipant);
participants.add(secondThreadParticipant);

CreateChatThreadOptions createChatThreadOptions = new CreateChatThreadOptions()
    .setTopic("Topic")
    .setParticipants(participants);
ChatThreadClient chatThreadClient = chatClient.createChatThread(createChatThreadOptions);
String chatThreadId = chatThreadClient.getChatThreadId();
```

## <a name="send-a-message-to-a-chat-thread"></a>Envoyer un message à un fil de conversation

Utilisez la méthode `sendMessage` pour envoyer un message au fil que vous venez de créer, identifié par chatThreadId.
`sendChatMessageOptions` est utilisé pour décrire la demande de message de conversation.

- Utilisez `content` pour fournir le contenu du message de conversation.
- Utilisez `type` pour spécifier le type de contenu du message de conversation, TEXTE ou HTML.
- Utilisez `senderDisplayName` pour spécifier le nom d’affichage de l’expéditeur.

La réponse `sendChatMessageResult` contient un `id`, qui est l’ID unique du message.

```Java
SendChatMessageOptions sendChatMessageOptions = new SendChatMessageOptions()
    .setContent("Message content")
    .setType(ChatMessageType.TEXT)
    .setSenderDisplayName("Sender Display Name");

SendChatMessageResult sendChatMessageResult = chatThreadClient.sendMessage(sendChatMessageOptions);
String chatMessageId = sendChatMessageResult.getId();
```


## <a name="get-a-chat-thread-client"></a>Obtenir un client de fil de conversation

La méthode `getChatThreadClient` retourne un client de fil pour un fil qui existe déjà. Elle peut être utilisée pour effectuer des opérations sur le fil créé : ajout de participants, envoi d’un message, etc. `chatThreadId` est l’ID unique du fil de conversation existant.

```Java
String chatThreadId = "Id";
ChatThread chatThread = chatClient.getChatThread(chatThreadId);
```

## <a name="receive-chat-messages-from-a-chat-thread"></a>Recevoir les messages de conversation d’un fil de conversation

Vous pouvez récupérer les messages de conversation en interrogeant la méthode `listMessages` sur le client de fil de conversation selon des intervalles définis.

```Java
chatThreadClient.listMessages().iterableByPage().forEach(resp -> {
    System.out.printf("Response headers are %s. Url %s  and status code %d %n", resp.getHeaders(),
        resp.getRequest().getUrl(), resp.getStatusCode());
    resp.getItems().forEach(message -> {
        System.out.printf("Message id is %s.", message.getId());
    });
});
```

`listMessages` retourne la version la plus récente du message, avec les modifications ou les suppressions dont le message a éventuellement fait l’objet via .editMessage() et .deleteMessage(). Pour les messages supprimés, `chatMessage.getDeletedOn()` retourne une valeur datetime indiquant à quel moment ce message a été supprimé. Pour les messages modifiés, `chatMessage.getEditedOn()` retourne une valeur datetime indiquant à quel moment ce message a été modifié. Il est possible d’accéder à l’heure initiale de création du message à l’aide de `chatMessage.getCreatedOn()` ; elle peut être utilisée à des fins de classement des messages.

`listMessages` retourne différents types de messages qui peuvent être identifiés par `chatMessage.getType()`. Ces types sont les suivants :

- `text` : Message de conversation ordinaire envoyé par un participant au fil de conversation.

- `html` : message de conversation envoyé par un participant au fil de conversation.

- `topicUpdated`: Message système qui indique que le sujet a été mis à jour

- `participantAdded` : Message système qui indique qu’un ou plusieurs participants ont été ajoutés au fil de conversation.

- `participantRemoved` : Message système qui indique qu’un participant a été supprimé du fil de conversation.

Pour plus d’informations, consultez [Types de messages](../../../concepts/chat/concepts.md#message-types).

## <a name="add-a-user-as-participant-to-the-chat-thread"></a>Ajouter un utilisateur comme participant au fil de conversation

Une fois qu’un fil de conversation est créé, vous pouvez y ajouter des utilisateurs et en supprimer. En ajoutant des utilisateurs, vous leur permettez d’envoyer des messages au fil de conversation et d’ajouter/supprimer d’autres participants. Vous devez commencer par obtenir un nouveau jeton d’accès et une identité pour cet utilisateur. Avant d’appeler la méthode addParticipants, vérifiez que vous avez acquis un nouveau jeton d’accès et une identité pour cet utilisateur. L’utilisateur aura besoin de ce jeton d’accès pour initialiser son client de conversation.

Utilisez la méthode `addParticipants` pour ajouter des participants au fil identifié par threadId.

- Utilisez `listParticipants` pour lister les participants à ajouter au fil de conversation.
- `communicationIdentifier`, obligatoire. Il s’agit du CommunicationIdentifier que vous avez créé avec le CommunicationIdentityClient dans le guide de démarrage rapide [Jeton d’accès utilisateur](../../access-tokens.md).
- `display_name`, facultatif, est le nom d’affichage pour le participant au fil.
- `share_history_time`, facultatif, est le moment à partir duquel l’historique de conversation est partagé avec le participant. Pour partager l’historique depuis le début du fil de conversation, attribuez à cette propriété une date égale ou antérieure à la date de création du fil. Pour ne pas partager l’historique antérieur au moment où le participant a été ajouté, définissez-la sur l’heure actuelle. Pour partager un historique partiel, attribuez-lui la date de votre choix.

```Java
List<ChatParticipant> participants = new ArrayList<ChatParticipant>();

ChatParticipant firstThreadParticipant = new ChatParticipant()
    .setCommunicationIdentifier(identity1)
    .setDisplayName("Display Name 1");

ChatParticipant secondThreadParticipant = new ChatParticipant()
    .setCommunicationIdentifier(identity2)
    .setDisplayName("Display Name 2");

participants.add(firstThreadParticipant);
participants.add(secondThreadParticipant);

AddChatParticipantsOptions addChatParticipantsOptions = new AddChatParticipantsOptions()
    .setParticipants(participants);
chatThreadClient.addParticipants(addChatParticipantsOptions);
```

## <a name="remove-participant-from-a-chat-thread"></a>Supprimer un participant d’un fil de conversation

De la même façon que vous ajoutez un participant à un fil de conversation, vous pouvez supprimer des participants d’un fil de conversation. Pour ce faire, vous devez suivre les identités des participants que vous avez ajoutés.

Utilisez `removeParticipant`, où `identifier` est le CommunicationUserIdentifier que vous avez créé.

```Java
chatThreadClient.removeParticipant(identity);
```

## <a name="run-the-code"></a>Exécuter le code

Accédez au répertoire contenant le fichier *pom.xml*, puis compilez le projet à l’aide de la commande `mvn` suivante.

```console
mvn compile
```

Ensuite, générez le package.

```console
mvn package
```

Exécutez la commande `mvn` suivante pour exécuter l’application.

```console
mvn exec:java -Dexec.mainClass="com.communication.quickstart.App" -Dexec.cleanupDaemonThreads=false
```