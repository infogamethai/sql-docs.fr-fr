---
title: Bureau et les descripteurs de pilotes de base de données | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0096dad8fbb4cf9847385759702e39ac074c4c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112049"
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descripteurs et pilotes pour les bases de données de poste de travail
Un descripteur est une structure de données qui conserve des informations sur les données de la colonne ou de paramètres dynamiques. **SQLGetDescField** peut être utilisée pour récupérer les descripteurs prises en charge répertoriées ci-dessous. Descripteurs de paramètre d’implémentation (IPD) ne sont pas renseignées automatiquement, car **SQLDescribeParam** n’est pas pris en charge. Champs de descripteur qui ne sont pas disponibles via Jet (par exemple, SQL_DESC_BASE_TABLE_NAME) ne sont pas également pris en charge.  
  
 Pour plus d’informations sur les champs de descripteur Jet pris en charge, consultez le *-Guide du programmeur moteur Microsoft Jet de base de données*.  
  
 Pour plus d’informations sur les descripteurs, consultez les rubriques sous « Descripteurs » dans le *de référence du programmeur ODBC*.  
  
|Champs de descripteur|Niveau de prise en charge|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Pris en charge|  
|SQL_DESC_ARRAY_SIZE|Prise en charge uniquement pour ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|Pris en charge|  
|SQL_DESC_BIND_OFFSET_PTR|Pris en charge|  
|SQL_DESC_BIND_TYPE|Pris en charge|  
|SQL_DESC_COUNT|Pris en charge|  
|SQL_DESC_ROWS_PROCESSED_PTR|Prise en charge uniquement pour ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Pris en charge|  
|SQL_DESC_BASE_COLUMN_NAME|Prise en charge (nouveau)|  
|SQL_DESC_BASE_TABLE_NAME|Prise en charge (nouveau)|  
|SQL_DESC_CASE_SENSITIVE|Toujours FALSE|  
|SQL_DESC_CATALOG_NAME|Non pris en charge|  
|SQL_DESC_CONCISE_TYPE|Pris en charge|  
|SQL_DESC_DATA_PTR|Pris en charge|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Pris en charge|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Prise en charge pour les types d’intervalle C|  
|SQL_DESC_DISPLAY_SIZE|Pris en charge|  
|SQL_DESC_FIXED_PREC_SCALE|Prise en charge (TRUE pour argent)|  
|SQL_DESC_INDICATOR_PTR|Pris en charge|  
|SQL_DESC_LABEL|Pris en charge|  
|SQL_DESC_LENGTH|Pris en charge|  
|SQL_DESC_LITERAL_PREFIX|Pris en charge|  
|SQL_DESC_LITERAL_SUFFIX|Pris en charge|  
|SQL_DESC_LOCAL_TYPE_NAME|Non pris en charge (renvoie une chaîne vide)|  
|SQL_DESC_NAME|Pris en charge|  
|SQL_DESC_NULLABLE|Pris en charge<br /><br /> **Remarque** non pris en charge dans les versions précédentes de Jet 4.0|  
|SQL_DESC_NUM_PREC_RADIX|Pris en charge|  
|SQL_DESC_OCTET_LENGTH|Pris en charge|  
|SQL_DESC_OCTET_LENGTH_PTR|Pris en charge|  
|SQL_DESC_PARAMETER_TYPE|Seuls les paramètres d’entrée|  
|SQL_DESC_PRECISION|Pris en charge|  
|SQL_DESC_SCALE|Pris en charge|  
|SQL_DESC_SCHEMA_NAME|Non pris en charge|  
|SQL_DESC_SEARCHABLE|Pris en charge|  
|SQL_DESC_TABLE_NAME|Non pris en charge|  
|SQL_DESC_TYPE|Pris en charge|  
|SQL_DESC_TYPE_NAME|Pris en charge|  
|SQL_DESC_UNNAMED|Pris en charge|  
|SQL_DESC_UNSIGNED|Pris en charge|  
|SQL_DESC_UPDATABLE|Pris en charge|
