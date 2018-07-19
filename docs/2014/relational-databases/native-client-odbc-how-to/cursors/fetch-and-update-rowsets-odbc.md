---
title: Extraire et mettre à jour des ensembles de lignes (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d41ba76ceaa157070fc2584c5ebd6d080f415420
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419468"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Extraire et mettre à jour des ensembles de lignes (ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>Extraire et mettre à jour des ensembles de lignes  
  
1.  Le cas échéant, appelez [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) avec SQL_ROW_ARRAY_SIZE pour modifier le nombre de lignes (R) dans l’ensemble de lignes.  
  
2.  Appelez [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) ou [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) pour obtenir un ensemble de lignes.  
  
3.  Si des colonnes dépendantes sont utilisées, utilisez les valeurs de données et les longueurs de données à présent disponibles dans les tampons de colonnes dépendantes pour l'ensemble de lignes.  
  
     Si des colonnes indépendantes sont utilisées, pour chaque ligne, appelez [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) avec SQL_POSITION pour définir la position du curseur ; ensuite, pour chaque colonne indépendante :  
  
    -   Appelez [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) une ou plusieurs fois pour obtenir les données pour les colonnes indépendant après la dernière colonne dépendante de l’ensemble de lignes. Les appels à [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) doit se trouver dans l’ordre croissant des numéros de colonne.  
  
    -   Appelez plusieurs fois [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) pour obtenir des données à partir d’une colonne text ou image.  
  
4.  Configurez toutes les colonnes image ou text de données en cours d'exécution.  
  
5.  Appelez [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) ou [SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398) pour définir la position du curseur, actualiser, mettre à jour, supprimer ou ajouter une ou des lignes dans l'ensemble de lignes.  
  
     Si des colonnes image ou text de données en cours d'exécution sont utilisées pour une opération de mise à jour ou d'ajout, gérez-les.  
  
6.  Si vous le souhaitez, exécuter une instruction UPDATE ou DELETE positionnée, en spécifiant le nom de curseur (disponible à partir de [SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md)) et l’utilisation d’un descripteur d’instruction différent sur la même connexion.  
  
## <a name="see-also"></a>Voir aussi  
 [À l’aide des rubriques de procédures de curseurs &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  