---
title: Récupération des signets | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f18b87adf31f19d2a93bb3af3e14c265ae3940af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020574"
---
# <a name="retrieving-bookmarks"></a>Récupération des signets
Si l’application utilisera des signets, il doit définir l’attribut d’instruction SQL_ATTR_USE_BOOKMARKS à SQL_UB_VARIABLE avant la préparation ou l’exécution de l’instruction. Cela est nécessaire, car la création et la maintenance des signets peuvent être une opération coûteuse, et signets doivent être activées uniquement quand une application peut faire une bonne de les utilisent.  
  
 Les signets sont retournés en tant que colonne 0 du jeu de résultats. Il existe trois façons qu'une application peut récupérer les :  
  
-   Lier la colonne 0 du jeu de résultats. **SQLFetch** ou **SQLFetchScroll** retourne les signets pour chaque ligne dans l’ensemble de lignes, ainsi que les données pour d’autres liées aux colonnes.  
  
-   Appelez **SQLSetPos** pour positionner à une ligne dans l’ensemble de lignes, puis appelez **SQLGetData** pour la colonne 0. Si un pilote prend en charge les signets, il doit toujours prendre en charge la possibilité d’appeler **SQLGetData** pour la colonne 0, même s’il n’autorise pas les applications d’appeler **SQLGetData** pour les autres colonnes avant la dernière limite colonne.  
  
-   Appelez **SQLBulkOperations** avec la *opération* SQL_ADD à l’argument et la colonne 0 liée. Le curseur insère la ligne et retourne le signet pour la ligne dans la mémoire tampon liée.
