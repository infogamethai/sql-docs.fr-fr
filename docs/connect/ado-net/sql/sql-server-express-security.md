---
title: Sécurité de SQL Server Express
description: Décrit les considérations en matière de sécurité pour SQL Server Express.
ms.date: 09/26/2019
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 9d6b711109f7d94e3bca8d9cf2bda6d2c124c798
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452021"
---
# <a name="sql-server-express-security"></a>Sécurité de SQL Server Express

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Télécharger ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition (SQL Server Express) repose sur Microsoft SQL Server et prend en charge la plupart des fonctionnalités du moteur de base de données. Il est conçu de sorte que les fonctionnalités non essentielles et la connectivité réseau soient désactivées par défaut. Cela réduit la surface d’exposition disponible pour les attaques par un utilisateur malveillant.  
  
SQL Server Express est généralement installé en tant qu’instance nommée. Le nom par défaut de l’instance est `SQLExpress`. Une instance nommée est identifiée par le nom réseau de l’ordinateur plus le nom de l’instance que vous spécifiez pendant l’installation.  
  
## <a name="network-access"></a>Accès réseau  
Pour des raisons de sécurité, les protocoles réseau sont désactivés par défaut dans SQL Server Express. Cela empêche les attaques d’utilisateurs extérieurs qui peuvent compromettre l’ordinateur qui héberge l’instance de SQL Server Express. Vous devez explicitement activer la connectivité réseau et démarrer le service SQL Server Browser pour vous connecter à une instance de SQL Server Express à partir d’un autre ordinateur.  
  
Une fois la connectivité réseau activée, une instance de SQL Server Express a les mêmes exigences de sécurité que les autres éditions de SQL Server.  
  
## <a name="user-instances"></a>Instances utilisateur  
Une instance utilisateur est une instance distincte du moteur de base de données SQL Server Express qui est générée par une instance parente de SQL Server Express. L’objectif principal d’une instance utilisateur est de permettre aux utilisateurs qui exécutent Windows dans le cadre d’un compte d’utilisateur doté de privilèges minimum d’avoir des privilèges d’administrateur système (`sysadmin`) sur l’instance de SQL Server Express sur leur ordinateur local. Les instances utilisateur ne sont pas destinées aux utilisateurs qui sont des administrateurs système sur leurs propres ordinateurs.  
  
Une instance utilisateur est générée à partir d’une instance principale de SQL Server ou SQL Server Express pour le compte d’un utilisateur. Il s’exécute en tant que processus utilisateur dans le contexte de sécurité Windows de l’utilisateur, pas en tant que service. Les connexions SQL Server ne sont pas autorisées ; seules les connexions Windows sont prises en charge. Cela empêche les logiciels en cours d’exécution sur une instance utilisateur d’apporter des modifications à l’ensemble du système que l’utilisateur ne serait pas autorisé à effectuer. Une instance utilisateur est également appelée instance enfant ou client, et est parfois appelée à l’aide de l’acronyme RANU (« exécuter en tant qu’utilisateur normal »).  
  
Chaque instance utilisateur est isolée de son instance parente et des autres instances utilisateur s’exécutant sur le même ordinateur. Les bases de données installées sur des instances utilisateur sont ouvertes en mode mono-utilisateur uniquement. plusieurs utilisateurs ne peuvent pas s’y connecter. La réplication, les requêtes distribuées et les connexions à distance sont désactivées pour les instances utilisateur. En cas de connexion à une instance utilisateur, les utilisateurs ne disposent pas de privilèges spéciaux sur l’instance de SQL Server Express parente.  
  
## <a name="external-resources"></a>Ressources externes  
Pour plus d’informations sur SQL Server Express, consultez les ressources suivantes.  
  
|||  
|-|-|  
|[Documentation en ligne de SQL Server 2005 Express Edition](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|Documentation complète pour SQL Server 2005 Express Edition.|  
|[Instances d’utilisateur pour les non-administrateurs](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms143684(v=sql.100)) dans la Documentation en ligne de SQL Server|Décrit comment créer et déployer des instances utilisateur.|  
|[Instances d’utilisateur SQL Server Express](sql-server-express-user-instances.md)|Décrit les fonctionnalités de l’instance utilisateur dans une application ADO.NET. Fournit des informations sur l’activation d’une instance utilisateur, la connexion à une instance utilisateur à l’aide d’une <xref:Microsoft.Data.SqlClient.SqlConnection>, la durée de vie d’une instance utilisateur et les scénarios d’instance utilisateur.|  
  
## <a name="next-steps"></a>Étapes suivantes
- [Sécurité de SQL Server](sql-server-security.md)
- [Instances d’utilisateur SQL Server Express](sql-server-express-user-instances.md)
