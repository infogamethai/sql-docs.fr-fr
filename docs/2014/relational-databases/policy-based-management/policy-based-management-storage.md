---
title: Stockage de Gestion basée sur des stratégies | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e1eab3ad745a83a8a55545570e020c1f1af732ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628870"
---
# <a name="policy-based-management-storage"></a>Stockage de Gestion basée sur des stratégies
  Les stratégies sont stockées dans la base de données msdb. Après la modification d'une stratégie ou d'une condition, vous devez sauvegarder msdb. Pour plus d’informations, consultez [Sauvegarder et restaurer des bases de données système &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="storing-policies"></a>Stockage des stratégies  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] est fourni avec des stratégies qui peuvent être utilisées pour contrôler une instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Par défaut, ces stratégies ne sont pas installées sur le [!INCLUDE[ssDE](../../includes/ssde-md.md)]; Toutefois, elles peuvent être importées à partir de l’emplacement d’installation par défaut de C:\Program Files (x86) \Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033.  
  
 Vous pouvez créer directement des stratégies à l’aide du menu **Fichier/Nouveau** , puis les enregistrer dans un fichier. Cela vous permet de créer des stratégies quand vous n’êtes pas connecté à une instance du [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 L’historique de stratégie pour les stratégies évaluées dans l’instance actuelle du [!INCLUDE[ssDE](../../includes/ssde-md.md)] est conservé dans les tables système msdb. L'historique de stratégie pour les stratégies appliquées à d'autres instances du [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou appliquées à [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou à [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] n'est pas conservé.  
  
  
