---
title: SQLBindParameter | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cba973be9b4dc2ec0da286b2d01b636f0ca4e2b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067815"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
  `SQLBindParameter` Permet d’éliminer le fardeau de conversion de données lorsqu’il est utilisé pour fournir des données pour le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pilote ODBC Native Client, ce qui entraîne des gains de performances significatifs pour les composants client et serveur d’applications. D'autres avantages incluent une perte réduite de précision lors de l'insertion ou de la mise à jour de types de données numériques approximatifs.  
  
> [!NOTE]  
>  Lors de l'insertion de données de type `char` et `wchar` dans une colonne image, la taille des données passées est utilisée, par opposition à la taille des données après conversion vers un format binaire.  
  
 Si le pilote ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client rencontre une erreur sur un élément de tableau unique d'un tableau de paramètres, le pilote continue d'exécuter l'instruction pour les éléments de tableau restants. Si l'application a lié un tableau d'éléments d'état de paramètre pour l'instruction, les lignes des paramètres qui génèrent des erreurs peuvent être déterminées à partir de ce tableau.  
  
 Lors de l'utilisation du pilote ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, spécifiez SQL_PARAM_INPUT lors de la liaison de paramètres d'entrée. Spécifiez seulement SQL_PARAM_OUTPUT ou SQL_PARAM_INPUT_OUTPUT lors de la liaison de paramètres de procédure stockée définis avec le mot clé OUTPUT.  
  
 [SQLRowCount](sqlrowcount.md) n’est pas fiable avec le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pilote ODBC Native Client si un élément de tableau d’un tableau de paramètres liés provoque une erreur dans l’exécution des instructions. L'attribut d'instruction ODBC SQL_ATTR_PARAMS_PROCESSED_PTR signale le nombre de lignes traitées avant l'erreur. L'application peut alors parcourir son tableau d'état de paramètre pour découvrir le nombre d'instructions exécutées avec succès, si nécessaire.  
  
## <a name="binding-parameters-for-sql-character-types"></a>Liaison de paramètres pour les types de caractères SQL  
 Si le type de données SQL passé est un type de caractère, *ColumnSize* est la taille en caractères (non en octets). Si la longueur de la chaîne de données en octets est supérieure à 8000, *ColumnSize* doit être défini sur `SQL_SS_LENGTH_UNLIMITED`, indiquant qu’il n’existe aucune limite à la taille du type SQL.  
  
 Par exemple, si le type de données SQL est `SQL_WVARCHAR`, *ColumnSize* ne doit pas être supérieure à 4 000. Si la longueur réelle des données est supérieure à 4000, puis *ColumnSize* doit être défini sur `SQL_SS_LENGTH_UNLIMITED` afin que `nvarchar(max)` sera utilisé par le pilote.  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter et paramètres table  
 Comme d’autres types de paramètre, les paramètres table sont liés par SQLBindParameter.  
  
 Une fois qu'un paramètre table a été lié, ses colonnes sont également liées. Pour lier les colonnes, vous appelez [SQLSetStmtAttr](sqlsetstmtattr.md) pour définir SQL_SOPT_SS_PARAM_FOCUS à la position ordinale du paramètre table incluse. Ensuite, appelez SQLBindParameter pour chaque colonne dans le paramètre table. Pour retourner aux liaisons de paramètre de premier niveau, attribuez à SQL_SOPT_SS_PARAM_FOCUS la valeur 0.  
  
 Pour plus d’informations sur les paramètres de mappage de champs de descripteur pour les paramètres table, consultez [liaison et les valeurs de colonne et les paramètres Data Transfer of Table-Valued](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Pour plus d’informations sur les paramètres table, consultez [paramètres table &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>Prise en charge de SQLBindParameter pour les fonctionnalités de date et heure améliorées  
 Les valeurs de paramètre des types de date/heure sont converties comme décrit dans [Conversions de C en SQL](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md). Notez que les paramètres de type `time` et `datetimeoffset` doit avoir *ValueType* spécifié en tant que `SQL_C_DEFAULT` ou `SQL_C_BINARY` si leurs structures correspondantes (`SQL_SS_TIME2_STRUCT` et `SQL_SS_TIMESTAMPOFFSET_STRUCT`) sont utilisés.  
  
 Pour plus d’informations, consultez [améliorations Date / heure &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>Prise en charge SQLBindParameter pour les types CLR volumineux définis par l'utilisateur  
 `SQLBindParameter` prend en charge les grands types CLR définis par l'utilisateur. Pour plus d’informations, consultez [Large CLR User-Defined Types &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Détails d’implémentation API ODBC](odbc-api-implementation-details.md)   
 [SQLBindParameter, fonction](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
