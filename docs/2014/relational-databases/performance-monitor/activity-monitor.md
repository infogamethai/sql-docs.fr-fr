---
title: Moniteur d’activité | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server]
ms.assetid: 1e6c430d-3a2a-468e-a3d5-ef5459c36c15
caps.latest.revision: 5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1e82e9c32d7b3c31b22fc22338733003ea7fba5b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37219199"
---
# <a name="activity-monitor"></a>Moniteur d'activité
  Le Moniteur d'activité affiche des informations sur les processus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] et sur la façon dont ces processus affectent l'instance actuelle de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="benefits-of-activity-monitor"></a>Avantages du Moniteur d'activité  
 Moniteur d’activité est une fenêtre de document à onglets qui compose les volets suivants extensibles et réductibles : **vue d’ensemble**, **tâches utilisateur actives**, **attentes de ressources**, **D’e/s du fichier de données**, et **requêtes coûteuses récentes**. Lorsqu'un volet est développé, le Moniteur d'activité interroge l'instance pour obtenir des informations. Lorsqu'un volet est réduit, toutes les activités d'interrogation cessent pour ce volet. Vous pouvez également développer en même temps un ou plusieurs volets pour afficher différents types d'activité sur l'instance.  
  
 Pour les colonnes qui sont inclus dans le **tâches utilisateur actives**, **attentes de ressources**, **e/s de fichier de données**, et **requêtes coûteuses récentes** volets, vous pouvez personnaliser l’affichage de plusieurs manières :  
  
1.  Pour réorganiser l'ordre des colonnes, cliquez sur l'en-tête de colonne et faites-le glisser vers un autre emplacement dans le ruban de titre.  
  
2.  Pour trier une colonne, cliquez sur son nom.  
  
3.  Pour effectuer un filtrage sur une ou plusieurs colonnes, cliquez sur la flèche de déroulement de l'en-tête de colonne, puis sélectionnez une valeur.  
  
## <a name="related-tasks"></a>Related Tasks  
 Utilisez les tâches suivantes pour commencer à utiliser le Moniteur d'activité :  
  
|||  
|-|-|  
|**Description**|**Rubrique**|  
|Décrit comment ouvrir le Moniteur d'activité et définir son intervalle d'actualisation.|[Ouvrir le Moniteur d’activité &#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)|  
|Liens vers des rubriques relatives à la surveillance des performances et de l'activité du serveur.|[Analyse des performances et surveillance de l'activité du serveur](../performance/server-performance-and-activity-monitoring.md)|  
  
  