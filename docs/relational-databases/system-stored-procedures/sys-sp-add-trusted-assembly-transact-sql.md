---
title: sys. sp_add_trusted_assembly (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_trusted_assembly_TSQL
- sp_add_trusted_assembly
- sys.sp_add_trusted_assembly_TSQL
- sys.sp_add_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_add_trusted_assembly
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb34a814780a46c12c65948bd0b552effaacda4d
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452875"
---
# <a name="syssp_add_trusted_assembly-transact-sql"></a>sys. sp_add_trusted_assembly (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md.md)]

Ajoute un assembly à la liste des assemblys approuvés pour le serveur.

 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône de lien de rubrique") [conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>Syntaxe
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>Notes  

Cette procédure ajoute un assembly à [sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md).

## <a name="arguments"></a>Arguments

[@hash =] '*valeur*'  
Valeur de hachage SHA2_512 de l’assembly à ajouter à la liste des assemblys approuvés pour le serveur. Les assemblys de confiance peuvent être chargés lorsque la [sécurité CLR stricte](../../database-engine/configure-windows/clr-strict-security.md) est activée, même si l’assembly n’est pas signé ou si la base de données n’est pas marquée comme digne de confiance.

[@description =] '*Description*'  
Description facultative définie par l’utilisateur de l’assembly. Microsoft recommande d’utiliser le nom canonique qui encode le nom simple, le numéro de version, la culture, la clé publique et l’architecture de l’assembly à approuver. Cette valeur identifie de façon unique l’assembly sur le côté common language runtime (CLR) et est identique à la valeur clr_name dans sys. Assemblies. 

## <a name="permissions"></a>Permissions

Requiert l’appartenance au rôle serveur fixe `sysadmin` ou à l’autorisation `CONTROL SERVER`.

## <a name="examples"></a>Exemples  

L’exemple suivant ajoute un assembly nommé `pointudt` à la liste des assemblys approuvés pour le serveur. Ces valeurs sont disponibles à partir de [sys. Assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md).     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>Voir aussi  
  [sys. sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [Sécurité CLR stricte](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

