---
title: Suppression de lignes par signet avec SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a34f96dd7f5c2f0e2ac4bbb3feae06ea4856a248
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076813"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>Suppression de lignes par signet avec SQLBulkOperations
Lorsque vous supprimez une ligne par signet, **SQLBulkOperations** rend la source de données à supprimer une ou plusieurs lignes sélectionnées de la table. Les lignes sont identifiées par le signet dans une colonne liée de signet.  
  
 Pour supprimer des lignes par signet avec **SQLBulkOperations**, l’application effectue les opérations suivantes :  
  
1.  Récupère et met en cache les signets de toutes les lignes à supprimer. S’il existe plus d’un signet et la liaison est utilisée, les signets sont stockés dans un tableau. s’il existe plus d’un signet et la liaison est utilisée, les signets sont stockés dans un tableau de structures de ligne.  
  
2.  Définit l’attribut d’instruction SQL_ATTR_ROW_ARRAY_SIZE au nombre de signets et lie la mémoire tampon contenant la valeur du signet, ou le tableau de signets, à la colonne 0.  
  
3.  Appels **SQLBulkOperations** avec *opération* SQL_DELETE_BY_BOOKMARK la valeur.
