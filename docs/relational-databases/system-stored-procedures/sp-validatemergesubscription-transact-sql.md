---
title: sp_validatemergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validatemergesubscription
- sp_validatemergesubscription_TSQL
helpviewer_keywords:
- sp_validatemergesubscription
ms.assetid: d73ad03c-e5b3-4606-a0ee-7d75e12762a6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 932a54323ad8f6ffafbe8ff8f4a7f3c2dc58b0e2
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632986"
---
# <a name="sp_validatemergesubscription-transact-sql"></a>sp_validatemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Effectue une validation pour l'abonnement spécifié. Cette procédure stockée est exécutée sur le serveur de publication dans la base de données de publication.  
  
 ![Icône Lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône Lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_validatemergesubscription [@publication=] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>Arguments  
`[ @publication = ] 'publication'` est le nom de la publication. *publication* est de **type sysname**, sans valeur par défaut.  
  
`[ @subscriber = ] 'subscriber'` est le nom de l’abonné. *Subscriber* est de **type sysname**, sans valeur par défaut.  
  
`[ @subscriber_db = ] 'subscriber_db'` est le nom de la base de données d’abonnement. *subscriber_db* est de **type sysname**, sans valeur par défaut.  
  
`[ @level = ] 'level'` est le type de validation à effectuer. *Level* est de **type tinyint**, sans valeur par défaut. Le paramètre « level » peut avoir l'une des valeurs suivantes :  
  
|Valeur de level (niveau)|Description|  
|-----------------|-----------------|  
|**1**|Validation du décompte de lignes uniquement.|  
|**2**|Validation du nombre de lignes et de la somme de contrôle.|  
|**3**|Validation du nombre de lignes et de la somme de contrôle binaire.|  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 **0** (succès) ou **1** (échec)  
  
## <a name="remarks"></a>Notes  
 **sp_validatemergesubscription** est utilisé dans la réplication de fusion.  
  
## <a name="permissions"></a>Autorisations  
 Seuls les membres du rôle serveur fixe **sysadmin** ou du rôle de base de données fixe **db_owner** peuvent exécuter **sp_validatemergesubscription**.  
  
## <a name="see-also"></a>Voir aussi  
 [Procédures stockées de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Valider les données répliquées](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_validatemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)  
  
  
