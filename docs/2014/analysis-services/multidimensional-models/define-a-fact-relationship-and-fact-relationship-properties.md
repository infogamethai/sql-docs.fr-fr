---
title: Définir une relation de faits et les propriétés de relation de faits | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 471a65cb8f7560b409e6ddf8f73969d83d42a346
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075787"
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>Définir une relation de fait et des propriétés de relation de fait
  Quand vous définissez une nouvelle dimension de cube ou un nouveau groupe de mesures, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tente de détecter si une relation de dimension de fait existe et attribut la valeur `Fact` au paramètre d'utilisation de la dimension. Vous pouvez afficher ou modifier une relation de dimension de fait sur l'onglet **Utilisation de la dimension** du Concepteur de cube. La relation de fait entre une dimension et un groupe de mesures a les contraintes suivantes :  
  
-   Une dimension de cube ne peut avoir qu'une seule relation de fait avec un groupe de mesures donné.  
  
-   Une dimension de cube peut avoir des relations de fait distinctes avec plusieurs groupes de mesures.  
  
-   L'attribut de granularité de la relation doit correspondre à l'attribut clé (comme le numéro de transaction) de la dimension. Cela crée une relation de type un-à-un entre les faits et la dimension de la table de faits.  
  
  
