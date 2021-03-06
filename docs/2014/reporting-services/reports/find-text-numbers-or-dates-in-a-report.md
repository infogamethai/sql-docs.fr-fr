---
title: Rechercher du texte, des nombres ou des Dates dans un rapport (Reporting Services en Mode intégré SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- searching reports
ms.assetid: 309dffe5-00f5-404f-bb63-9e6046253ae0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6cf40f4d3baa60caa0d9d44f372e41521497e33e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102669"
---
# <a name="find-text-numbers-or-dates-in-a-report-reporting-services-in-sharepoint-integrated-mode"></a>Rechercher du texte, des nombres ou des dates dans un rapport (Reporting Services en mode intégré SharePoint)
  Vous pouvez rechercher du contenu dans un rapport en tapant un mot ou une expression que vous souhaitez trouver (la longueur maximale de la chaîne de recherche est de 256 caractères). La recherche est une technique de navigation qui vous permet de trouver une valeur correspondante dans le rapport et de placer le focus sur la partie du rapport qui contient cette valeur.  
  
 La recherche respecte la casse et commence au niveau de la page ou de la section actuellement sélectionnée. Seul le contenu visible dans le rapport est inclus dans l'opération de recherche. Si le rapport contient des zones que vous pouvez développer ou réduire, les valeurs qui figurent dans une zone réduite sont ignorées durant la recherche. Vous ne pouvez rechercher que du texte, des nombres ou des dates figurant dans le rapport actuel. Si vous utilisez un rapport consultable à l'aide de clics et généré automatiquement pour l'exploration des données, vous ne pouvez pas rechercher un terme aperçu dans un rapport généré antérieurement ; par ailleurs, vous ne pouvez pas non plus utiliser la fonctionnalité de recherche pour trouver un terme susceptible d'apparaître dans un rapport situé plus loin dans le chemin d'accès aux données.  
  
 Lorsque vous entrez une valeur à rechercher, tapez-la telle qu'elle est censée apparaître dans le rapport. Ne posez pas une question de type « quel est le bénéfice moyen pour ce mois-ci » à moins que chaque mot de la phrase ne soit censé figurer dans le rapport.  
  
 Vous ne pouvez rechercher qu'un seul terme ou une seule valeur à la fois. Vous ne pouvez pas utiliser d'opérateurs de recherche (par exemple ET ou OU), de symboles ou de caractères génériques. Vous ne pouvez pas effectuer de recherche dans une section croisée des données (par exemple rechercher le chiffre d'affaires correspondant à un mois spécifique pour un produit particulier). Pour ce type d'analyse, utilisez le Générateur de rapports afin de créer des rapports générés interactifs.  
  
 Les paramètres de sécurité de base de données et de modèle qui restreignent l'accès aux données de rapport s'appliquent également aux opérations de recherche. Si vous recherchez une valeur dans un rapport consultable à l'aide de clics qui utilise un modèle comme source de données, et si vous n'avez pas accès à une partie du modèle, les données représentées par cette partie du modèle sont exclues de la recherche.  
  
### <a name="to-find-data-in-a-report"></a>Pour rechercher des données dans un rapport  
  
1.  Ouvrez le rapport.  
  
2.  Dans la barre d'outils de rapport, entrez le texte, la valeur numérique ou la date à rechercher.  
  
     Si la barre d'outils de rapport n'est pas visible, elle a été masquée délibérément et vous ne pouvez pas utiliser les fonctionnalités qu'elle propose. Les propriétés définies pour le composant WebPart Visionneuse de rapports déterminent si la barre d'outils est visible ou non.  
  
3.  Cliquez sur **Rechercher**.  
  
4.  Pour rechercher d'autres occurrences de la même valeur, cliquez sur **Suivant**.  
  
## <a name="see-also"></a>Voir aussi  
 [Ajouter le composant WebPart Visionneuse de rapports à une page web &#40;Reporting Services en mode intégré SharePoint&#41;](../report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  
