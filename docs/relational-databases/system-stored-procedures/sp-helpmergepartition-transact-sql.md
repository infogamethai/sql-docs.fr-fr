---
title: sp_helpmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepartition
- sp_helpmergepartition_TSQL
helpviewer_keywords:
- sp_helpmergepartition
ms.assetid: 184188cc-f519-445d-97ce-aae38f1eb550
author: stevestein
ms.author: sstein
ms.openlocfilehash: 01155b1fb294660c92bfa975bc04de8f748b730f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137661"
---
# <a name="sphelpmergepartition-transact-sql"></a>sp_helpmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retourne des informations de partition pour la publication de fusion spécifiée. Cette procédure stockée est exécutée sur n'importe quelle base de données du serveur de publication.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_helpmergepartition [ @publication= ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]  
    [ , [ @host_name = ] 'host_name' ]  
```  
  
## <a name="arguments"></a>Arguments  
`[ @publication = ] 'publication'` Est le nom de la publication. *publication* est **sysname**, sans valeur par défaut.  
  
`[ @suser_sname = ] 'suser_sname'` Valeur SUSER_SNAME permet de définir une partition. *SUSER_SNAME* est **sysname**, avec NULL comme valeur par défaut. Précisez ce paramètre pour limiter le jeu de résultats aux seules partitions dans lesquelles SUSER_SNAME correspond à la valeur fournie.  
  
> [!NOTE]  
>  Lorsque *suser_sname* est fourni, *host_name* doit être NULL  
  
`[ @host_name = ] 'host_name'` La valeur HOST_NAME est utilisée pour définir une partition. *HOST_NAME* est **sysname**, avec NULL comme valeur par défaut. Précisez ce paramètre pour limiter le jeu de résultats aux seules partitions dans lesquelles HOST_NAME correspond à la valeur fournie.  
  
> [!NOTE]  
>  Lorsque *suser_sname* est fourni, *host_name* doit être NULL  
  
## <a name="result-sets"></a>Jeux de résultats  
  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**partition**|**int**|Identifie la partition de l'Abonné.|  
|**host_name**|**sysname**|Valeur utilisée lors de la création de la partition pour un abonnement qui est filtré par la valeur de la [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) fonction sur l’abonné.|  
|**SUSER_SNAME**|**sysname**|Valeur utilisée lors de la création de la partition pour un abonnement qui est filtré par la valeur de la [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) fonction sur l’abonné.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Emplacement de l'instantané des données filtrées pour la partition de l'Abonné.|  
|**date_refreshed**|**datetime**|Date de la dernière exécution du travail d'instantané visant à générer l'instantané de données filtrées pour la partition.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|Identifie le travail qui crée l'instantané de données filtrées pour une partition.|  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 **0** (réussite) ou **1** (échec)  
  
## <a name="remarks"></a>Notes  
 **sp_helpmergepartition** est utilisé dans la réplication de fusion.  
  
## <a name="permissions"></a>Autorisations  
 Seuls les membres de la **sysadmin** rôle serveur fixe et le **db_owner** rôle de base de données fixe peuvent exécuter **sp_helpmergepartition**.  
  
## <a name="see-also"></a>Voir aussi  
 [sp_addmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_dropmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)  
  
  
