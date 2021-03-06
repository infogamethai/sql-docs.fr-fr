---
title: Créer une table pour le stockage de données FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], table storage
ms.assetid: 029c3059-5c83-43e2-a859-9027031b7de1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b1a81cd7442e73723b9b1d7c4d0b0cd41101b95b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010330"
---
# <a name="create-a-table-for-storing-filestream-data"></a>Créer une table pour le stockage de données FILESTREAM
  Cette rubrique indique comment créer une table pour stocker des données FILESTREAM.  
  
 Lorsque la base de données comporte un groupe de fichiers FILESTREAM, vous pouvez créer ou modifier des tables pour stocker des données FILESTREAM. Pour spécifier qu'une colonne contient des données FILESTREAM, créez une colonne `varbinary(max)` et ajoutez l'attribut FILESTREAM.  
  
### <a name="to-create-a-table-to-store-filestream-data"></a>Pour créer une table pour stocker des données FILESTREAM  
  
1.  Dans [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], cliquez sur **Nouvelle requête** pour afficher l'Éditeur de requête.  
  
2.  Copiez le code [!INCLUDE[tsql](../../includes/tsql-md.md)] de l'exemple suivant dans l'éditeur de requête. Ce code [!INCLUDE[tsql](../../includes/tsql-md.md)] crée une table compatible FILESTREAM appelée Enregistrements.  
  
3.  Pour créer la table, cliquez sur **Exécuter**.  
  
## <a name="example"></a>Exemple  
 L'exemple de code suivant montre comment créer une table nommée `Records`. La colonne `Id` est une colonne `ROWGUIDCOL` requise pour utiliser des données FILESTREAM avec les API Win32. La colonne `SerialNumber` est une colonne `UNIQUE INTEGER`. La colonne `Chart` est une colonne `FILESTREAM` qui sert à stocker `Chart` dans le système de fichiers.  
  
> [!NOTE]  
>  Cette rubrique fait référence à la base de données Archive créée dans [Créer une base de données compatible FILESTREAM](create-a-filestream-enabled-database.md).  
  
 [!code-sql[FILESTREAM#FS_CreateTable](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_createtable)]  
  
## <a name="see-also"></a>Voir aussi  
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
