---
title: sp_schemafilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_schemafilter_TSQL
- sp_schemafilter
helpviewer_keywords:
- sp_schemafilter
ms.assetid: 199e869b-2cd2-44ee-b2ee-69edb06a1bc4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 231796d1678a19106eb89f3039cd755e8385082c
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73633015"
---
# <a name="sp_schemafilter-transact-sql"></a>sp_schemafilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifie et affiche des informations sur le schéma exclus lors de l'affichage de la liste des tables Oracle qui peuvent être publiées.  
  
 ![Icône Lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône Lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_schemafilter [ @publisher = ] 'publisher'   
   [ , [ @schema = ] 'schema' ]   
   [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>Arguments  
`[ @publisher = ] 'publisher'` est le nom du serveur de publication non [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Publisher* est de **type sysname**, sans valeur par défaut.  
  
`[ @schema = ] 'schema'` est le nom du schéma. *Schema* est de **type sysname**, avec NULL comme valeur par défaut.  
  
`[ @operation = ] 'operation'` est l’action à effectuer sur ce schéma. *operation* est de type **nvarchar (4)** et peut prendre l’une des valeurs suivantes.  
  
|Value|Description|  
|-----------|-----------------|  
|**complémentaires**|Ajoute le schéma spécifié à la liste des schémas qui ne peuvent pas être publiés.|  
|**Déplacez**|Supprime le schéma spécifié de la liste des schémas qui ne peuvent pas être publiés.|  
|**Aide**|Retourne la liste de schémas qui ne peuvent pas être publiés.|  
  
## <a name="result-sets"></a>Jeux de résultats  
  
|Nom de colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**SchemaName**|**sysname**|Nom du schéma dont la publication n'est pas admise.|  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 **0** (succès) ou **1** (échec)  
  
## <a name="remarks"></a>Notes  
 **sp_schemafilter** ne doit être utilisé que pour les serveurs de publication hétérogènes.  
  
## <a name="permissions"></a>Autorisations  
 Seuls les membres du rôle serveur fixe **sysadmin** sur le serveur de distribution peuvent exécuter **sp_schemafilter**.  
  
## <a name="see-also"></a>Voir aussi  
 [Procédures stockées de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
