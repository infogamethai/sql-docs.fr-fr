---
title: sp_deletetracertokenhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
author: stevestein
ms.author: sstein
ms.openlocfilehash: cf591964e5dfef0536c79b0b35e5918d4f46d972
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771142"
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Supprime les enregistrements de jeton de suivi des tables système Transact [-SQL &#40;&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) et [ &#40;MStracer_history&#41; Transact-SQL](../../relational-databases/system-tables/mstracer-history-transact-sql.md) MStracer_tokens. Cette procédure stockée est exécutée sur la base de données de publication du serveur de publication ou sur la base de données de distribution du serveur de distribution.

![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Syntaxe

```
sp_deletetracertokenhistory [ @publication = ] 'publication'
    [ , [ @tracer_id = ] tracer_id ]
    [ , [ @cutoff_date = ] cutoff_date ]
    [ , [ @publisher = ] 'publisher' ]
    [ , [ @publisher_db = ] 'publisher_db' ]
```

## <a name="arguments"></a>Arguments

`@publication= 'publication'`  
Nom de la publication dans laquelle le jeton de suivi a été inséré. Le type de données est **sysname**. Ce paramètre est obligatoire.

`[ @tracer_id= ] tracer_id`  
ID du jeton de suivi à supprimer. Le type de données est **int**. La valeur par défaut est *null*. Si la *valeur est null*, tous les jetons de suivi appartenant à la publication sont supprimés.

`[ @cutoff_date= ] cutoff_date`  
Les jetons de suivi insérés dans la publication avant cette date sont supprimés. Le type de données est **DateTime**. La valeur par défaut est *null*.

`[ @publisher= ] 'publisher'`  
Nom du serveur de publication. Le type de données est **sysname**. La valeur par défaut est *null*.

> [!NOTE]
> Ce paramètre doit être spécifié uniquement pour les serveurs [!INCLUDE[msCoName](../../includes/msconame-md.md)] de publication non- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou lors de l’exécution de la procédure stockée à partir du serveur de distribution.

`[ @publisher_db= ] 'publisher_db'`  
Nom de la base de données de publication. Le type de données est **sysname**. La valeur par défaut est NULL. Ce paramètre est ignoré si la procédure stockée est exécutée sur le serveur de publication.

> [!NOTE]
> Ce paramètre doit être spécifié lors de l’exécution de la procédure stockée à partir du serveur de distribution.

## <a name="return-code-values"></a>Valeurs des codes de retour

**0** (succès) ou **1** (échec)

## <a name="remarks"></a>Notes

**sp_deletetracertokenhistory** est utilisé dans la réplication transactionnelle.  

Une erreur se produit si vous spécifiez les paramètres *tracer_id* et *cutoff_date*.

Si vous n’exécutez pas **sp_deletetracertokenhistory** pour supprimer les métadonnées de jeton de suivi, les informations sont supprimées lors du nettoyage régulier de l’historique.

Les ID de jeton de suivi peuvent être déterminés en exécutant [sp_helptracertokens &#40;Transact&#41; -SQL](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) ou en interrogeant la table système [Transact- &#40;SQL&#41; MStracer_tokens](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) .

## <a name="permissions"></a>Autorisations

Seul le personnel suivant est habilité à exécuter **sp_deletetracertokenhistory**:

- Membres des rôles **replmonitor** , dans la base de données de distribution
- Membres du rôle serveur fixe **sysadmin** .
- Membres du rôle de base de données fixe **db_owner** dans la base de données de publication.
- **Db_owner** de la base de données fixe.

## <a name="see-also"></a>Voir aussi

[Mesurer la latence et valider les connexions pour la réplication transactionnelle](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
