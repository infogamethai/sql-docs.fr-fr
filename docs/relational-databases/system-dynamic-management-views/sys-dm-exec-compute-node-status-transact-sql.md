---
title: sys. dm_exec_compute_node_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODE_STATUS_TSQL
- DM_EXEC_COMPUTE_NODE_STATUS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_compute_node_status
- sys.dm_exec_compute_node_status management view
ms.assetid: b606f91f-3a08-4a4f-bb57-32ae155b3738
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11883f7744aad3f8d483e808922a7170c8fe5391
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532764"
---
# <a name="sysdm_exec_compute_node_status-transact-sql"></a>sys.dm_exec_compute_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contient des informations supplémentaires sur les performances et l’état de tous les nœuds Polybase. Répertorie une ligne par nœud.  
  
|Column Name|Type de données|Description|Plage|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|`int`|ID numérique unique associé au nœud.|Unique sur un cluster avec montée en puissance parallèle, quel que soit le type.|  
|process_id|`int`|||  
|process_name|`nvarchar(255)`|Nom logique du nœud.|Toute chaîne de longueur appropriée.|  
|allocated_memory|`bigint`|Mémoire allouée totale sur ce nœud.||  
|available_memory|`bigint`|Quantité totale de mémoire disponible sur ce nœud.||  
|process_cpu_usage|`bigint`|Utilisation totale du processeur, en graduations.||  
|total_cpu_usage|`bigint`|Utilisation totale du processeur, en graduations.||  
|thread_count|`bigint`|Nombre total de threads en cours d’utilisation sur ce nœud.||  
|handle_count|`bigint`|Nombre total de handles en cours d’utilisation sur ce nœud.||  
|total_elapsed_time|`bigint`|Temps total écoulé depuis le démarrage ou le redémarrage du système.|Temps total écoulé depuis le démarrage ou le redémarrage du système. Si total_elapsed_time dépasse la valeur maximale d’un entier (24,8 jours en millisecondes), cela entraînera un échec de matérialisation en raison d’un dépassement de capacité. La valeur maximale en millisecondes est équivalente à 24,8 jours.|  
|is_available|`bit`|Indicateur précisant si ce nœud est disponible.||  
|sent_time|`datetime`|Dernière fois qu’un package réseau a été envoyé par ce||  
|received_time|`datetime`|Dernière fois qu’un package réseau a été envoyé par ce nœud.||  
|error_id|`nvarchar(36)`|Identificateur unique de la dernière erreur qui s’est produite sur ce nœud.||
|compute_pool_id|`int`|Identificateur unique du pool.|

## <a name="see-also"></a>Voir aussi  
 [Résolution des problèmes de Polybase avec les vues de gestion dynamique](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Fonctions et vues de gestion dynamique &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vues &#40;de gestion dynamique liées aux bases de données Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
