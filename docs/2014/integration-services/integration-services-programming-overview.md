---
title: Vue d’ensemble de la programmation Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services, programming
- architecture [Integration Services]
- assemblies [Integration Services]
- SSIS, programming
- SQL Server Integration Services, programming
- run-time engine [Integration Services]
- packages [Integration Services], programming
- data flow engine [Integration Services]
- languages [Integration Services]
ms.assetid: 262babc6-eea5-4609-bc65-07d64cbcfee9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4bf90de7f1ebcadbc65b6f2ee7eaaacb6d52e0e1
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2019
ms.locfileid: "74683622"
---
# <a name="integration-services-programming-overview"></a>Vue d'ensemble de la programmation Integration Services
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dispose d’une architecture qui sépare le déplacement et la transformation des données du workflow et de la gestion des packages. Cette architecture se définit par deux moteurs distincts qui peuvent être automatisés et étendus lors de la programmation [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Le moteur d'exécution implémente l'infrastructure de flux de contrôle et de gestion de packages qui permet aux développeurs de contrôler le flux d'exécution et de définir des options pour la journalisation, les gestionnaires d'événements et les variables. Le moteur de flux de données est un moteur spécialisé, hautement performant, exclusivement dédié à l'extraction, la transformation et le chargement de données. La programmation [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] s'effectue à partir de ces deux moteurs.  
  
 L'image suivante représente l'architecture d'[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 ![Architecture Integration Services](media/mw-dts-01.gif "Architecture Integration Services")  
  
## <a name="integration-services-run-time-engine"></a>Moteur d'exécution Integration Services  
 Le moteur d'exécution [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contrôle la gestion et l'exécution de packages, en implémentant l'infrastructure qui active l'ordre d'exécution, la journalisation, les variables et la gestion d'événements. La programmation du moteur d'exécution [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] permet aux développeurs d'automatiser la création, la configuration et l'exécution de packages et de créer des tâches personnalisées et d'autres extensions.  
  
 Pour plus d’informations, consultez [Extension du package à l’aide de la tâche de script](extending-packages-scripting/task/extending-the-package-with-the-script-task.md), [Développement d’une tâche personnalisée](extending-packages-custom-objects/task/developing-a-custom-task.md) et [Génération de packages par programmation](building-packages-programmatically/building-packages-programmatically.md).  
  
## <a name="integration-services-data-flow-engine"></a>Moteur de flux de données Integration Services  
 Le moteur de flux de données gère la tâche de flux de données, qui est une tâche spécialisée, hautement performante, destinée à déplacer et transformer les données provenant de sources disparates. Contrairement à d'autres tâches, la tâche de flux de données contient des objets supplémentaires, appelés composants de flux de données, qui peuvent être des sources, des transformations ou des destinations. Ces composants constituent les principaux éléments en mouvement de la tâche. Ils définissent le déplacement et la transformation des données. La programmation du moteur de flux de données permet aux développeurs d'automatiser la création et la configuration des composants dans une tâche de flux de données et de créer des composants personnalisés.  
  
 Pour plus d’informations, consultez [extension du workflow de données à l’aide du composant Script] (extension-packages-Scripting/Workflow-script-Component/extension-The-Data-Flow-with-the-script-Component. MD, [développement d’un composant de transmission de données personnalisé](extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)et [génération de packages par programmation](building-packages-programmatically/building-packages-programmatically.md)).  
  
## <a name="supported-languages"></a>Langues prises en charge  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]prend entièrement en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]charge. Les développeurs peuvent ainsi programmer [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dans les langages compatibles .NET de leur choix. Bien qu'ils soient écrits en code natif, le moteur d'exécution et le moteur de flux de données sont accessibles par le biais d'un modèle objet entièrement managé.  
  
 Vous pouvez programmer [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] des packages, des tâches personnalisées et [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] des composants dans ou dans un autre code ou éditeur de texte. 
  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] offre de nombreux outils et fonctionnalités au développeur pour simplifier et accélérer les cycles itératifs du codage, du débogage et du test. 
  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] facilite également le déploiement. Toutefois, vous n'avez pas besoin de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] pour compiler et générer des projets de code [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Le Kit de développement [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK inclut les compilateurs et les outils connexes [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] et [!INCLUDE[csprcs](../includes/csprcs-md.md)].  
  
> [!IMPORTANT]  
>  Le [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] est installé par défaut avec [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mais pas le Kit de développement [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK. Les liens vers les rubriques relatives au Kit de développement figurant dans cette section ne fonctionnent que si le Kit de développement est installé sur l'ordinateur et que la documentation qui lui est propre figure dans la documentation en ligne. Après avoir installé le SDK [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], vous pouvez ajouter la documentation le concernant à la documentation en ligne et à la table des matières en suivant les instructions figurant dans [Ajouter ou supprimer la documentation du produit SQL Server](../2014-toc/index.yml).  
  
 La [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tâche de script et le composant [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] script utilisent Tools for Applications (VSTA) comme environnement de script incorporé. VSTA prend en charge [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic et [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#.  
  
> [!NOTE]  
>  Les interfaces de programmation d'applications [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sont incompatibles avec les langages de script COM, tels que VBScript.  
  
## <a name="locating-assemblies"></a>Recherche d'assemblys  
 Dans [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], les assemblys [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ont été mis à niveau vers le .NET 4.0. Il existe un global assembly cache distinct pour .net 4, situé dans * \<le lecteur>*: \Windows\Microsoft.NET\assembly. Vous trouverez tous les assemblys [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sous ce chemin d'accès, en général dans le dossier GAC_MSIL.  
  
 Comme dans les versions précédentes [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de, les [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fichiers. dll d’extensibilité de base se trouvent également dans le * \<lecteur>*: \Program Files\Microsoft SQL Server\100\SDK\Assemblies.  
  
## <a name="commonly-used-assemblies"></a>Assemblys couramment utilisés  
 Le tableau suivant répertorie les assemblys fréquemment utilisés lors de la programmation [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] à l'aide du [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
|Assembly|Description|  
|--------------|-----------------|  
|Microsoft.SqlServer.ManagedDTS.dll|Contient le moteur d'exécution managé.|  
|Microsoft.SqlServer.RuntimeWrapper.dll|Contient l'assembly PIA (Primary Interop Assembly), ou wrapper, du moteur d'exécution natif.|  
|Microsoft.SqlServer.PipelineHost.dll|Contient le moteur de flux de données managé.|  
|Microsoft.SqlServer.PipelineWrapper.dll|Contient l'assembly PIA (Primary Interop Assembly), ou wrapper, du moteur de flux de données natif.|  

![Icône de Integration Services (petite)](media/dts-16.gif "Icône Integration Services (petite)")  **restez à jour avec Integration Services**<br /> Pour obtenir les derniers téléchargements, articles, exemples et vidéos de Microsoft, ainsi que des solutions sélectionnées par la communauté, visitez la page [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sur MSDN :<br /><br /> [Visitez la page Integration Services sur MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Pour recevoir une notification automatique de ces mises à jour, abonnez-vous aux flux RSS disponibles sur la page.  
  
  
