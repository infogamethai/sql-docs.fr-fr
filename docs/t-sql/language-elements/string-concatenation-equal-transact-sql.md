---
title: += Concaténation de chaînes
description: Concaténer deux chaînes et définir la chaîne obtenue à l’aide du résultat de l’opération.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 12/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- concatenate strings
- string concatenation
- += (concatenate operator)
ms.assetid: 4aaeaab7-9b2b-48e0-8487-04ed672ebcb1
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dd21fb221076470d0c39194ea4c38d96af0f1056
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75257053"
---
# <a name="-string-concatenation-assignment-transact-sql"></a>+= (Affectation après concaténation de chaînes) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Concatène deux chaînes et définit la chaîne obtenue à l'aide du résultat de l'opération. Par exemple, si une variable @x a la valeur « Adventure », alors @x += « Works » prend la valeur d’origine de @x, ajoute « Works » à la chaîne, puis assigne à @x la nouvelle valeur « AdventureWorks ».  
  
 ![Icône du lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône du lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
expression += expression  
```  
  
## <a name="arguments"></a>Arguments  
 *expression*  
 Toute [expression](../../t-sql/language-elements/expressions-transact-sql.md) valide des types de données caractères.  
  
## <a name="result-types"></a>Types des résultats  
 Retourne le type de données défini pour la variable.  
  
## <a name="remarks"></a>Notes  
 SET @v1 += 'expression' équivaut à SET @v1 = @v1 + ('expression'). De plus, SET @v1 = @v2 + @v3 + @v4 équivaut à SET @v1 = (@v2 + @v3) + @v4.  
  
 L'opérateur += ne peut pas être utilisé sans une variable. Par exemple, le code suivant génère une erreur :  
  
```  
SELECT 'Adventure' += 'Works'  
```  
  
## <a name="examples"></a>Exemples  
### <a name="a-concatenation-using--operator"></a>R. Concaténation à l’aide de l’opérateur +=
 L'exemple suivant est une concaténation basée sur l'opérateur `+=`.  
  
```  
DECLARE @v1 varchar(40);  
SET @v1 = 'This is the original.';  
SET @v1 += ' More text.';  
PRINT @v1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `This is the original. More text.`  
  
### <a name="b-order-of-evaluation-while-concatenating-using--operator"></a>B. Ordre d’évaluation lors de la concaténation à l’aide de l’opérateur +=
L’exemple suivant concatène plusieurs chaînes pour former une seule et même longue chaîne, puis essaie de calculer la longueur de la chaîne finale. Cet exemple illustre les règles d’ordre d’évaluation et de troncation, lors de l’utilisation de l’opérateur de concaténation. 

```
DECLARE @x varchar(4000) = replicate('x', 4000)
DECLARE @z varchar(8000) = replicate('z',8000)
DECLARE @y varchar(max);
 
SET @y = '';
SET @y += @x + @z;
SELECT LEN(@y) AS Y; -- 8000
 
SET @y = '';
SET @y = @y + @x + @z;
SELECT LEN(@y) AS Y; -- 12000
 
SET @y = '';
SET @y = @y +(@x + @z);
SELECT LEN(@y) AS Y; -- 8000
-- or
SET @y = '';
SET @y = @x + @z + @y;
SELECT LEN(@y) AS Y; -- 8000
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
    
 Y       
 ------- 
 12000 
  
 (1 row(s) affected) 

 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
 Y       
 ------- 
 8000 
  
 (1 row(s) affected)
  ```   
   
## <a name="see-also"></a>Voir aussi  
 [Opérateurs &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+= &#40;Affectation après addition&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [+ &#40;Concaténation de chaînes&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
  
  
