---
title: sp_fulltext_load_thesaurus_file (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_load_thesaurus_file
- sp_fulltext_load_thesaurus_file_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_load_thesaurus_file
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], editing
ms.assetid: 73a309c3-6d22-42dc-a6fe-8a63747aa2e4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 96fb5c880346c534c3b956e577f15622e598d48c
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305211"
---
# <a name="sp_fulltext_load_thesaurus_file-transact-sql"></a>sp_fulltext_load_thesaurus_file (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Oblige l'instance de serveur à analyser et charger les données à partir du fichier de dictionnaire des synonymes qui correspond à la langue dont le LCID est spécifié. Cette procédure stockée est utile après la mise à jour d'un fichier de dictionnaire des synonymes. L’exécution de **sp_fulltext_load_thesaurus_file** entraîne la recompilation des requêtes de texte intégral qui utilisent le dictionnaire des synonymes du LCID spécifié.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
sys.sp_fulltext_load_thesaurus_file lcid [ , @loadOnlyIfNotLoaded  = action ]   
```  
  
## <a name="arguments"></a>Arguments  
 *lcid*  
 Entier mappant l’identificateur de paramètres régionaux (LCID) de la langue pour laquelle vous souhaitez Lade la définition XML du dictionnaire des synonymes. Pour obtenir les LCID des langues disponibles sur une instance de serveur, utilisez l’affichage catalogue [Transact- &#40;SQL&#41; sys. fulltext_languages](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) .  
  
 *action* **\@loadOnlyIfNotLoaded** =   
 Spécifie si le fichier de dictionnaire des synonymes doit être chargé dans les tables internes du dictionnaire des synonymes même s'il a déjà été chargé. *action* est l’une des suivantes :  
  
|Value|Définition|  
|-----------|----------------|  
|**0**|Charge le fichier de dictionnaire des synonymes, qu'il ait ou non été déjà chargé. Il s’agit du comportement par défaut de **sp_fulltext_load_thesaurus_file**.|  
|1|Charge le fichier de dictionnaire des synonymes uniquement s'il n'est pas encore chargé.|  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 Aucun  
  
## <a name="result-sets"></a>Jeux de résultats  
 Aucun  
  
## <a name="remarks"></a>Notes  
 Les fichiers d'un dictionnaire des synonymes sont chargés automatiquement par les requêtes de texte intégral qui l'utilisent. Pour éviter cet impact de la première fois sur les performances des requêtes de texte intégral, nous vous recommandons d’exécuter **sp_fulltext_load_thesaurus_file**.  
  
 Utilisez [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**'pour mettre à jour la liste des langues inscrites avec la recherche en texte intégral.  
  
## <a name="permissions"></a>Autorisations  
 Seuls les membres du rôle serveur fixe **sysadmin** ou de l’administrateur système peuvent exécuter la procédure stockée **sp_fulltext_load_thesaurus_file** .  
  
 Seuls des administrateurs système peuvent mettre à jour, modifier ou supprimer des fichiers de dictionnaire des synonymes.  
  
## <a name="examples"></a>Exemples  
  
### <a name="a-load-a-thesaurus-file-even-if-it-is-already-loaded"></a>R. Chargement d'un fichier de dictionnaire des synonymes même s'il a déjà été chargé  
 L'exemple suivant analyse et charge le fichier de dictionnaire des synonymes anglais.  
  
```sql
EXEC sys.sp_fulltext_load_thesaurus_file 1033;
```  
  
### <a name="b-load-a-thesaurus-file-only-if-it-is-not-yet-loaded"></a>B. Chargement d'un fichier de dictionnaire des synonymes uniquement s'il n'est pas encore chargé  
 L'exemple suivant analyse et charge le fichier de dictionnaire des synonymes arabe, sauf s'il est déjà chargé.  
  
```sql
EXEC sys.sp_fulltext_load_thesaurus_file 1025, @loadOnlyIfNotLoaded = 1;
```  

## <a name="see-also"></a>Voir aussi

[FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)  
[Procédures stockées système &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
[Configurer et gérer les fichiers de dictionnaire des synonymes pour la recherche en texte intégral](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)
