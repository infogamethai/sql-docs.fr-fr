---
title: Utiliser la base de données de l’ajouter à l’Assistant groupe de disponibilité (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.adddatabasewizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], databases
ms.assetid: 81e5e36d-735d-4731-8017-2654673abb88
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0be8ed6cf2a163b3c195cfb5e4e18440549b501c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62815724"
---
# <a name="use-the-add-database-to-availability-group-wizard-sql-server-management-studio"></a>Utiliser l'Assistant Ajouter une base de données au groupe de disponibilité (SQL Server Management Studio)
  Utilisez l'Assistant Ajouter une base de données au groupe de disponibilité pour ajouter une ou plusieurs bases de données à un groupe de disponibilité AlwaysOn existant.  
  
> [!NOTE]  
>  Pour plus d’informations sur l’utilisation de [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou de PowerShell pour ajouter une base de données, consultez [Ajouter une base de données à un groupe de disponibilité &#40;SQL Server&#41;](availability-group-add-a-database.md).  
  
 **Dans cette rubrique :**  
  
-   **Avant de commencer :**  
  
     [Conditions préalables requises et restrictions](#Prerequisites)  
  
     [Sécurité](#Security)  
  
-   **Pour ajouter une base de données, à l’aide de :**  [Assistant Ajouter un base de données au groupe de disponibilité (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Avant de commencer  
 Si vous n’avez jamais ajouté une base de données à un groupe de disponibilité, consultez la section « Bases de données de disponibilité » dans [prérequis, Restrictions et recommandations pour les groupes de disponibilité AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Prerequisites"></a> Conditions préalables requises, restrictions et recommandations  
  
-   Vous devez être connecté à l'instance de serveur qui héberge le réplica principal actuel.  
  
-   Si une base de données est chiffrée ou même contient une clé de chiffrement de base de données (DEK), vous ne pouvez pas utiliser [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] ou [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] pour ajouter la base de données à un groupe de disponibilité. Même si une base de données chiffrée a été déchiffrée, ses sauvegardes de fichiers journaux peuvent contenir des données chiffrées. Dans ce cas, la synchronisation complète initiale des données peut échouer sur la base de données. En effet, l'opération de journalisation de la restauration peut nécessiter le certificat utilisé par les clés de chiffrement de base de données (DEK), et le certificat peut être indisponible.  
  
     **Pour qu’une base de données déchiffrée puisse être ajoutée à un groupe de disponibilité à l’aide de l’Assistant :**  
  
    1.  Créez une sauvegarde de fichier journal de la base de données principale.  
  
    2.  Créez une sauvegarde complète de la base de données principale.  
  
    3.  Restaurez la sauvegarde de la base de données sur l'instance de serveur qui héberge le réplica secondaire.  
  
    4.  Créez une nouvelle sauvegarde du journal de la base de données primaire.  
  
    5.  Restaurez cette sauvegarde de journal sur la base de données secondaire.  
  
-   **Conditions préalables requises pour utiliser la synchronisation de données initiale complète**  
  
    -   Tous les chemins d'accès des fichiers de base de données doivent être identiques sur chaque instance de serveur qui héberge un réplica pour le groupe de disponibilité.  
  
    -   Aucun nom de base de données primaire ne peut exister sur une instance de serveur qui héberge un réplica secondaire. Cela signifie qu'aucune des nouvelles bases de données secondaires ne peut exister pour le moment.  
  
    -   Vous devez spécifier un partage réseau pour que l'assistant crée des sauvegardes et puisse y accéder. Pour le réplica principal, le compte utilisé pour démarrer le [!INCLUDE[ssDE](../../../includes/ssde-md.md)] doit disposer d'autorisations de système de fichiers en lecture et en écriture sur un partage réseau. Pour les réplicas secondaires, le compte doit disposer d'une autorisation en lecture sur le partage réseau.  
  
     Si vous ne pouvez pas utiliser l'Assistant pour effectuer la synchronisation des données initiale complète, vous devez préparer vos bases de données secondaires manuellement. Vous pouvez le faire avant ou après l'exécution de l'Assistant. Pour plus d’informations, consultez [Préparer manuellement une base de données secondaire pour un groupe de disponibilité &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Sécurité  
  
####  <a name="Permissions"></a> Autorisations  
 Requiert l'autorisation ALTER AVAILABILITY GROUP sur le groupe de disponibilité, l'autorisation CONTROL AVAILABILITY GROUP, l'autorisation ALTER ANY AVAILABILITY GROUP ou l'autorisation CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Utilisation de l'Assistant Ajouter une base de données au groupe de disponibilité (SQL Server Management Studio)  
 **Pour utiliser l'Assistant Ajouter une base de données au groupe de disponibilité**  
  
1.  Dans l'Explorateur d'objets, connectez-vous à l'instance de serveur qui héberge le réplica principal du groupe de disponibilité et développez l'arborescence du serveur.  
  
2.  Développez le nœud **Haute disponibilité AlwaysOn** et le nœud **Groupes de disponibilité** .  
  
3.  Cliquez avec le bouton droit sur le groupe de disponibilité auquel vous ajoutez une base de données, puis sélectionnez la commande **Ajouter une base de données** . Cette commande lance l'Assistant Ajouter une base de données au groupe de disponibilité.  
  
4.  Sur la page **Sélectionner les bases de données** , sélectionnez une ou plusieurs bases de données. Pour plus d’informations, consultez [sélectionner une Page de bases de données &#40;nouveau disponibilité groupe Assistant Assistant Ajouter une base de données&#41;](select-databases-page-new-availability-group-wizard-and-add-database-wizard.md).  
  
5.  Sur la page **Sélectionner la synchronisation de données initiale** , choisissez comment vous souhaitez que vos nouvelles bases de données secondaires soient créées et jointes au groupe de disponibilité. Choisissez l'une des options suivantes :  
  
    -   **Complet**  
  
         Sélectionnez cette option si votre environnement répond aux conditions requises pour démarrer automatiquement la synchronisation initiale des données (pour plus d’informations, consultez [Conditions préalables requises, restrictions et recommandations](#Prerequisites), plus haut dans cette rubrique).  
  
         Si vous sélectionnez **Complet**, après avoir créé le groupe de disponibilité, l'assistant tente de sauvegarder chaque base de données primaire et son journal des transactions sur un partage réseau et restaure les sauvegardes sur chaque instance de serveur qui héberge un réplica secondaire. L'assistant joint ensuite chaque base de données secondaire au groupe de disponibilité.  
  
         Dans le champ **Spécifier un emplacement réseau partagé accessible par tous les réplicas** , spécifiez un partage de sauvegarde dans lequel l’intégralité de l’instance de serveur qui héberge les réplicas dispose d’un accès en lecture-écriture. Les sauvegardes de journaux feront partie de votre chaîne de sauvegarde du journal. Stockez les fichiers de sauvegarde des journaux de manière appropriée.  
  
        > [!IMPORTANT]  
        >  Pour plus d’informations sur les autorisations de système de fichiers requises, consultez [Configuration préalable requise](#Prerequisites)plus haut dans cette rubrique.  
  
    -   **Joindre uniquement**  
  
         Si vous avez préparé manuellement les bases de données secondaires sur les instances de serveur qui hébergeront les réplicas secondaires, vous pouvez sélectionner cette option. L'assistant joindra les bases de données secondaires existantes au groupe de disponibilité.  
  
    -   **Ignorer la synchronisation de données initiale**  
  
         Sélectionnez cette option si vous souhaitez utiliser votre propre base de données et sauvegardes de journaux de vos bases de données primaires. Pour plus d’informations, consultez [Démarrer un mouvement de données sur une base de données secondaire AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
     Pour plus d’informations, consultez [sélectionnez la Page de synchronisation de données initiale &#40;Assistants de groupe de disponibilité AlwaysOn&#41;](select-initial-data-synchronization-page-always-on-availability-group-wizards.md).  
  
6.  Sur la page **Se connecter à des réplicas secondaires existants** , si les instances de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] qui hébergent les réplicas de disponibilité pour ce groupe de disponibilité sont toutes exécutées en tant que service dans le même compte d'utilisateur, cliquez sur **Se connecter à tous**. Si l'une des instances de serveur s'exécute en tant que service sous des comptes différents, cliquez sur le bouton **Se connecter** individuel figurant à droite du nom de chaque instance de serveur.  
  
     Pour plus d’informations, consultez [se connecter à la Page de réplicas secondaires existants &#40;Assistant Ajouter un réplica et Assistant Ajout de bases de données&#41;](connect-to-existing-secondary-replicas-page.md).  
  
7.  La page **Validation** vérifie si les valeurs que vous avez spécifiées dans cet Assistant répondent aux exigences de l'Assistant Nouveau groupe de disponibilité. Pour effectuer un changement, vous pouvez cliquer sur **Précédent** pour revenir à une page antérieure de l'assistant pour modifier une ou plusieurs valeurs. Cliquez sur **Suivant** pour revenir à la page **Validation** , puis cliquez sur **Réexécuter la validation**.  
  
     Pour plus d’informations, consultez [Page Validation &#40;Assistants de groupe de disponibilité AlwaysOn&#41;](validation-page-always-on-availability-group-wizards.md).  
  
8.  Sur la page **Résumé** , examinez vos choix pour le nouveau groupe de disponibilité. Pour apporter une modification, cliquez sur **Précédent** pour revenir à la page appropriée. Après avoir apporté la modification, cliquez sur **Suivant** pour revenir à la page **Résumé** .  
  
     Pour plus d’informations, consultez [Page Résumé &#40;Assistants de groupe de disponibilité AlwaysOn&#41;](summary-page-always-on-availability-group-wizards.md).  
  
     Si vous êtes satisfait de vos sélections, cliquez éventuellement sur Script pour créer un script des étapes que l'assistant devra exécuter. Ensuite, pour créer et configurer le nouveau groupe de disponibilité, cliquez sur **Terminer**.  
  
9. La page **État d’avancement** affiche l’état d’avancement des étapes de création du groupe de disponibilité (configuration de points de terminaison, création du groupe de disponibilité et jointure du réplica secondaire au groupe).  
  
     Pour plus d’informations, consultez [Page progression &#40;Assistants de groupe de disponibilité AlwaysOn&#41;](progress-page-always-on-availability-group-wizards.md).  
  
10. Lorsque ces étapes sont terminées, la page **Résultats** affiche le résultat de chaque étape. Si toutes ces étapes aboutissent, le nouveau groupe de disponibilité est entièrement configuré. Si l'une des étapes se solde par une erreur, vous devrez peut-être effectuer la configuration manuellement. Pour plus d'informations sur la cause d'une erreur donnée, cliquez sur le lien « Erreur » associé dans la colonne **Résultat** .  
  
     À la fin de l'Assistant, cliquez sur **Fermer** pour le quitter.  
  
     Pour plus d’informations, consultez [Page Résultats &#40;Assistants de groupe de disponibilité AlwaysOn&#41;](results-page-always-on-availability-group-wizards.md).  
  
11. Si la synchronisation initiale des données n'a pas démarré automatiquement sur toutes vos bases de données secondaires, vous devez configurer toutes les bases de données secondaires non encore jointes. Pour plus d’informations, consultez [Démarrer un mouvement de données sur une base de données secondaire AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tâches associées  
  
-   [Préparer manuellement une base de données secondaire pour un groupe de disponibilité &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Joindre une base de données secondaire à un groupe de disponibilité &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Vue d’ensemble des groupes de disponibilité AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Conditions préalables, Restrictions et recommandations pour les groupes de disponibilité AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Ajouter une base de données à un groupe de disponibilité &#40;SQL Server&#41;](availability-group-add-a-database.md)   
 [Démarrer un mouvement de données sur une base de données secondaire AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)   
 [Ajouter une base de données à un groupe de disponibilité &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
  
