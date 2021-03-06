---
title: Exécuter Windows PowerShell à partir de SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c6d71f1158ef73b84e5b04dcc9a1970bfd7dce35
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783103"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Exécuter Windows PowerShell à partir de SQL Server Management Studio
  Vous pouvez démarrer des sessions Windows PowerShell à partir de l' **Explorateur d'objets** dans [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] lance Windows PowerShell, charge le module `sqlps` et définit le contexte de chemin d’accès sur le nœud associé dans l’arborescence de l' **Explorateur d’objets** .  
  
## <a name="before-you-begin"></a>Avant de commencer  
 Quand vous spécifiez l’exécution de PowerShell pour un objet dans l’ **Explorateur d’objets**, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] démarre une session Windows PowerShell dans laquelle les composants logiciels enfichables [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell ont été chargés et inscrits. Le chemin d'accès de la session est prédéfini avec l'emplacement de l'objet sur lequel vous avez cliqué avec le bouton droit dans l'Explorateur d'objets. Par exemple, si vous cliquez avec le bouton droit sur l’objet de base de données [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] dans l’Explorateur d’objets et que vous sélectionnez **Démarrer PowerShell**, le chemin Windows PowerShell est défini comme suit :  
  
```
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="to-run-powershell-from-sql-server-management-studio"></a>Pour exécuter PowerShell à partir de SQL Server Management Studio 
  
1.  Ouvrez l' **Explorateur d'objets**.  
  
2.  Accédez au nœud de l'objet à utiliser.  
  
3.  Cliquez avec le bouton droit sur l’objet et sélectionnez **Démarrer PowerShell**.  
  
## <a name="permissions"></a>Permissions  
 S'il a été ouvert à partir de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], PowerShell ne fonctionne pas avec les privilèges d'administrateur, ce qui peut empêcher certaines activités telles que les appels à WMI.  
  
## <a name="see-also"></a>Voir aussi  
 [SQL Server PowerShell](sql-server-powershell.md)  
