---
title: sys. availability_groups_cluster (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_cluster
- availability_groups_cluster
- availability_groups_cluster_TSQL
- sys.availability_groups_cluster_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: d0f4683f-cdf0-4227-8b68-720ffe58f158
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a9ca998a0b65fff44e71549d1dae879d73288dfb
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874269"
---
# <a name="sysavailability_groups_cluster-transact-sql"></a>sys.availability_groups_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retourne une ligne pour chaque groupe de disponibilité Always On dans le clustering de basculement Windows Server (WSFC). Chaque ligne contient les métadonnées du groupe de disponibilité du cluster WSFC.  
  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificateur unique (GUID) du groupe de disponibilité.|  
|**nom**|**sysname**|Nom du groupe de disponibilité. Il s'agit d'un nom spécifié par l'utilisateur qui doit être unique dans le cluster de basculement Windows Server (WSFC).|  
|**resource_id**|**nvarchar(40)**|ID de ressource pour la ressource de cluster WSFC.|  
|**resource_group_id**|**nvarchar(40)**|ID du groupe de ressources pour le groupe de ressources du cluster WSFC du groupe de disponibilité.|  
|**failure_condition_level**|**int**|Niveau de condition d'échec défini par l'utilisateur, en fonction duquel un basculement automatique doit être déclenché ; les valeurs possibles sont les entiers suivants :<br /><br /> 1 : spécifie qu’un basculement automatique doit être initié lorsque l’un des éléments suivants se produit : <br />-Le service [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] est inactif.<br />-Le bail du groupe de disponibilité pour la connexion au cluster de basculement WSFC expire car aucun accusé de réception n’est reçu de l’instance de serveur. Pour plus d’informations, consultez [Fonctionnement : délai d’expiration de bail Always On SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).<br /><br /> 2 : spécifie qu’un basculement automatique doit être initié lorsque l’un des éléments suivants se produit :  <br />-L’instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ne se connecte pas au cluster et le seuil de **health_check_timeout** spécifié par l’utilisateur du groupe de disponibilité est dépassé. <br />-Le réplica de disponibilité est dans un état d’échec. <br />3 : spécifie qu’un basculement automatique doit être initié sur les erreurs critiques [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] internes, telles que les verrouillages spinlock orphelins, les violations graves d’accès en écriture ou trop de vidages. Valeur par défaut. <br />4 : spécifie qu’un basculement automatique doit être initialisé sur les erreurs internes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modérées, telles qu’une condition de mémoire insuffisante persistante dans le pool de ressources interne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br />5 : spécifie qu’un basculement automatique doit être initié sur toutes les conditions d’échec qualifiées, notamment :<br />-Épuisement des threads de travail du moteur SQL. <br />-Détection d’un blocage insoluble.<br /><br /> Les niveaux de condition d’échec (1-5) s’étendent du moins restrictif, le niveau 1, au plus restrictif, le niveau 5. Un niveau de condition donné comprend tous les niveaux moins restrictifs. Par conséquent, le niveau de condition le plus strict, le niveau 5, inclut les quatre niveaux de condition moins restrictifs (1 à 4), le niveau 4 inclut les niveaux 1 à 3, et ainsi de suite.<br /><br /> Pour modifier cette valeur, utilisez l’option FAILURE_CONDITION_LEVEL de l’instruction [ALTER Availability GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|**health_check_timeout**|**int**|Délai d’attente (en millisecondes) pour la procédure stockée système [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) pour retourner les informations sur l’intégrité du serveur, avant que l’instance de serveur soit considérée comme lente ou ne répond pas. La valeur par défaut est 30 000 millisecondes (ou 30 secondes).<br /><br /> Pour modifier cette valeur, utilisez l’option HEALTH_CHECK_TIMEOUT de l’instruction [ALTER Availability GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|**automated_backup_preference**|**tinyint**|Emplacement par défaut des sauvegardes effectuées sur des bases de données de disponibilité dans ce groupe de disponibilité. Une des valeurs suivantes :<br /><br /> 0 : principal. Les sauvegardes doivent toujours avoir lieu sur le réplica principal.<br />1 : secondaire uniquement. Les sauvegardes sur un réplica secondaire sont préférables.<br />2 : préférer le réplica secondaire. Les sauvegardes sur un réplica secondaire sont préférables, mais celles sur le réplica principal sont acceptables si aucun réplica secondaire n'est disponible pour les opérations de sauvegarde. Il s'agit du comportement par défaut.<br />3 : tout réplica. Aucune préférence : les sauvegardes sont effectuées sur le réplica principal ou sur un réplica secondaire.<br /><br /> Pour plus d’informations, consultez [Secondaires actifs : sauvegarde sur les réplicas secondaires &#40;groupes de disponibilité Always On&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**automated_backup_preference_desc**|**nvarchar(60)**|Description de **automated_backup_preference**, parmi :<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> NONE|  
  
## <a name="security"></a>Sécurité  
  
### <a name="permissions"></a>Autorisations  
 Nécessite l'autorisation VIEW ANY DEFINITION sur l'instance de serveur.  
  
## <a name="see-also"></a>Voir aussi  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Groupes de disponibilité Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Surveiller des groupes de disponibilité &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Surveiller des groupes de disponibilité &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
