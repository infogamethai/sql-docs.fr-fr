---
title: SQLGetStmtOption (pilote ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5521fb11cad064cf487d38562f4146fd32587993
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898783"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (pilote ODBC Visual FoxPro)
> [!NOTE]  
>  Cette rubrique contient des informations spécifiques au pilote ODBC Visual FoxPro. Pour obtenir des informations générales sur cette fonction, consultez la rubrique appropriée sous [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Prise en charge : Complète  
  
 Conformité d’API ODBC : Niveau 1  
  
 Retourne le paramètre actuel d’une option d’instruction.  
  
|*FOption*|Valeur renvoyée|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|valeur entière de 32 bits qui est le signet pour le numéro d’enregistrement en cours|  
|SQL_ROW_NUMBER|valeur d’entier 32 bits en spécifiant la position de la ligne actuelle dans le résultat|  
|SQL_TRANSLATE_DLL|Erreur : « Non compatibles avec le pilote »|  
  
 Le pilote ODBC Visual FoxPro ne contient aucune DLL de traduction.  
  
 Pour plus d’informations, consultez [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) dans le *de référence du programmeur ODBC*.
