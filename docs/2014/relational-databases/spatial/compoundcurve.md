---
title: CompoundCurve | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: ae357f9b-e3e2-4cdf-af02-012acda2e466
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 48d1ca9458b4993ad509cc2bbedd8d23b127918c
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688680"
---
# <a name="compoundcurve"></a>CompoundCurve
  Un `CompoundCurve` est une collection de zéro ou plusieurs instances continues `CircularString` ou `LineString`, de type geometry ou geography.  
  
> [!IMPORTANT]  
>  Pour obtenir une description détaillée et des exemples des nouvelles fonctionnalités spatiales de cette version, y compris le sous-type `CompoundCurve`, téléchargez le livre blanc [nouvelles fonctionnalités spatiales dans SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
 Une instance `CompoundCurve` vide peut être instanciée, mais pour qu'un `CompoundCurve` soit valide, il doit respecter les critères suivants :  
  
1.  Il doit contenir au moins une instance `CircularString` ou `LineString`.  
  
2.  La séquence des instances `CircularString` ou `LineString` doit être continue.  
  
 Si un `CompoundCurve` contient une séquence de plusieurs instances de `CircularString` et de `LineString`, le point de terminaison de fin pour chaque instance, à l’exception de la dernière instance, doit être le point de terminaison de départ pour l’instance suivante de la séquence. Cela signifie que si le point de fin d'une instance précédente dans la séquence est (4 3 7 2), le point de départ de l'instance suivante dans la séquence doit être (4 3 7 2). Notez que les valeurs Z (élévation) et M (mesure) du point doivent également être identiques. Si les deux points présentent une différence, une `System.FormatException` est levée. Les points dans un `CircularString` n'ont pas besoin de valeur Z ou M. Si aucune valeur Z ou M n'est indiquée pour le point de fin de l'instance précédente, le point de départ de l'instance suivante ne peut pas inclure de valeur Z ou M. Si le point de fin de la séquence précédente est (4 3), le point de départ de la séquence suivante doit être (4 3), mais pas (4 3 7 2). Tous les points d'une instance `CompoundCurve` doivent soit ne pas avoir de valeur Z, soit avoir une valeur Z identique.  
  
## <a name="compoundcurve-instances"></a>Instances CompoundCurve  
 L'illustration suivante montre des types de `CompoundCurve` valides.  
  
 ![](../../database-engine/media/f278742e-b861-4555-8b51-3d972b7602bf.png "f278742e-b861-4555-8b51-3d972b7602bf")  
  
### <a name="accepted-instances"></a>Instances acceptées  
 L'instance `CompoundCurve` est acceptée s'il s'agit d'une instance vide ou si elle répond aux critères suivants.  
  
1.  Toutes les instances contenues par l'instance `CompoundCurve` sont des instances de segment d'arc de cercle acceptées. Pour plus d’informations sur les instances de segment d’arc de cercle acceptées, consultez [LineString](linestring.md) et [CircularString](circularstring.md).  
  
2.  Tous les segments d'arc de cercle dans l'instance `CompoundCurve` sont connectés. Le premier point de chaque segment d'arc de cercle suivant est identique au dernier point du segment d'arc de cercle précédent.  
  
    > [!NOTE]  
    >  Cela inclut les coordonnées Z et M. Ainsi, les quatre coordonnées X, Y, Z et M doivent être identiques.  
  
3.  Aucune des instances contenues n'est une instance vide.  
  
 L'exemple suivant illustre des instances `CompoundCurve` acceptées.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
```  
  
 L'exemple suivant montre des instances `CompoundCurve` qui ne sont pas acceptées. Ces instances lèvent une `System.FormatException`.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING EMPTY)';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (1 0, 2 0))';  
```  
  
### <a name="valid-instances"></a>Instances valides  
 Une instance `CompoundCurve` est valide si elle répond aux critères suivants.  
  
1.  L'instance `CompoundCurve` est acceptée.  
  
2.  Toutes les instances de segment d'arc de cercle contenues par l'instance `CompoundCurve` sont des instances valides.  
  
 L'exemple suivant montre des instances `CompoundCurve` valides.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
  
```  
  
 `@g3` est valide parce que l'instance `CircularString` est valide. Pour plus d’informations sur la validité de l’instance de `CircularString`, consultez [CircularString](circularstring.md).  
  
 L'exemple suivant montre des instances `CompoundCurve` qui ne sont pas valides.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4, 3 5))';  
DECLARE @g2 geometry = 'COMPOUNDCURVE((1 1, 1 1))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 2 3, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g1` n’est pas valide car la deuxième instance n’est pas une instance LineString valide. `@g2` n'est pas valide car l'instance `LineString` n'est pas valide. `@g3` n'est pas valide car l'instance `CircularString` n'est pas valide. Pour plus d’informations sur les instances `CircularString` et `LineString` valides, consultez [CircularString](circularstring.md) et [LineString](linestring.md).  
  
## <a name="examples"></a>Exemples  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-compooundcurve"></a>A. Instanciation d'une instance geometry avec un CompooundCurve vide  
 L'exemple suivant montre comment créer une instance `CompoundCurve` vide :  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-using-a-compoundcurve-in-the-same-statement"></a>B. Déclaration et instanciation d'une instance geometry à l'aide d'un CompoundCurve dans la même instruction  
 L’exemple suivant indique comment déclarer et initialiser une instance `geometry` avec `CompoundCurve`dans la même instruction :  
  
```sql  
DECLARE @g geometry = 'COMPOUNDCURVE ((2 2, 0 0),CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-compoundcurve"></a>C. Instanciation d'une instance geography avec un CompoundCurve  
 L'exemple suivant indique comment déclarer et initialiser une instance `geography` avec un `CompoundCurve` :  
  
```sql  
DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-square-in-a-compoundcurve-instance"></a>D. Stocker un carré dans une instance CompoundCurve  
 L'exemple suivant montre deux façons différentes d'utiliser une instance `CompoundCurve` pour stocker un carré.  
  
```sql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3), (1 3, 3 3),(3 3, 3 1), (3 1, 1 1))');  
SET @g2 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3, 3 3, 3 1, 1 1))');  
SELECT @g1.STLength(), @g2.STLength();  
```  
  
 Les longueurs de `@g1` et `@g2` sont identiques. Notez dans cet exemple qu'une instance `CompoundCurve` peut stocker une ou plusieurs instances `LineString`.  
  
### <a name="e-instantiating-a-geometry-instance-using-a-compoundcurve-with-multiple-circularstrings"></a>E. Instanciation d'une instance geometry à l'aide d'un CompoundCurve avec plusieurs CircularStrings  
 L'exemple suivant montre comment utiliser deux instances `CircularString` différentes pour initialiser un `CompoundCurve`.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT @g.STLength();  
```  
  
 Cela génère la sortie suivante : 12,566370... qui est l’équivalent de 4&#x03c0; (4 * pi). L'instance `CompoundCurve` de l'exemple stocke un cercle avec un rayon de 2. Les deux exemples de code précédents n'ont pas eu à utiliser un `CompoundCurve`. Pour le premier exemple, une instance `LineString` aurait été plus simple et pour le deuxième exemple, une instance `CircularString` . Toutefois, l'exemple suivant montre en quoi un `CompoundCurve` constitue une meilleure solution.  
  
### <a name="f-using-a-compoundcurve-to-store-a-semicircle"></a>F. Utilisation d'un CompoundCurve pour stocker un demi-cercle  
 L'exemple suivant utilise une instance `CompoundCurve` pour stocker un demi-cercle.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))');  
SELECT @g.STLength();  
```  
  
### <a name="g-storing-multiple-circularstring-and-linestring-instances-in-a-compoundcurve"></a>G. Stocker plusieurs instances CircularString et LineString dans un CompoundCurve  
 L'exemple suivant montre comment plusieurs instances `CircularString` et `LineString` peuvent être stockées à l'aide d'un `CompoundCurve`.  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::Parse('COMPOUNDCURVE((3 5, 3 3), CIRCULARSTRING(3 3, 5 1, 7 3), (7 3, 7 5), CIRCULARSTRING(7 5, 5 7, 3 5))');  
SELECT @g.STLength();  
```  
  
### <a name="h-storing-instances-with-z-and-m-values"></a>H. Stockage d'instances avec des valeurs Z et M  
 L'exemple suivant indique comment utiliser une instance `CompoundCurve` pour stocker une séquence d'instances `CircularString` et `LineString` comportant toutes deux des valeurs Z et M.  
  
```sql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(7 5 4 2, 5 7 4 2, 3 5 4 2), (3 5 4 2, 8 7 4 2))');  
```  
  
### <a name="i-illustrating-why-circularstring-instances-must-be-explicitly-declared"></a>I. Illustration de la raison pour laquelle les instances CircularString doivent être déclarées de manière explicite  
 L'exemple suivant montre pourquoi les instances `CircularString` doivent être déclarées de manière explicite. Le programmeur essaie de stocker un cercle dans une instance `CompoundCurve` .  
  
```sql  
DECLARE @g1 geometry;    
DECLARE @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 2 4, 0 2))');  
SELECT 'Circle One', @g1.STLength() AS Perimeter;  -- gives an inaccurate amount  
SET @g2 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT 'Circle Two', @g2.STLength() AS Perimeter;  -- now we get an accurate amount  
```  
  
 La sortie est la suivante :  
  
```  
Circle One11.940039...  
Circle Two12.566370...  
```  
  
 Le périmètre du cercle deux est approximativement de&#x03c0; 4 (4 * pi), qui est la valeur réelle du périmètre. Toutefois, le périmètre de Circle One est exagérément inexact. L'instance `CompoundCurve` de Circle One stocke un segment d'arc de cercle (ABC) et deux segments de ligne (CD, DA). L'instance `CompoundCurve` doit stocker deux segments d'arc de cercle (ABC, CDA) pour définir un cercle. Une instance `LineString` définit le deuxième ensemble de points (4 2, 2 4, 0 2) dans l'instance `CompoundCurve` de Circle One. Vous devez déclarer de manière explicite une instance `CircularString` à l'intérieur d'un `CompoundCurve`.  
  
## <a name="see-also"></a>Voir aussi  
 [STIsValid &#40;type de données geometry&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)   
 [STLength &#40;type de données geometry&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STStartPoint &#40;type de données geometry&#41;](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)   
 [STEndPoint &#40;type de données geometry&#41;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)   
 [LineString](linestring.md)   
 [CircularString](circularstring.md)   
 [Présentation des types de données spatiales](spatial-data-types-overview.md)   
 [Point](point.md)  
  
  
