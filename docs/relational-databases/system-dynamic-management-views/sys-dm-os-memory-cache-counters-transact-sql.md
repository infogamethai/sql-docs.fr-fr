---
title: sys.dm_os_memory_cache_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_counters_TSQL
- dm_os_memory_cache_counters_TSQL
- sys.dm_os_memory_cache_counters
- dm_os_memory_cache_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_counters dynamic management view
ms.assetid: ca7bd036-d661-4c17-b00a-e1a975bd8932
author: stevestein
ms.author: sstein
ms.openlocfilehash: 755e0cdbf5bff5bcd9c048a2f77918dc9a6eb2a3
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982528"
---
# <a name="sysdm_os_memory_cache_counters-transact-sql"></a>sys.dm_os_memory_cache_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retourne un instantané de l'état d'un cache dans [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **sys. dm_os_memory_cache_counters** fournit des informations au moment de l’exécution sur les entrées du cache allouées, leur utilisation et la source de mémoire pour les entrées du cache.  
  
> **Remarque :** Pour l’appeler à partir de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], utilisez le nom **sys. dm_pdw_nodes_os_memory_cache_counters**.  
  
|Nom de colonne|Data type|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Indique l'adresse (clé primaire) des compteurs associés à un cache en particulier. N'accepte pas la valeur NULL.|  
|**nom**|**nvarchar (256)**|Spécifie le nom du cache. N'accepte pas la valeur NULL.|  
|**type**|**nvarchar(60)**|Indique le type de cache associé à cette entrée. N'accepte pas la valeur NULL.|  
|**single_pages_kb**|**bigint**|**S'applique à**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] et [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Taille, en kilo-octets, de la mémoire monopage allouée. Il s'agit de la quantité de mémoire allouée au moyen de l'allocateur monopage. Cela fait référence aux pages de 8 kilo-octets prélevées directement dans le pool de mémoires tampons de ce cache. N'accepte pas la valeur NULL.|  
|**pages_kb**|**bigint**|**S’applique à** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] et versions ultérieures.<br /><br /> Spécifie la taille, en kilo-octets, de la mémoire allouée dans le cache. N'accepte pas la valeur NULL.|  
|**multi_pages_kb**|**bigint**|**S'applique à**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] et [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Taille, en kilo-octets, de la mémoire multipage allouée. Il s'agit de la quantité de mémoire allouée à l'aide de l'allocateur de pages multiples du nœud de mémoire. Cette mémoire est allouée en dehors du pool de mémoires tampons ; elle tire parti de l'allocateur virtuel des nœuds mémoire. N'accepte pas la valeur NULL.|  
|**pages_in_use_kb**|**bigint**|**S’applique à** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] et versions ultérieures.<br /><br /> Spécifie la taille, en kilo-octets, de la mémoire allouée et en cours d'utilisation dans le cache. Autorise la valeur NULL.  Les valeurs pour les objets de type `USERSTORE_<*>` ne font pas l'objet d'un suivi.  NULL est retourné pour chacune d'entre elles.|  
|**single_pages_in_use_kb**|**bigint**|**S'applique à**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] et [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Taille, en kilo-octets, de la mémoire monopage utilisée. Autorise la valeur NULL. Ces informations ne sont pas suivies pour les objets de type USERSTORE_\<* > et ces valeurs sont NULL.|  
|**multi_pages_in_use_kb**|**bigint**|**S'applique à**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] et [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Taille, en kilo-octets, de la mémoire multipage utilisée. Accepte la valeur NULL. Ces informations ne sont pas suivies pour les objets de type USERSTORE_\<* >, et ces valeurs sont NULL.|  
|**entries_count**|**bigint**|Indique le nombre d'entrées dans le cache. N'accepte pas la valeur NULL.|  
|**entries_in_use_count**|**bigint**|Indique le nombre d'entrées dans le cache en cours d'utilisation. N'accepte pas la valeur NULL.|  
|**pdw_node_id**|**int**|**S’applique à**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificateur du nœud sur lequel cette distribution se trouve.|  
  
## <a name="permissions"></a>Autorisations 

Sur [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiert `VIEW SERVER STATE` autorisation.   
Sur les niveaux [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium, requiert l’autorisation `VIEW DATABASE STATE` dans la base de données. Sur [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveaux standard et de base, nécessite l' **administrateur du serveur** ou un compte d' **administrateur Azure Active Directory** .   

## <a name="see-also"></a>Voir aussi  
  [SQL Server les vues &#40;de gestion dynamique associées au système d’exploitation Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


