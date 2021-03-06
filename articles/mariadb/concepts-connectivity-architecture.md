---
title: Architecture de connectivité - Azure Database for MariaDB
description: Décrit l’architecture de connectivité pour votre serveur Azure Database for MariaDB.
author: Bashar-MSFT
ms.author: bahusse
ms.service: mariadb
ms.topic: conceptual
ms.date: 2/11/2021
ms.openlocfilehash: b166e2f648446ac1672ead00a774d71d34699380
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101724640"
---
# <a name="connectivity-architecture-in-azure-database-for-mariadb"></a>Architecture de connectivité dans Azure Database for MariaDB
Cet article présente l’architecture de connectivité Azure Database for MariaDB, ainsi que la façon dont le trafic est orienté vers votre instance Azure Database for MariaDB des clients dans Azure et en dehors.

## <a name="connectivity-architecture"></a>Architecture de connectivité

La connexion à votre instance Azure Database for MariaDB est établie via une passerelle qui est responsable du routage des connexions entrantes vers l’emplacement physique de votre serveur dans nos clusters. Le schéma suivant illustre le flux de trafic.

![Vue d’ensemble de l’architecture de connectivité](./media/concepts-connectivity-architecture/connectivity-architecture-overview-proxy.png)


Lorsque le client se connecte à la base de données, la chaîne de connexion au serveur correspond à l’adresse IP de la passerelle. La passerelle écoute sur l’adresse IP sur le port 3306. À l’intérieur du cluster de bases de données, le trafic est transféré vers l’instance Azure Database for MariaDB appropriée. Par conséquent, pour vous connecter à votre serveur, notamment à partir de réseaux d’entreprise, il est nécessaire d’ouvrir le **pare-feu côté client pour autoriser le trafic sortant à atteindre nos passerelles**. Vous trouverez ci-dessous une liste complète des adresses IP utilisées par nos passerelles en fonction de la région.

## <a name="azure-database-for-mariadb-gateway-ip-addresses"></a>Adresses IP de passerelle Azure Database for MariaDB

Le service de passerelle est hébergé sur un groupe de nœuds de calcul sans état situé derrière une adresse IP, que votre client doit atteindre en premier lors de la tentative de connexion à un serveur Azure Database for MariaDB. 

Dans le cadre de la maintenance de service en cours, nous allons actualiser régulièrement le matériel de calcul hébergeant les passerelles pour nous assurer que nous proposons l’expérience la plus sûre et la plus performante. Lorsque le matériel de passerelle est actualisé, un nouvel anneau des nœuds de calcul est créé en premier. Ce nouvel anneau gère le trafic pour tous les serveurs Azure Database for MariaDB nouvellement créés. Il a une adresse IP différente des anneaux de passerelle plus anciens dans la même région pour différencier le trafic. Une fois que le nouvel anneau est entièrement fonctionnel, la mise hors service de l’ancien matériel de passerelle desservant les serveurs existants est planifiée. Avant de mettre hors service un matériel de passerelle, les clients qui exécutent leurs serveurs et se connectent à des anneaux de passerelle plus anciens sont avertis par e-mail et dans le portail Azure, trois mois avant la mise hors service. La mise hors service des passerelles peut avoir un impact sur la connectivité de vos serveurs si 

* Vous codez en dur les adresses IP de la passerelle dans la chaîne de connexion de votre application. Cela **n’est pas recommandé**. Vous devez utiliser le nom de domaine complet (FQDN) de votre serveur au format <servername>.mariadb.database.azure.com dans la chaîne de connexion de votre application. 
* Vous ne mettez pas à jour les adresses IP de passerelle les plus récentes dans le pare-feu côté client pour autoriser le trafic sortant à atteindre nos nouveaux anneaux de passerelle.

Le tableau suivant répertorie les adresses IP de la passerelle Azure Database for MariaDB pour toutes les régions de données. Les informations les plus récentes des adresses IP de la passerelle pour chaque région sont indiquées dans le tableau ci-dessous. Dans le tableau ci-dessous, les colonnes représentent les éléments suivants :

* **Adresses IP de la passerelle :** cette colonne répertorie les adresses IP actuelles des passerelles hébergées sur la dernière génération de matériel. Si vous provisionnez un nouveau serveur, nous vous recommandons d’ouvrir le pare-feu côté client afin d’autoriser le trafic sortant pour les adresses IP répertoriées dans cette colonne.
* **Adresses IP de passerelle (en cours de mise hors service) :** cette colonne répertorie les adresses IP des passerelles hébergées sur une ancienne génération de matériel en cours de mise hors service. Si vous provisionnez un nouveau serveur, vous pouvez ignorer ces adresses IP. Si vous disposez déjà d’un serveur, continuez à conserver la règle de trafic sortant pour le pare-feu pour ces adresses IP, car nous ne l’avons pas encore mis hors service. Si vous supprimez les règles de pare-feu pour ces adresses IP, vous risquez d’obtenir des erreurs de connectivité. Au lieu de cela, vous devez ajouter de manière proactive les nouvelles adresses IP répertoriées dans la colonne Adresses IP de la passerelle à la règle de pare-feu de trafic sortant dès que vous recevez la notification de mise hors service. Ainsi, lorsque votre serveur sera migré vers le dernier matériel de passerelle, il n’y aura aucune interruption de la connectivité à votre serveur.
* **Adresses IP de passerelle (mises hors service) :** cette colonne répertorie les adresses IP des anneaux de passerelle, qui sont désactivées et qui ne sont plus fonctionnelles. Vous pouvez supprimer ces adresses IP de votre règle de pare-feu sortante en toute sécurité. 


