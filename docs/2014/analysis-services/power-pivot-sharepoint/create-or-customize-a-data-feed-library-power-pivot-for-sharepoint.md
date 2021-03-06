---
title: Créer ou personnaliser une bibliothèque de flux de données (PowerPivot pour SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data feed library
- data feeds [Analysis Services with SharePoint]
ms.assetid: 699fbeb9-42ab-436b-beba-214db51ea3dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 31e69ddc36079c993e66a7e9253bfdd178057302
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071557"
---
# <a name="create-or-customize-a-data-feed-library-powerpivot-for-sharepoint"></a>Créer ou personnaliser une bibliothèque de flux de données (PowerPivot pour SharePoint)
  Une *bibliothèque de flux de données* est une bibliothèque SharePoint spécifique qui permet d’enregistrer et de partager des documents de service de données Atom (.atomsvc). Ces documents fournissent des flux XML aux classeurs [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou à d'autres applications clientes qui prennent en charge le format de flux Atom. Une bibliothèque de flux de données est différente des autres bibliothèques SharePoint, car elle vous donne la possibilité :  
  
-   de créer ou modifier un *document de service de données*, utilisé pour spécifier une connexion HTTP à un flux spécifique ;  
  
-   de partager et gérer des documents de service de données depuis un emplacement central ;  
  
-   d'identifier visuellement des documents de service de données à l'aide d'une icône, ce qui vous permet de distinguer facilement les documents de service des autres documents stockés dans la même bibliothèque : ![GMNI_IconDataFeed](../media/gmni-icondatafeed.gif "GMNI_IconDataFeed")  
  
 Une bibliothèque de flux de données contient toujours des fichiers de documents de service de données (.atomsvc), et jamais le flux de données lui-même. Contrairement à un flux de données, qui est constitué de données XML statiques, le document de service de données spécifie l'URL d'un service ou d'une application qui génère un flux à la demande, fournissant ainsi des informations de connexion réutilisables pour les opérations d'importation répétées.  
  
 Cette rubrique contient les sections suivantes :  
  
 [Conditions préalables](#prereq)  
  
 [Créer une bibliothèque de flux](#createlib)  
  
 [Ajouter le type de contenu du flux à une bibliothèque](#addtolib)  
  
##  <a name="prereq"></a> Conditions préalables  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] L’intégration de la fonctionnalité doit être activée pour les sites pour lesquels vous créez la bibliothèque de flux de données. Si le type de modèle de bibliothèque de flux n'est pas disponible, la cause en est probablement que cette condition préalable n'est pas respectée. Pour plus d’informations, consultez [activer fonctionnalité d’intégration PowerPivot pour les Collections de sites dans l’Administration centrale](activate-power-pivot-integration-for-site-collections-in-ca.md).  
  
 Vous devez être propriétaire de site pour créer la bibliothèque.  
  
##  <a name="createlib"></a> Créer une bibliothèque de flux  
 La création d’une bibliothèque de flux de données est la première étape de l’activation des flux de données pour les classeurs [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Avant de pouvoir créer un document, une bibliothèque de flux doit être en place, car c'est elle qui fournit les pages d'application et de gestion de documents de service de données.  
  
 Une bibliothèque de flux de données est basée sur un modèle intégré et sur un *type de contenu de document de service de données* préconfiguré qui définit les propriétés et comportements d’un document de service de données.  
  
1.  Cliquez sur **Actions du site** dans l’angle supérieur gauche de la page.  
  
2.  Cliquez sur **davantage d’Options**...  
  
3.  Sous Bibliothèques, cliquez sur **Bibliothèque de flux de données**.  
  
4.  Tapez le nom et la description, ainsi que les préférences en termes de démarrage et de version. Incluez des informations descriptives pour aider les utilisateurs à identifier cette bibliothèque en tant qu'emplacement de stockage pour les documents de service de données.  
  
5.  Cliquez sur **Créer**.  
  
 Un lien vers la bibliothèque de flux s'affiche dans le volet de navigation Lancement rapide du site actuel.  
  
 Après avoir créé une bibliothèque, vous pouvez l'utiliser pour créer des documents de service de données. Pour plus d’informations, consultez [utiliser des flux de données &#40;PowerPivot pour SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="addtolib"></a> Ajouter le type de contenu du flux à une bibliothèque  
 Si vous ne souhaitez pas créer de bibliothèque de flux de données dédiée, mais souhaitez toujours créer et gérer des documents de service de données à partir d'un site SharePoint, vous pouvez ajouter et configurer manuellement le type de contenu de document de service de données pour toute bibliothèque que vous utiliserez pour partager des fichiers de documents de service de données (.atomsvc).  
  
 Pour ajouter et configurer un type de contenu, vous devez au minimum disposer d'une autorisation Gérer les listes. Cette autorisation est intégrée au niveau d'autorisation de conception et aux niveaux supérieurs.  
  
 Les étapes suivantes doivent être répétées pour chaque bibliothèque dans laquelle vous souhaitez créer ou modifier des documents d'inscription de flux de données.  
  
#### <a name="step-1-enable-content-type-management"></a>Étape 1 : Activer la gestion du Type de contenu  
  
1.  Ouvrez la bibliothèque de documents pour laquelle activer plusieurs types de contenu.  
  
2.  Sur le ruban SharePoint, dans Outils de bibliothèque, cliquez sur **Bibliothèque**.  
  
3.  Cliquez sur **Paramètres**.  
  
4.  Cliquez sur **Paramètres de la bibliothèque**.  
  
5.  Sous Paramètres généraux, cliquez sur **Paramètres avancés**.  
  
6.  Dans Types de contenu, dans la section « Autoriser la gestion des types de contenu ? », cliquez sur **Oui**.  
  
7.  Cliquez sur **OK**.  
  
#### <a name="step-2-add-the-data-service-document-content-type"></a>Étape 2 : Ajouter le Type contenu de Document de Service de données  
  
1.  Dans la section Types de contenu, cliquez sur **Ajouter à partir de types de contenu de site existants**. Si vous ne voyez pas cette page, retournez au site, cliquez sur **Bibliothèque** dans Outils de bibliothèque, puis sur **Paramètres de la bibliothèque**.  
  
2.  Dans Types de contenu, cliquez sur **Ajouter à partir de types de contenu de site existants**.  
  
3.  Dans Sélectionner des types de contenu dans, sélectionnez **Aide à la décision**.  
  
4.  Dans Types de contenu de site disponibles, cliquez sur **Document de service de données**, puis sur **Ajouter** pour déplacer le type de contenu sélectionné dans la liste Types de contenu à ajouter.  
  
5.  Cliquez sur **OK**.  
  
#### <a name="step-3-verify-data-service-document-configuration"></a>Étape 3 : Vérifier la Configuration de Document de Service de données  
  
1.  Ouvrez la page d'accueil du site.  
  
2.  Ouvrez la bibliothèque.  
  
3.  Sur le ruban SharePoint, cliquez sur **Documents**.  
  
4.  Cliquez sur la flèche vers le bas de Nouveau document et sélectionnez **Document de service de données**. La page Nouveau document de service de données s'affiche.  
  
## <a name="see-also"></a>Voir aussi  
 [Utiliser des flux de données &#40;PowerPivot pour SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md)   
 [Supprimer une bibliothèque de flux de données PowerPivot](delete-a-power-pivot-data-feed-library.md)   
 [Administration de serveur PowerPivot et de Configuration dans l’Administration centrale](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Flux de données PowerPivot](power-pivot-data-feeds.md)  
  
  
