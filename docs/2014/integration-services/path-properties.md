---
title: Propriétés du chemin d’accès | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- paths [Integration Services], properties
ms.assetid: 89b1e347-9579-4f6b-af74-c6519ea08eea
caps.latest.revision: 25
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9d5917edcf5038028075d0f71b70a8e90acc53d7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285425"
---
# <a name="path-properties"></a>Propriétés du chemin d'accès
  Les objets de flux de données dans le modèle d’objet [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ont des propriétés communes et des propriétés personnalisées au niveau du composant, des entrées et sorties, et des colonnes d’entrée et colonnes de sortie. De nombreuses propriétés ont des valeurs en lecture seule qui sont assignées au moment de l'exécution par le moteur de flux de données.  
  
 Cette rubrique répertorie et décrit les propriétés personnalisées des chemins d'accès qui connectent des objets de flux de données.  
  
## <a name="path-properties"></a>Propriétés du chemin d'accès  
 Dans le modèle objet [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], un chemin d'accès qui connecte des composants dans le flux de données implémente l'interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>.  
  
 Le tableau suivant décrit les propriétés configurables des chemins d'accès dans un flux de données. Le moteur de flux de données assigne également des valeurs à d'autres propriétés en lecture seule qui ne sont pas répertoriées ici.  
  
|Nom de la propriété|Type de données|Description|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Integer (énumération)|Valeur qui indique si une annotation doit être affichée avec le chemin d'accès sur l'aire du concepteur. Les valeurs possibles sont `AsNeeded`, `SourceName`, `PathName`, et `Never`. La valeur par défaut est `AsNeeded`.|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|Entrée associée au chemin d'accès.|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|Sortie associée au chemin d'accès.|  
  
## <a name="see-also"></a>Voir aussi  
 [Chemins Integration Services](data-flow/integration-services-paths.md)   
 [Propriétés communes](../../2014/integration-services/common-properties.md)   
 [Propriétés personnalisées de transformation](data-flow/transformations/transformation-custom-properties.md)   
 [Propriétés du flux de données pouvant être définies à l’aide d’expressions](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  