| **Nom de la région** | **Adresses IP de la passerelle** |**Adresses IP de la passerelle (en cours de mise hors service)** | **Adresses IP de la passerelle (mises hors service)** |
|:----------------|:-------------------------|:-------------------------------------------|:------------------------------------------|
| Centre de l’Australie| 20.36.105.0  | | |
| Australie Centre 2     | 20.36.113.0  | | |
| Australie Est | 13.75.149.87, 40.79.161.1     |  | |
| Sud-Est de l’Australie |191.239.192.109, 13.73.109.251   |  | |
| Brésil Sud |191.233.201.8, 191.233.200.16    |  | 104.41.11.5|
| Centre du Canada |40.85.224.249  | | |
| Est du Canada | 40.86.226.166    | | |
| USA Centre | 23.99.160.139, 52.182.136.37, 52.182.136.38 | 13.67.215.62 | |
| Chine orientale | 139.219.130.35    | | |
| Chine orientale 2 | 40.73.82.1  | | |
| Chine du Nord | 139.219.15.17    | | |
| Chine Nord 2 | 40.73.50.0     | | |
| Asie Est | 191.234.2.139, 52.175.33.150, 13.75.33.20, 13.75.33.21     | | |
| USA Est |40.71.8.203, 40.71.83.113 |40.121.158.30|191.238.6.43 |
| USA Est 2 | 40.70.144.38, 52.167.105.38  | 52.177.185.181 | |
| France Centre | 40.79.137.0, 40.79.129.1  | | |
| France Sud | 40.79.177.0     | | |
| Centre de l’Allemagne | 51.4.144.100     | | |
| Nord-Est de l’Allemagne | 51.5.144.179  | | |
| Inde Centre | 104.211.96.159     | | |
| Sud de l’Inde | 104.211.224.146  | | |
| Inde Ouest | 104.211.160.80    | | |
| Japon Est | 40.79.192.23, 40.79.184.8 | 13.78.61.196 | |
| OuJapon Est | 191.238.68.11, 40.74.96.6, 40.74.96.7     | 104.214.148.156 | |
| Centre de la Corée | 52.231.17.13   | 52.231.32.42 | |
| Corée du Sud | 52.231.145.3     | 52.231.200.86 | |
| Centre-Nord des États-Unis | 52.162.104.35, 52.162.104.36    | 23.96.178.199 | |
| Europe Nord | 52.138.224.6, 52.138.224.7  | 40.113.93.91 |191.235.193.75 |
| Afrique du Sud Nord  | 102.133.152.0    | | |
| Afrique du Sud Ouest | 102.133.24.0   | | |
| États-Unis - partie centrale méridionale |104.214.16.39, 20.45.120.0  |13.66.62.124  |23.98.162.75 |
| Asie Sud-Est | 40.78.233.2, 23.98.80.12     | 104.43.15.0 | |
| Émirats arabes unis Centre | 20.37.72.64  | | |
| Émirats arabes unis Nord | 65.52.248.0    | | |
| Sud du Royaume-Uni | 51.140.184.11   | | |
| Ouest du Royaume-Uni | 51.141.8.11  | | |
| Centre-USA Ouest | 13.78.145.25     | | |
| Europe Ouest |13.69.105.208, 104.40.169.187 | 40.68.37.158 | 191.237.232.75 |
| USA Ouest |13.86.216.212, 13.86.217.212 |104.42.238.205  | 23.99.34.75|
| USA Ouest 2 | 13.66.226.202  | | |
||||

## <a name="connection-redirection"></a>Redirection de connexion

Azure Database for MariaDB prend en charge une stratégie de connexion supplémentaire, la **redirection**, qui permet de réduire la latence réseau entre les applications clientes et les serveurs MariaDB. Avec cette fonctionnalité, une fois que la session TCP initiale est établie au serveur Azure Database for MariaDB, le serveur retourne l’adresse back-end du nœud qui héberge le serveur MariaDB au client. Par la suite, les paquets suivants sont directement acheminés vers le serveur, en ignorant la passerelle. Étant donné que les paquets vont directement au serveur, la latence et le débit améliorent les performances.

Cette fonctionnalité est prise en charge dans les serveurs Azure Database for MariaDB avec les versions de moteur 10.2 et 10.3.

La prise en charge de la redirection est disponible dans l’extension [PHP mysqlnd_azure](https://github.com/microsoft/mysqlnd_azure), développée par Microsoft et est disponible sur [PECL](https://pecl.php.net/package/mysqlnd_azure). Pour plus d’informations sur l’utilisation de la redirection dans vos applications, consultez l’article [configuration de la redirection](./howto-redirection.md).

> [!IMPORTANT]
> La prise en charge de la redirection dans l’extension [mysqlnd_azure](https://github.com/microsoft/mysqlnd_azure) PHP est actuellement disponible en préversion.

## <a name="next-steps"></a>Étapes suivantes

* [Créer et gérer des règles de pare-feu Azure Database for MariaDB à l’aide du portail Azure](./howto-manage-firewall-portal.md)
* [Create and manage Azure Database for MariaDB firewall rules using Azure CLI](./howto-manage-firewall-cli.md) (Créer et gérer des règles de pare-feu Azure Database for MariaDB à l’aide de l’interface de ligne de commande Azure)
