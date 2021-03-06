---
title: Application sqlagent90 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server Agent
- sqlagent90 application
- SQL Server Agent, starting
- command prompt utilities [SQL Server], sqlagent90
ms.assetid: e8b80e8d-d0c9-4500-a868-0ce08233da08
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 20405a10a2e36232068329542923aae65c10c4e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059592"
---
# <a name="sqlagent90-application"></a>application sqlagent90
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  L’application **sqlagent90** démarre [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent à partir de l’invite de commandes. En règle générale, l'Agent [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] doit être exécuté à partir de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou en utilisant des méthodes SQL-SMO dans une application. N’exécutez **sqlagent90** à partir de l’invite de commandes que si vous effectuez un diagnostic de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent, ou lorsque vous y êtes invité par votre fournisseur de support principal.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sqlagent90  
-c [-v] [-i instance_name]  
```  
  
## <a name="arguments"></a>Arguments  
 **-c**  
 Indique que l'Agent [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] s'exécute depuis l'invite de commandes et est indépendant du Gestionnaire de contrôle du service Windows. Lorsque **-c** est utilisé, l’Agent [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ne peut pas être commandé depuis l’application Services dans les Outils d’administration ni depuis le Gestionnaire de configuration de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Cet argument est obligatoire.  
  
 **-v**  
 Indique que l'Agent [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] s'exécute en mode documenté et inscrit les informations de diagnostic dans la fenêtre de l'invite de commandes. Les informations de diagnostic sont semblables à celles inscrites dans le journal des erreurs de l'Agent [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **-i** *instance_name*  
 Indique que l’Agent [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se connecte à l’instance [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nommée qui est spécifiée par l’argument *instance_name*.  
  
## <a name="remarks"></a>Notes  
 Après avoir affiché un message de copyright, **sqlagent90** ne présente une sortie dans la fenêtre d’invite de commandes que si le commutateur **-v** a été spécifié. Pour arrêter **sqlagent90**, appuyez sur CTRL+C à l’invite de commandes. Ne fermez pas la fenêtre d’invite de commandes avant d’arrêter **sqlagent90**.  
  
## <a name="see-also"></a>Voir aussi  
 [Tâches d’administration automatisée &#40;SQL Server Agent&#41;](https://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)  
  
  
