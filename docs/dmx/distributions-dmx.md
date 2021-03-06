---
title: Distributions (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fda2eb169985eb670614f611764fbf149c71a42d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892794"
---
# <a name="distributions-dmx"></a>Distributions (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Dans [!INCLUDE[msCoName](../includes/msconame-md.md)] ,vouspouvez[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]définir le contenu des colonnes dans une structure d’exploration de données, pour affecter la façon dont les algorithmes traitent les données dans ces colonnes lorsque vous créez des modèles d’exploration de données. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Pour certains algorithmes, il est judicieux de définir la distribution des colonnes continues avant de traiter le modèle, s'il est établi que les colonnes contiennent des distributions de valeurs communes. Si vous ne définissez pas de distributions, les modèles d'exploration de données obtenus risquent de générer des prévisions moins précises, car les algorithmes disposent dans ce cas d'une moins grande quantité d'informations pour interpréter les données.  
  
 Les algorithmes d'exploration de données [!INCLUDE[msCoName](../includes/msconame-md.md)] prennent en charge les types de distribution suivants :  
  
 **NORMAL**  
 Les valeurs de la colonne continue forment un histogramme à distribution gaussienne normale.  
  
 **Log-normale**  
 Les valeurs de la colonne continue forment un histogramme dans lequel le logarithme des valeurs est normalement distribué.  
  
 **UNIFORME**  
 Les valeurs de la colonne continue forment une courbe plate, dont toutes les valeurs sont sensiblement les mêmes.  
  
 Pour plus d’informations [!INCLUDE[msCoName](../includes/msconame-md.md)] sur les algorithmes d’exploration de données, consultez algorithmes d' [exploration de données &#40;Analysis Services-exploration&#41;de données](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining). Des algorithmes tiers peuvent prendre en charge des types de distribution supplémentaires. Pour déterminer les types de distribution pris en charge par un algorithme, utilisez l’ensemble de lignes de schéma **SUPPORTED_DISTRIBUTION_FLAGS** .  
  
 Pour plus d’informations sur les types de distribution, consultez [ &#40;Data distributions Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining).  
  
## <a name="see-also"></a>Voir aussi  
 [Types de contenu &#40;Exploration de données&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)   
 [Référence DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Éléments de syntaxe &#40;DMX&#41; des extensions d’exploration de données](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Référence des fonctions &#40;DMX&#41; des extensions d’exploration de données](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Référence des opérateurs &#40;DMX&#41; Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Référence des instructions &#40;DMX&#41; Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Conventions de la &#40;syntaxe&#41; DMX des extensions d’exploration de données](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Fonctions &#40;de prédiction générales DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Structure et utilisation des requêtes de prédiction DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Présentation de l’instruction DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
