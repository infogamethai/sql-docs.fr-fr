---
title: Éditeur de formulaire d’Action d’extraction (onglet Actions, Concepteur de Cube) (Analysis Services - données multidimensionnelles) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.drillthroughaction.f1
ms.assetid: 225fd818-b5ea-494f-b67b-66e09798274a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 33d20da736308b4436c40a50b8b01da7445663c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081455"
---
# <a name="drillthrough-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Éditeur de formulaire d'action d'extraction (onglet Actions, Concepteur de cube) (Analysis Services - Données multidimensionnelles)
  Utilisez le volet **Éditeur de formulaire d’action d’extraction** sous l’onglet **Actions** du Concepteur de cube pour modifier l’action d’extraction sélectionnée dans le volet **Organisateur d’action**. Pour plus d’informations sur les actions d’extraction, consultez [Actions &#40;Analysis Services - Données multidimensionnelles&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Les actions d'extraction ne descendent plus vers la banque de données sous-jacente. Les informations auxquelles accèdent les actions d'extraction doivent être façonnées dans le cube à l'aide de membres de la dimension ou la hiérarchie.  
  
## <a name="options"></a>Options  
 **nom**  
 Tapez le nom de l'action.  
  
 **Cible d'action**  
 Développez pour afficher l’option **Membres de groupe de mesures** .  
  
 **Membres de groupe de mesures**  
 Sélectionnez le groupe de mesures auquel l'action d'extraction doit être associée.  
  
 **Condition (facultatif)**  
 Entrez la syntaxe MDX (Multidimensional Expressions) qui décrit une condition facultative utilisée conjointement avec l’option **Membres de groupe de mesures**, pour restreindre davantage quand l’action est disponible. L'expression doit retourner une valeur booléenne qui, si elle est vraie, indique que l'action est disponible.  
  
 Faites glisser les éléments sélectionnés du volet **Outils de calcul** dans cette option pour inclure la syntaxe MDX de l'élément sélectionné.  
  
 **Colonnes d'extraction**  
 Développez afin d'afficher une grille qui mentionne les attributs renvoyés lorsque l'utilisateur exécute cette action.  
  
> [!NOTE]  
>  Vous pouvez sélectionner plusieurs dimensions, mais chaque dimension ne peut être utilisée qu'une seule fois dans une action d'extraction.  
  
 Cette grille comporte les colonnes suivantes :  
  
|colonne|Description|  
|------------|-----------------|  
|**Dimensions**|Sélectionnez la dimension dont est dérivé l'attribut renvoyé. Sélectionnez MEASURES pour réaliser une extraction sur les mesures.|  
|**Colonnes de retour**|Sélectionnez l'attribut ou la mesure à partir de la dimension choisie et qui doit être renvoyé(e) lors de l'exécution de l'action.|  
  
 **Propriétés supplémentaires**  
 Développez pour afficher les options **Par défaut**, **Lignes au maximum**, **Invocation**, **Application**, **Description**, **Légende**et **La légende est MDX** .  
  
 **Default**  
 Sélectionnez **True** pour définir cette action d’extraction comme valeur par défaut. Sinon, sélectionnez **False**.  
  
 Si le `RETURN` clause est omise dans MDX `DRILLTHROUGH` instruction exécutée par une application cliente, le [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instance évalue toutes les actions d’extraction par défaut et exécute la première extraction par défaut action qui retourne un jeu non vide. Pour plus d’informations sur MDX `DRILLTHROUGH` instruction, consultez [instruction DRILLTHROUGH &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-drillthrough).  
  
> [!NOTE]  
>  Cette option est utilisée à des fins de compatibilité ascendante.  
  
 **Nombre maximal de lignes**  
 Tapez le nombre maximum de lignes à retourner par l'action d'extraction. Si vous attribuez la valeur zéro à cette option ou que vous la laissez vide, l'action d'extraction retourne toutes les lignes à l'application cliente.  
  
 **Invocation**  
 Sélectionnez le paramètre qui indique le moment où l'action doit être effectuée.  
  
> [!NOTE]  
>  Cette option ne fournit qu'une recommandation à une application cliente quant au moment d'exécution d'une action ; elle ne commande pas directement l'appel de l'action.  
  
 Le tableau suivant décrit les paramètres disponibles.  
  
|Value|Description|  
|-----------|-----------------|  
|Traitement|L’action doit s’exécuter dans le cadre d’une opération par lot ou d’une tâche [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .|  
|Interactif|L'action s'exécute lorsque l'utilisateur l'invoque.|  
|À l’ouverture|L'action s'exécute à la première ouverture du cube.|  
  
 **Application**  
 Tapez le nom de l'application qui peut exécuter l'action d'extraction.  
  
 Vous pouvez également utiliser cette option pour identifier l'application cliente qui utilise le plus souvent cette action, ainsi que pour afficher les icônes appropriées dans un menu contextuel à côté de l'action.  
  
> [!NOTE]  
>  Cette option ne fournit qu'une recommandation à une application cliente quant à l'application cliente qui doit exécuter une action ; elle ne commande pas directement l'accès à l'action. Les applications clientes doivent masquer toute action associée à d'autres applications clientes.  
  
 **Description**  
 Tapez une description facultative de l'action.  
  
 **Légende**  
 Entrez la légende à afficher pour l’action dans l’application cliente si l’option **La légende est MDX** a la valeur **False**.  
  
 Entrez l’expression MDX (Multidimensional Expressions) qui retourne une chaîne pour la légende si l’option **La légende est MDX** a la valeur **True**.  
  
 **La légende est MDX**  
 Sélectionnez **False** pour indiquer que la **Légende** contient une chaîne littérale qui représente une légende à afficher pour l’action dans l’application cliente.  
  
 Sélectionnez **True** pour indiquer que la **Légende** contient une expression MDX qui retourne une chaîne représentant une légende à afficher pour l’action dans l’application cliente. L'expression MDX doit être résolue avant que l'action soit retournée à l'application cliente.  
  
## <a name="see-also"></a>Voir aussi  
 [Référence MDX &#40;Multidimensional Expressions&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Actions &#40;Concepteur de Cube&#41; &#40;Analysis Services - données multidimensionnelles&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Barre d’outils &#40;onglet Actions, Concepteur de Cube&#41; &#40;Analysis Services - données multidimensionnelles&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organisateur d’action &#40;onglet Actions, Concepteur de Cube&#41; &#40;Analysis Services - données multidimensionnelles&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Outils de calcul &#40;onglet Actions, Concepteur de Cube&#41; &#40;Analysis Services - données multidimensionnelles&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Éditeur de formulaire d’action &#40;onglet Actions, Concepteur de Cube&#41; &#40;Analysis Services - données multidimensionnelles&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Report Action Form Editor &#40;onglet Actions, Concepteur de Cube&#41; &#40;Analysis Services - données multidimensionnelles&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
