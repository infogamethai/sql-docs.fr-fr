---
title: Stdev (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 40af02ce74363fb1df2ae142e7665be8714d181e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036865"
---
# <a name="stdev-mdx"></a>Stdev (MDX)


  Retourne l'exemple d'écart-type d'une expression numérique évaluée sur un jeu à l'aide de la formule de remplissage non biaisée (division par n-1).  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
Stdev(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Arguments  
 *Set_Expression*  
 Une expression MDX (Multidimensional Expressions) valide qui retourne un jeu.  
  
 *Numeric_expression*  
 Expression numérique valide qui correspond généralement à une expression MDX (Multidimensional Expressions) des coordonnées des cellules qui retournent un nombre.  
  
## <a name="remarks"></a>Notes  
 Le **Stdev** fonction utilise le remplissage non biaisée formule lors de la [StdevP](../mdx/stdevp-mdx.md) fonction utilise la formule de remplissage biaisée.  
  
## <a name="example"></a>Exemple  
 L'exemple ci-dessous retourne l'écart-type de la mesure Internet Order Quantity (volume de commandes Internet) évaluée sur les trois premiers mois de l'année civile 2003 à l'aide de la formule de remplissage non biaisée.  
  
```  
WITH MEMBER Measures.x AS   
   Stdev   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Guide de référence des fonctions MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
