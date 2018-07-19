---
title: Annuler l’inscription de plusieurs serveurs cibles dans un serveur maître | Microsoft Docs
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
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
- multiple target server defections
ms.assetid: 61a3713b-403a-4806-bfc4-66db72ca1156
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e89114908358520f09dccb8ca618b700d6d030e2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278236"
---
# <a name="defect-multiple-target-servers-from-a-master-server"></a>Annuler l'inscription de plusieurs serveurs cibles dans un serveur maître
  Cette rubrique explique comment annuler l'inscription de plusieurs serveurs cibles sur une configuration d'administration multiserveur dans [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] à l'aide de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Exécutez la procédure suivante à partir du serveur maître :  
  
##  <a name="SSMSProcedure"></a> Utilisation de SQL Server Management Studio  
  
#### <a name="to-defect-multiple-target-servers-from-a-master-server"></a>Pour annuler l'inscription de plusieurs serveurs cibles dans un serveur maître  
  
1.  Dans l' **Explorateur d'objets**, développez un serveur configuré en tant que serveur maître.  
  
2.  Cliquez avec le bouton droit sur **Agent SQL Server**, pointez sur **Administration multiserveur**, puis cliquez sur **Gérer les serveurs cibles**.  
  
3.  Cliquez sur **Publier les instructions**puis, dans la liste **Type d'instruction** , sélectionnez **Désinscrire**.  
  
4.  Sous **Destinataires**, activez l'une des options suivantes :  
  
    -   **Tous les serveurs cibles** pour annuler l'inscription de tous les serveurs cibles de ce serveur principal. Utilisez cette option si vous souhaitez désinstaller complètement la configuration de l'administration multiserveur active.  
  
    -   **Serveurs cibles sélectionnés**, puis cliquez sur la zone **Sélectionner** correspondante afin d'annuler l'inscription de certains serveurs cibles (mais pas tous) de ce serveur maître.  
  
## <a name="see-also"></a>Voir aussi  
 [Créer un environnement multi-serveur](create-a-multiserver-environment.md)   
 [Administration automatisée à l'échelle d'une entreprise](automated-administration-across-an-enterprise.md)   
 [Annuler l’inscription d’un serveur cible dans un serveur maître](defect-a-target-server-from-a-master-server.md)  
  
  