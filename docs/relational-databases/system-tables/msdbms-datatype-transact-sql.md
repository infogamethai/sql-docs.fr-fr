---
title: MSdbms_datatype (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
author: stevestein
ms.author: sstein
ms.openlocfilehash: 301aa5af9aa34031f381235341f1e7d461675432
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907515"
---
# <a name="msdbmsdatatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Le **MSdbms_datatype** table contient la liste complète des types de données natifs sur chaque système de gestion prises en charge de la base de données (SGBD) utilisé comme un serveur de publication ou un abonné dans la réplication de bases de données hétérogènes. Cette table est stockée dans le **msdb** base de données.  
  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|Identifie chaque type de données unique.|  
|**dbms_id**|**int**|Identifie le SGBD auquel appartient le type.|  
|**type**|**sysname**|Nom du type de données (natif).|  
|**createparams**|**int**|Bitmap qui décrit la combinaison de longueur, précision et échelle applicable à chaque type de données, à savoir :<br /><br /> **0 x 1** = précision.<br /><br /> **0 x 2** = mise à l’échelle.<br /><br /> **0 x 4** = longueur.|  
  
## <a name="remarks"></a>Notes  
 Cette table contient des entrées pour les types de données SQL Server, car une instance de SQL Server peut s’abonner à une base de données non SQL Server et publier vers un abonné non SQL Server.  
  
## <a name="see-also"></a>Voir aussi  
 [Réplication de base de données hétérogène](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Spécifier des mappages de types de données pour un serveur de publication Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tables de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vues de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
