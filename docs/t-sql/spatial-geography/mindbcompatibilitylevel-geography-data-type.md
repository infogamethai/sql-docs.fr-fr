---
title: MinDbCompatibilityLevel (type de données geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MinDbCompatibilityLevel
- MinDbCompatibilityLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geography)
ms.assetid: a9e44748-4a9e-4179-abc4-7631597be5a7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a8aaa21498c95c215de5e5a49f9ced8089b4c71e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68223659"
---
# <a name="mindbcompatibilitylevel-geography-data-type"></a>MinDbCompatibilityLevel (type de données geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retourne la compatibilité minimale de la base de données pour reconnaître le type de données **geography**.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
. MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>Types de retour  
 Type de retour [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : **int**  
  
 Type de retour CLR : **int**  
  
## <a name="remarks"></a>Notes  
 Utilisez `MinDbCompatibilityLevel()` pour tester la compatibilité d'un objet spatial avant de modifier le niveau de compatibilité sur une base de données. Un type **geography** non valide retourne 110.  
  
## <a name="examples"></a>Exemples  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>R. Test de compatibilité de CircularString avec le niveau de compatibilité 110  
 L'exemple suivant teste la compatibilité d'une instance `CircularString` avec une version précédente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 110  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. Test de compatibilité de LineString avec le niveau de compatibilité 100  
 L'exemple suivant teste la compatibilité d'une instance `LineString` avec [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] :  
  
```  
DECLARE @g geometry = 'LINESTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 100  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="c-testing-the-value-of-a-geography-instance-for-compatibility"></a>C. Test de compatibilité de la valeur d'une instance géographique  
 L'exemple suivant affiche les niveaux de compatibilité de deux instances `geography`. L'une est plus petite qu'un hémisphère et l'autre est plus grande qu'un hémisphère :  
  
```  
DECLARE @g geography = geography::Parse('POLYGON((0 -10, 120 -10, 240 -10, 0 -10))');  
DECLARE @h geography = geography::Parse('POLYGON((0 10, 120 10, 240 10, 0 10))');  
IF (@g.EnvelopeAngle() >= 90)  
BEGIN  
SELECT @g.MinDbCompatibilityLevel();  
END     
IF (@h.EnvelopeAngle() < 90)  
BEGIN  
SELECT @h.MinDbCompatibilityLevel();  
END  
  
```  
  
 La première instruction SELECT retourne 110, la deuxième retourne 100.  
  
## <a name="see-also"></a>Voir aussi  
 [Niveau de compatibilité ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Compatibilité descendante du moteur de base de données SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
  
  
