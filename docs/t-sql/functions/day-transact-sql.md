---
title: DAY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DAY_TSQL
- DAY
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], DAY
- dates [SQL Server], functions
- DAY function [SQL Server]
- dates [SQL Server], days
- functions [SQL Server], date and time
- dateparts [SQL Server], day
ms.assetid: 2f4410ea-fd3e-4d69-ac4b-3b0091a084bc
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0f1d58e89e6fd7cdc4d8af85d3d8745e1bc15fa7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68119063"
---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Cette fonction retourne un entier représentant le jour (jour du mois) de la *date* spécifiée.
  
Pour obtenir une vue d’ensemble de tous les types de données et fonctions de date et d’heure [, consultez ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)Types de données et fonctions de date et d’heure &#40;Transact-SQL&#41;[!INCLUDE[tsql](../../includes/tsql-md.md)].
  
![Icône du lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône du lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntaxe  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>Arguments  
*date*  
Expression qui est résolue en l’un des types de données suivants :

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

Pour *date*, `DAY` accepte une expression de colonne, une expression, un littéral de chaîne ou une variable définie par l’utilisateur.
  
## <a name="return-type"></a>Type de retour  
**int**
  
## <a name="return-value"></a>Valeur de retour  
DAY retourne la même valeur que [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**day**, *date*).
  
Si *date* contient uniquement une partie heure, `DAY` retourne 1, le jour de base.
  
## <a name="examples"></a>Exemples  
Cette instruction retourne `30`, le numéro du jour lui-même.
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
Cette instruction retourne `1900, 1, 1`. L’argument *date* a la valeur numérique `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interprète `0` comme le 1er janvier 1900.
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>Voir aussi
[CAST et CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


