---
title: sys.dm_hadr_cluster (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster
- dm_hadr_cluster_HADR
- sys.dm_hadr_cluster_TSQL
- dm_hadr_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: 13ce70e4-9d43-4a80-a826-099e6213bf85
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e2d58132b71e16f31e7369ae8f5b09fa3dac240f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900659"
---
# <a name="sysdmhadrcluster-transact-sql"></a>sys.dm_hadr_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Si le nœud de Clustering de basculement Windows Server (WSFC) qui héberge une instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qui est activé pour [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] possède un quorum WSFC, **sys.dm_hadr_cluster** retourne une ligne qui expose le nom du cluster et les informations sur le quorum. Si le nœud WSFC n’a aucun quorum, aucune ligne n’est retournée.  
 > [!TIP]
 > À compter de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], cette vue de gestion dynamique prend en charge le basculement Instances de Cluster AlwaysOn en plus des groupes de disponibilité AlwaysOn.

|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar(128)**|Nom du cluster WSFC qui héberge les instances de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] activées pour [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**quorum_type**|**tinyint**|Type de quorum utilisé par ce cluster WSFC, prend l'une des valeurs suivantes :<br /><br /> 0 = Nœud majoritaire. Cette configuration de quorum permet de faire face aux échecs de la moitié des nœuds (arrondi) moins un. Par exemple, sur un cluster à sept nœuds, cette configuration de quorum peut faire face aux échecs de trois nœuds.<br /><br /> 1 = Nœud et disque majoritaire. Si le disque témoin reste en ligne, cette configuration de quorum peut faire face aux échecs de la moitié des nœuds (arrondi). Par exemple, un cluster à six nœuds dans lequel le disque témoin est en ligne peut faire face aux échecs de trois nœuds. Si le disque témoin est mis hors connexion ou échoue, cette configuration de quorum peut faire face aux échecs de la moitié des nœuds (arrondi) moins un. Par exemple, un cluster à six nœuds avec un disque témoin défectueux peut faire face aux échecs de deux nœuds (3-1 = 2).<br /><br /> 2 = Nœud et partage de fichiers majoritaires. Cette configuration de quorum s'exécute de façon similaire à la configuration Nœud et disque majoritaires, mais utilise un témoin de partage de fichiers au lieu d'un disque témoin.<br /><br /> 3 = aucune majorité : Disque uniquement. Si le disque quorum est en ligne, cette configuration de quorum peut faire face aux échecs de tous les nœuds sauf un.<br /><br /> 4 = Quorum inconnu. Quorum inconnu pour le cluster.<br /><br /> 5 = témoin de cloud. Cluster utilise Microsoft Azure pour l’arbitrage de quorum. Si le témoin de cloud est disponible, le cluster peut soutenir l’échec de la moitié des nœuds (arrondi).|  
|**quorum_type_desc**|**varchar(50)**|Description de **quorum_type**, l’un des :<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY:_DISK_ONLY <br /><br /> UNKNOWN_QUORUM <br /><br /> CLOUD_WITNESS|  
|**quorum_state**|**tinyint**|État du quorum WSFC, peut prendre l'une des valeurs suivantes :<br /><br /> 0 = état de quorum inconnu<br /><br /> 1 = quorum normal<br /><br /> 2 = quorum forcé|  
|**quorum_state_desc**|**varchar(50)**|Description de **quorum_state**, l’un des :<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## <a name="permissions"></a>Autorisations  
 requièrent l'autorisation VIEW SERVER STATE sur le serveur.  
  
## <a name="see-also"></a>Voir aussi  
 [Vues et fonctions de gestion dynamiques de groupes de disponibilité Always On &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Affichages catalogue des groupes de disponibilité Always On &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Surveiller des groupes de disponibilité &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
