---
title: Attacher et détacher une base de données (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [SQL Server], detaching
- detach database [SQL Server]
- databases [SQL Server], attaching
- removing databases
- transaction logs [SQL Server], detaching
- databases [SQL Server], removing
- restoring [SQL Server], attached databases
- transaction logs [SQL Server], attaching
- differential backups, after detaching
- moving databases
- attach database [SQL Server]
- detaching databases [SQL Server]
- differential base [SQL Server]
- attaching databases [SQL Server]
- databases [SQL Server], moving
ms.assetid: d0de0639-bc54-464e-98b1-6af22a27eb86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5eae331b064d83510d657f6f09a819955e6259a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62762417"
---
# <a name="database-detach-and-attach-sql-server"></a>Attacher et détacher une base de données (SQL Server)
  Les données et les journaux de transactions d'une base de données peuvent être détachés, puis rattachés à la même instance ou à une autre instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le détachement et l'attachement d'une base de données sont utiles pour transférer la base de données dans une instance différente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sur le même ordinateur ou pour la déplacer.  
  
 Le format de stockage sur disque de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] est le même dans les environnements 64 bits et 32 bits. Par conséquent, l'attachement fonctionne sur les environnements 32 bits et 64 bits.  Une base de données détachée d'une instance de serveur s'exécutant dans un environnement peut être attachée à une instance de serveur qui s'exécute dans un autre environnement.  
  
  
  
##  <a name="Security"></a> Sécurité  
 Les autorisations d'accès au fichier sont définies au cours de plusieurs opérations de base de données, notamment le détachement ou l'attachement d'une base de données.  
  
> [!IMPORTANT]  
>  Nous vous recommandons de ne pas attacher ni restaurer de bases de données provenant de sources inconnues ou non approuvées. Ces bases de données peuvent contenir du code malveillant susceptible d'exécuter du code [!INCLUDE[tsql](../../includes/tsql-md.md)] indésirable ou de provoquer des erreurs en modifiant le schéma ou la structure physique des bases de données. Avant d’utiliser une base de données issue d’une source inconnue ou non approuvée, exécutez [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) sur la base de données sur un serveur autre qu’un serveur de production et examinez également le code, notamment les procédures stockées ou le code défini par l’utilisateur, de la base de données.  
  
##  <a name="DetachDb"></a> Détachement d'une base de données  
 Détacher une base de données consiste à la supprimer de l'instance [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sans toucher à ses fichiers de données et à ses journaux de transactions. Ces fichiers peuvent ensuite servir à rattacher la base de données à n'importe quelle instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y compris le serveur d'où la base de données a été détachée.  
  
 Une base de données ne peut pas être détachée si l'une des conditions suivantes est vraie :  
  
-   La base de données est répliquée et publiée. Si elle est répliquée, la base de données ne doit pas être publiée. Avant de pouvoir la détacher, vous devez désactiver la publication en exécutant [sp_replicationdboption](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql).  
  
    > [!NOTE]  
    >  Si vous ne pouvez pas utiliser **sp_replicationdboption**, vous pouvez supprimer la réplication en exécutant [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql).  
  
-   Un instantané existe sur la base de données.  
  
     Avant de pouvoir détacher la base de données, vous devez supprimer tous ses instantanés. Pour plus d’informations, consultez [Supprimer un instantané de base de données &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md).  
  
    > [!NOTE]  
    >  Un instantané de base de données ne peut pas être détaché ni attaché.  
  
-   La base de données est en cours de mise en miroir dans une session de mise en miroir de bases de données.  
  
     La base de données ne peut pas être détachée tant que la session n'est pas interrompue. Pour plus d’informations, consultez [Suppression d’une mise en miroir des bases de données &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
