---
title: MSmerge_articlehistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_articlehistory
- MSmerge_articlehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_articlehistory system table
ms.assetid: 2870e7ea-dbec-4636-9171-c2cee96018ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 96b6c2599920c8d251b6d421cc18dc43c82fe521
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907252"
---
# <a name="msmergearticlehistory-transact-sql"></a>MSmerge_articlehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Le **MSmerge_articlehistory** table suit les modifications apportées aux articles pendant une session de synchronisation de l’Agent de fusion, avec une ligne pour chaque article auquel des modifications ont été apportées. Cette table est stockée dans la base de données de distribution.  
  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**Int**|L’ID d’une session de travail de l’Agent de fusion dans le [MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) (table système).|  
|**phase_id**|**int**|La phase de la session de synchronisation, qui peut être l'une des suivantes :<br /><br /> **1** = téléchargement.<br /><br /> **2** = téléchargement.<br /><br /> **4** = nettoyage.<br /><br /> **5** = arrêt.<br /><br /> **6** = modifications de schéma.<br /><br /> **7** = BCP.|  
|**nom_article**|**sysname**|Nom de l'article auquel des modifications ont été apportées.|  
|**start_time**|**datetime**|Heure à laquelle l'Agent a débuté le traitement de l'article.|  
|**duration**|**int**|Durée en secondes pendant laquelle l'Agent a traité un article.|  
|**insertions**|**int**|Nombre d'insertions appliquées à un article spécifique durant la synchronisation. Cette valeur est incrémentée pendant le processus de synchronisation et la valeur de fin représente le nombre total.|  
|**mises à jour**|**Int**|Nombre de mises à jour appliquées à un article spécifique durant la synchronisation. Cette valeur est incrémentée pendant le processus de synchronisation et la valeur de fin représente le nombre total.|  
|**suppressions**|**Int**|Nombre de suppressions appliquées à un article spécifique durant la synchronisation. Cette valeur est incrémentée pendant le processus de synchronisation et la valeur de fin représente le nombre total.|  
|**conflits**|**Int**|Nombre de conflits qui se sont produits durant la synchronisation. Cette valeur est incrémentée pendant le processus de synchronisation et la valeur de fin représente le nombre total.|  
|**conflicts_resolved**|**int**|Nombre de conflits qui se sont produits durant la synchronisation et qui ont été résolus. Cette valeur est incrémentée pendant le processus de synchronisation et la valeur de fin représente le nombre total.|  
|**rows_retried**|**Int**|Nombre de lignes ayant subi un échec qui ont fait l'objet d'une nouvelle tentative durant la synchronisation. Cette valeur est incrémentée pendant le processus de synchronisation et la valeur de fin représente le nombre total.|  
|**percent_complete**|**decimal**|Pourcentage de la durée totale de la synchronisation que l'Agent de fusion a passé sur l'article durant une session. Cette valeur est NULL jusqu'à ce que la session soit terminée.|  
|**estimated_changes**|**Int**|Une estimation du nombre de modifications de lignes qui doivent être appliquées à l'article.|  
|**relative_cost**|**decimal**|Temps passé en secondes à appliquer les modifications à cet article par rapport à la durée totale de la session entière.|  
  
## <a name="see-also"></a>Voir aussi  
 [Tables de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
