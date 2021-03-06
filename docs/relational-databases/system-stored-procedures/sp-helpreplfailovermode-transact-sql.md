---
title: sp_helpreplfailovermode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
author: stevestein
ms.author: sstein
ms.openlocfilehash: b998a11acd71175e8868b669d9491822f60d2b33
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632750"
---
# <a name="sp_helpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Affiche le mode de basculement actuel d'un abonnement. Cette procédure stockée est exécutée au niveau de l'Abonné, sur n'importe quelle base de données. Pour plus d’informations sur les modes de basculement, consultez [abonnements pouvant être mis à jour pour la réplication transactionnelle](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Icône Lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône Lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>Arguments  
`[ @publisher = ] 'publisher'` est le nom du serveur de publication qui participe à la mise à jour de cet abonné. *Publisher* est de **type sysname**, sans valeur par défaut. Le serveur de publication doit déjà être configuré pour la publication.  
  
`[ @publisher_db = ] 'publisher_db'` est le nom de la base de données de publication. *publisher_db* est de **type sysname**, sans valeur par défaut.  
  
`[ @publication = ] 'publication'` est le nom de la publication qui participe à la mise à jour de cet abonné. *publication*est de **type sysname**, sans valeur par défaut.  
  
`[ @failover_mode_id = ] 'failover_mode_id' OUTPUT` retourne la valeur entière du mode de basculement et est un paramètre de **sortie** . *failover_mode_id* est de **type tinyint** , avec **0**comme valeur par défaut. Elle retourne **0** pour la mise à jour immédiate et **1** pour la mise à jour en file d’attente.  
  
`[ @failover_mode = ] 'failover_mode' OUTPUT` retourne le mode dans lequel les modifications de données sont effectuées sur l’abonné. *failover_mode* est de type **nvarchar (10),** avec NULL comme valeur par défaut. Est un paramètre de **sortie** .  
  
|Value|Description|  
|-----------|-----------------|  
|**bogage**|Mise à jour immédiate : les mises à jour réalisées sur l'Abonné sont immédiatement propagées au serveur de publication à l'aide du protocole de validation à deux phases (2PC).|  
|**en attente**|Mise à jour en attente : les mises à jour effectuées sur l'Abonné sont stockées dans une file d'attente.|  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 **0** (succès) ou **1** (échec)  
  
## <a name="remarks"></a>Notes  
 **sp_helpreplfailovermode** est utilisé dans la réplication d’instantané ou dans la réplication transactionnelle pour laquelle les abonnements sont activés pour la mise à jour immédiate avec mise à jour en file d’attente comme basculement en cas d’échec.  
  
## <a name="permissions"></a>Autorisations  
 Seuls les membres du rôle serveur fixe **sysadmin** ou du rôle de base de données fixe **db_owner** peuvent exécuter **sp_helpreplfailovermode**.  
  
## <a name="see-also"></a>Voir aussi  
 [sp_setreplfailovermode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
