---
title: Le défilement par signet | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d27c46407e2994960af4f6abddd6cdc6f08ec852
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055537"
---
# <a name="scrolling-by-bookmark"></a>Défilement par signet
Lors de l’extraction des lignes avec **SQLFetchScroll**, une application peut utiliser un signet comme base pour la sélection de la ligne de départ. Il s'agit d'une forme d'adressage absolu qui ne dépend pas de la position actuelle du curseur. Pour accéder à une ligne marquée par un signet, l’application appelle **SQLFetchScroll** avec un *FetchOrientation* de SQL_FETCH_BOOKMARK. Cette opération utilise le signet vers lequel pointé l’attribut d’instruction SQL_ATTR_FETCH_BOOKMARK_PTR. Elle retourne l'ensemble de lignes démarrant à la ligne identifiée par ce signet. Une application peut spécifier un décalage pour cette opération dans le *FetchOffset* argument de l’appel à **SQLFetchScroll**. Lorsqu’un offset est spécifié, la première ligne de l’ensemble de lignes retourné est déterminée en additionnant le nombre dans le *FetchOffset* argument pour le numéro de la ligne identifiée par le signet. Cette utilisation de la *FetchOffset* argument n’est pas pris en charge lorsqu’il est utilisé avec ODBC 2. *x* pilotes ; lorsqu’une application appelle **SQLFetchScroll** dans un ODBC 2. *x* pilote avec *FetchOrientation* SQL_FETCH_BOOKMARK, la valeur la *FetchOffset* argument doit être défini sur 0.
