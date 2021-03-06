---
title: Créer une alerte à l’aide d’un niveau de gravité | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- severity levels [SQL Server]
- alerts [SQL Server], severity levels
ms.assetid: a1fd71bf-5bf9-4ce2-9a1d-032576a4a6e9
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 696527b77cba555ad5c70a8ee65c8409295d18e4
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846798"
---
# <a name="create-an-alert-using-severity-level"></a>Créer une alerte à l'aide d'un niveau de gravité
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Dans [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la plupart des fonctionnalités SQL Server Agent sont prises en charge. Pour plus d’informations, consultez [Différences T-SQL entre Azure SQL Database Managed Instance et SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Cette rubrique explique comment créer une alerte de l'Agent [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qui est déclenchée lou desqu'un événement d'un niveau de gravité spécifique a lieu dans [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] à l'aide de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="BeforeYouBegin"></a>Avant de commencer  
  
### <a name="Restrictions"></a>Limitations et restrictions  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] est un outil simple, fonctionnant en mode graphique, qui permet de gérer tout le système d'alerte. Son utilisation est recommandée pour configurer une infrastructure d'alertes.  
  
-   Les événements créés à l’aide de **xp_logevent** surviennent dans la base de données master. Ainsi, **xp_logevent** ne déclenche pas d’alerte sauf si la valeur **\@database_name** pour l’alerte est **'master'** ou NULL.  
  
-   Les niveaux de gravité compris entre 19 et 25 envoient un message [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] au journal des applications [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows et déclenchent une alerte. Les événements dont le niveau de gravité est inférieur à 19 déclenchent des alertes uniquement si vous avez utilisé **sp_altermessage**, RAISERROR WITH LOG ou **xp_logevent** pour forcer leur enregistrement dans le journal des applications Windows.  
  
### <a name="Security"></a>Sécurité  
  
#### <a name="Permissions"></a>Permissions  
Par défaut, seuls les membres du rôle serveur fixe **sysadmin** peuvent exécuter la procédure **sp_add_alert**.  
  
## <a name="SSMSProcedure"></a>Utilisation de SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-severity-level"></a>Pour créer une alerte à l'aide d'un niveau de gravité  
  
1.  Dans **l’Explorateur d'objets** , cliquez sur le signe plus (+) pour développer le serveur sur lequel vous souhaitez créer une alerte à l'aide d'un niveau de gravité.  
  
2.  Cliquez sur le signe plus (+) pour développer **Agent SQL Server**.  
  
3.  Cliquez avec le bouton droit sur **Alertes** , puis sélectionnez **Nouvelle alerte**.  
  
4.  Dans la boîte de dialogue **Nouvelle alerte** , dans la zone **Nom** , entrez un nom pour cette alerte.  
  
5.  Dans la liste **Type** , sélectionnez **Alerte d'événement SQL Server**.  
  
6.  Sous **Définition d'une alerte d'événement**, dans la liste **Nom de base de données** , sélectionnez une base de données pour restreindre l'alerte à une base de données spécifique.  
  
7.  Sous **Les alertes seront déclenchées selon**, cliquez sur **Gravité** , puis sélectionnez la gravité spécifique qui déclenchera l'alerte.  
  
8.  Activez la case à cocher correspondant à **Déclencher une alerte quand le message contient** afin de limiter l'alerte à une certaine séquence de caractères, puis entrez un mot clé ou une chaîne de caractères pour le **Texte du message**. Le nombre maximal de caractères autorisé est de 100.  
  
9. Cliquez sur **OK**.  
  
## <a name="TsqlProcedure"></a>Utilisation de Transact-SQL  
  
#### <a name="to-create-an-alert-using-severity-level"></a>Pour créer une alerte à l'aide d'un niveau de gravité  
  
1.  Dans l' **Explorateur d'objets**, connectez-vous à une instance de [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Dans la barre d'outils standard, cliquez sur **Nouvelle requête**.  
  
3.  Copiez et collez l'exemple suivant dans la fenêtre de requête, puis cliquez sur **Exécuter**.  
  
    ```  
    -- Adds an alert (Test Alert) that notifies the
    -- Alert Operator via email when an error with a 
    -- severity of 23 is detected.
    
    -- Assumes that the Alert Operator already exists 
    -- and that database mail is configured.
    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert @name=N'Test Alert', 
      @message_id = 0, 
      @severity = 23, 
      @enabled = 1, 
      @include_event_description_in = 1
    ;
    GO
    
    EXEC dbo.sp_add_notification @alert_name=N'Test Alert',
      @operator_name=N'Alert Operator',
      @notification_method=1
    ;
    GO

    ```  
  
Pour plus d’informations, consultez [sp_add_alert (Transact-SQL)](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09).  
  