-   La base de données est suspecte. Une base de données suspecte ne peut pas être détachée ; avant de pouvoir le faire, vous devez la mettre en mode urgence. Pour plus d’informations sur la manière de mettre une base de données en mode urgence, consultez [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
-   La base de données est une base de données système.  
  
### <a name="backup-and-restore-and-detach"></a>Sauvegarde et restauration et détachement  
 Le détachement d'une base de données en lecture seule provoque la perte des informations relatives aux bases différentielles des sauvegardes différentielles. Pour plus d’informations, consultez [Sauvegardes différentielles &#40;SQL Server&#41;](../backup-restore/differential-backups-sql-server.md).  
  
### <a name="responding-to-detach-errors"></a>Réponse aux erreurs de détachement  
 Les erreurs générées à l'occasion du détachement d'une base de données peuvent empêcher la fermeture correcte de la base de données et la reconstruction du journal des transactions. Si vous obtenez un message d'erreur, procédez comme suit pour corriger le problème :  
  
1.  Rattachez tous les fichiers associés à la base de données, en plus du fichier primaire.  
  
2.  Résolvez le problème à l'origine de l'affichage du message d'erreur.  
  
3.  Détachez la base de données de nouveau.  
  
##  <a name="AttachDb"></a> Attachement d'une base de données  
 Vous pouvez attacher une base de données [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copiée ou détachée. Lorsque vous attachez un [!INCLUDE[ssVersion2005](../../includes/sscurrent-md.md)] instance de serveur, les fichiers catalogue sont attachés à partir de leur emplacement précédent avec les autres fichiers de base de données, les mêmes que dans [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Pour plus d’informations, consultez [Mise à niveau de la fonction de recherche en texte intégral](../search/upgrade-full-text-search.md).  
  
 Lorsque vous attachez une base de données, tous les fichiers de données (fichiers MDF et NDF) doivent être disponibles. Si un fichier de données possède un chemin différent de celui qui existait lorsque la base de données a été créée pour la première fois ou attachée pour la dernière fois, vous devez spécifier le chemin actuel du fichier.  
  
> [!NOTE]  
>  Si le fichier de données primaires attaché est en lecture seule, le [!INCLUDE[ssDE](../../includes/ssde-md.md)] suppose que la base de données est en lecture seule.  
  
 Quand une base de données chiffrée est d’abord attaché à une instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], le propriétaire de la base de données doit ouvrir la clé principale de la base de données en exécutant l’instruction suivante : OPEN MASTER KEY DÉCHIFFREMENT PAR MOT DE PASSE = **' *`password`* '** . Nous vous recommandons d’activer le déchiffrement automatique de la clé principale en exécutant l’instruction suivante : ALTER MASTER KEY ADD CHIFFREMENT PAR CLÉ PRINCIPALE DU SERVICE. Pour plus d’informations, consultez [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql) et [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql).  
  
 Les conditions requises pour attacher des fichiers journaux dépendent en partie des autorisations de lecture-écriture ou de lecture seule de la base de données. Elles sont exposées ci-dessous.  
  
-   Pour une base de données en lecture-écriture, vous pouvez généralement attacher un fichier journal dans un nouvel emplacement. Toutefois, dans certains cas, le rattachement d'une base de données nécessite ses fichiers journaux existants. Par conséquent, il est important de toujours conserver tous les fichiers journaux détachés tant que la base de données n'a pas été attachée sans eux.  
  
     Si une base de données en lecture-écriture possède un seul fichier journal dont vous ne précisez pas le nouvel emplacement, l'opération d'attachement le recherche dans son emplacement précédent. S'il est trouvé, l'ancien fichier journal est utilisé, que la base de données ait été fermée correctement ou non. Toutefois, si l'ancien fichier journal n'est pas trouvé et si la base de données a été fermée correctement sans séquence de journaux de transactions active, l'opération d'attachement tente de créer un nouveau fichier journal pour la base de données.  
  
-   Si le fichier de données primaire qui est attaché est en lecture seule, le [!INCLUDE[ssDE](../../includes/ssnoversion-md.md)] Impossible de mettre à jour l’emplacement du journal stockée dans le fichier primaire.  
  
  
  
###  <a name="Metadata"></a> Modifications des métadonnées lors de l'attachement d'une base de données  
 Lorsqu'une base de données en lecture seule est détachée puis rattachée, les informations de sauvegarde sur la base différentielle active sont perdues. La *base différentielle* est la sauvegarde complète la plus récente de toutes les données de la base de données ou d'un sous-ensemble des fichiers ou groupes de fichiers de la base de données. Sans les informations de sauvegarde de la base, la base de données **MASTER** est désynchronisée par rapport à la base de données en lecture seule ; ainsi, les sauvegardes différentielles effectuées ultérieurement peuvent produire des résultats inattendus. C'est la raison pour laquelle, si vous utilisez des sauvegardes différentielles avec une base de données en lecture seule, vous devez établir une nouvelle base différentielle en effectuant une sauvegarde complète après le rattachement de la base de données. Pour plus d’informations sur les sauvegardes différentielles, consultez [Sauvegardes différentielles &#40;SQL Server&#41;](../backup-restore/differential-backups-sql-server.md).  
  
 À l'attachement, la base de données démarre. En général, l'attachement d'une base de données la place dans le même état où elle se trouvait au moment de son détachement ou de sa copie. Toutefois, les opérations d'attachement et de détachement désactivent le chaînage des propriétés des bases de données croisées de la base de données. Pour plus d’informations sur l’activation du chaînage, consultez [Chaînage des propriétés des bases de données croisées (option de configuration de serveur)](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md). En outre, TRUSTWORTHY prend la valeur OFF à chaque fois que la base de données est attachée. Pour plus d’informations sur la façon d’affecter la valeur ON à TRUSTWORTHY, consultez [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
### <a name="backup-and-restore-and-attach"></a>Sauvegarder, restaurer et attacher  
 Comme toutes les bases de données complètement ou partiellement hors connexion, une base de données contenant des fichiers de restauration ne peut pas être attachée. Pour attacher la base de données, arrêtez la séquence de restauration. Puis, vous pouvez redémarrer la séquence de restauration.  
  
###  <a name="OtherServerInstance"></a> Attachement d'une base de données à une autre instance de serveur  
  
> [!IMPORTANT]  
>  Une base de données créée dans une version plus récente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ne peut pas être attachée à des versions antérieures.  
  
 Lorsque vous attachez une base de données à une autre instance de serveur et si vous souhaitez offrir une expérience cohérente aux utilisateurs et aux applications, il est possible que vous deviez recréer une partie ou l'ensemble des métadonnées de la base de données, telles que les connexions et les travaux, sur cette autre instance de serveur. Pour plus d’informations, consultez [Gérer les métadonnées lors de la mise à disposition d’une base de données sur une autre instance de serveur &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md).  
  
##  <a name="RelatedTasks"></a> Tâches associées  
 **Pour détacher une base de données**  
  
-   [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
-   [Détacher une base de données](detach-a-database.md)  
  
 **Pour attacher une base de données**  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
-   [Attacher une base de données](attach-a-database.md)  
  
-   [sp_attach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-db-transact-sql)  
  
-   [sp_attach_single_file_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql)  
  
 **Pour mettre à niveau une base de données à l'aide des opérations de détachement et d'attachement**  
  
-   [Mettre à niveau une base de données avec Detach et Attach &#40;Transact-SQL&#41;](upgrade-a-database-using-detach-and-attach-transact-sql.md)  
  
 **Pour déplacer une base de données à l'aide des opérations de détachement et d'attachement**  
  
-   [Déplacer une base de données à l’aide de la méthode de détachement et d’attachement &#40;Transact-SQL&#41;](move-a-database-using-detach-and-attach-transact-sql.md)  
  
 **Pour supprimer un instantané de base de données**  
  
-   [Supprimer un instantané de base de données &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Groupes de fichiers et fichiers de base de données](database-files-and-filegroups.md)  
  
  
