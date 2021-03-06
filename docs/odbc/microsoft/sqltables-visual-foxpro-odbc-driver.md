---
title: SQLTables (pilote ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22e5f34a6accac3a2bb0d1ecefe7c1d5431cb562
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949004"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (pilote ODBC Visual FoxPro)
> [!NOTE]  
>  Cette rubrique contient des informations spécifiques au pilote ODBC Visual FoxPro. Pour obtenir des informations générales sur cette fonction, consultez la rubrique appropriée sous [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Prise en charge : Complète  
  
 Conformité d’API ODBC : Niveau 1  
  
 Retourne la liste des noms de table spécifié par le paramètre dans le **SQLTables** instruction. Si aucun paramètre n’est spécifié, retourne les noms de table stockées dans la source de données actuelle. Le pilote retourne les informations comme jeu de résultats.  
  
 Énumération type appelle la méthode ne reçoit pas une entrée de jeu de résultats pour des vues paramétrées locales ou distant. Toutefois, un appel à **SQLTables** avec une table unique spécificateur de nom trouve une correspondance pour une telle vue s’il est présent portant ce nom ; Cela permet à l’API à utiliser pour rechercher les conflits de noms avant la création d’une nouvelle table.  
  
> [!NOTE]  
>  Le pilote ODBC Visual FoxPro fait la distinction entre [tables de base de données](../../odbc/microsoft/visual-foxpro-terminology.md) et [gratuit tables](../../odbc/microsoft/visual-foxpro-terminology.md), même si les deux types de tables sont stockées dans le même répertoire sur votre système. Si votre source de données est un répertoire de tables gratuits, le pilote ODBC Visual FoxPro ne catalogue ni retourner les noms de toutes les tables qui sont associés à une base de données.  
  
 Pour plus d’informations, consultez [SQLTables](../../odbc/reference/syntax/sqltables-function.md) dans le *de référence du programmeur ODBC*.
