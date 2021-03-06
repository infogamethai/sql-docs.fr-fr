---
title: sys.database_service_objectives
titleSuffix: Azure SQL Database
ms.custom: seo-dt-2019
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- Pool élastique
- Pool élastique, gestion
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 465416e87966ba3a80c8e98394c0b1f2009f591b
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844460"
---
# <a name="sysdatabase_service_objectives-azure-sql-database"></a>sys. database_service_objectives (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Retourne l’édition (niveau de service), l’objectif de service (niveau tarifaire) et le nom du pool élastique, le cas échéant, pour une base de données SQL Azure ou un Azure SQL Data Warehouse. Si vous êtes connecté à la base de données Master dans un serveur Azure SQL Database, retourne des informations sur toutes les bases de données. Pour Azure SQL Data Warehouse, vous devez être connecté à la base de données Master.  
  
  
 Pour plus d’informations sur la tarification, consultez [options et performances de SQL Database : tarification SQL Database](https://azure.microsoft.com/pricing/details/sql-database/) et [tarification des SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).  
  
 Pour modifier les paramètres du service, consultez [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md) et [alter Database (Azure SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest).  
  
 La vue sys. database_service_objectives contient les colonnes suivantes.  
  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|database_id|int|ID de la base de données, unique au sein d’une instance de Azure SQL Database Server. Rejoignable avec [sys. databases &#40;Transact-&#41;SQL](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|édition|sysname|Niveau de service de la base de données ou de l’entrepôt de données : de **base**, **standard**, **Premium** ou **Data Warehouse**.|  
|service_objective|sysname|Niveau tarifaire de la base de données. Si la base de données se trouve dans un pool élastique, retourne **ElasticPool**.<br /><br /> Sur le niveau de **base** , retourne de **base**.<br /><br /> **Une seule base de données dans un niveau de service standard** retourne l’un des éléments suivants : S0, S1, S2, S3, S4, S6, S7, S9 ou S12.<br /><br /> **Une seule base de données dans un niveau Premium** retourne les éléments suivants : P1, P2, P4, P6, P11 ou P15.<br /><br /> **SQL Data Warehouse** retourne DW100 via DW30000c.<br /><br /> Pour plus d’informations, consultez [bases de données uniques](/azure/sql-database/sql-database-dtu-resource-limits-single-databases/), [Pools élastiques](/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools/), [entrepôts de données](/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu/) .|  
|elastic_pool_name|sysname|Nom du [pool élastique](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) auquel appartient la base de données. Retourne **null** si la base de données est une base de données unique ou un warehoue de données.|  
  
## <a name="permissions"></a>Autorisations  
 Nécessite l’autorisation **dbManager** sur la base de données Master.  Au niveau de la base de données, l’utilisateur doit être le créateur ou le propriétaire.  
  
## <a name="examples"></a>Exemples  
 Cet exemple peut être exécuté sur la base de données Master ou sur Azure SQL Database bases de données utilisateur. La requête renvoie les informations sur le nom, le service et le niveau de performance de la ou des bases de données.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
