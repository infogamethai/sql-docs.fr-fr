---
title: = (Égal à) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 189facb54de244ff220b41ec08c8b02faf5a2c27
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139322"
---
# <a name="-equal-to-mdx"></a>= (Égal à) (MDX)


  Exécute une opération de comparaison qui détermine si la valeur d'une expression MDX est égale à celle d'une autre expression MDX.  
  
> [!NOTE]  
>  Pour comparer des objets, utilisez le [IS &#40;MDX&#41; ](../mdx/is-mdx.md) opérateur. Par exemple, utilisez l'opérateur IS lorsque vous vérifiez si le membre actuel sur un axe de requête est un membre spécifique.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>Paramètres  
 *MDX_Expression*  
 Expression MDX valide.  
  
## <a name="return-value"></a>Valeur de retour  
 Valeur booléenne basée sur les conditions suivantes :  
  
-   **true** si la valeur du premier paramètre est égale à la valeur du second paramètre.  
  
-   **false** si la valeur du premier paramètre n’est pas égale à la valeur du second paramètre.  
  
-   **true** si les deux paramètres sont null, ou un paramètre est null, et l’autre paramètre est 0.  
  
## <a name="examples"></a>Exemples  
 La requête suivante offre des exemples de ces conditions :  
  
 `With`  
  
 `--Returns true`  
  
 `Member [Measures].bool1 as 1=1`  
  
 `--Returns false`  
  
 `Member [Measures].bool2 as 1=0`  
  
 `--Returns true`  
  
 `Member [Measures].bool3 as null=null`  
  
 `--Returns true`  
  
 `Member [Measures].bool4 as 0=null`  
  
 `--Returns false`  
  
 `Member [Measures].bool5 as 1=null`  
  
 `Select {[Measures].bool1,[Measures].bool2,[Measures].bool3,[Measures].bool4,[Measures].bool5}`  
  
 `On 0`  
  
 `From [Adventure Works]`  
  
## <a name="see-also"></a>Voir aussi  
 [Référence des opérateurs MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
