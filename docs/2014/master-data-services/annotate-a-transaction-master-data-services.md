---
title: Annoter une transaction (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- annotations [Master Data Services], for transactions
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 87e33ff166f07c10ee8b0b32eac5590f486e70c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483915"
---
# <a name="annotate-a-transaction-master-data-services"></a>Annoter une transaction (Master Data Services)
  Dans [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], annotez une transaction lorsque vous souhaitez fournir des informations de prise en charge relatives à la transaction à des fins d'historique.  
  
> [!NOTE]  
>  Vous ne pouvez pas supprimer des annotations.  
  
## <a name="prerequisites"></a>Prérequis  
  
-   Pour annoter des transactions que vous avez créées, vous devez avoir l’autorisation d’accéder à la zone fonctionnelle **Explorateur** et disposer au minimum de l’autorisation **Mettre à jour** sur l’objet de modèle que vous souhaitez annoter.  
  
-   Pour annoter des transactions pour tous les utilisateurs, vous devez avoir l’autorisation d’accéder à la zone fonctionnelle **Gestion des versions** et être administrateur de modèle. Pour plus d’informations, consultez [Administrateurs &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-annotate-a-transaction-in-explorer"></a>Pour annoter une transaction dans l'Explorateur  
  
1.  Dans la page d'accueil de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , dans la liste **Modèle** , sélectionnez un modèle.  
  
2.  Dans la liste **Version** , sélectionnez une version.  
  
3.  Cliquez sur **Explorateur**.  
  
4.  Dans la barre de menus, pointez sur **Entités** , puis cliquez sur l’entité qui contient le membre dont vous voulez annoter une transaction.  
  
5.  Dans la grille, cliquez sur la ligne correspondant au membre.  
  
6.  Cliquez sur **Afficher les transactions**.  
  
7.  Dans la boîte de dialogue **Afficher les transactions** , cliquez sur la transaction que vous souhaitez annoter.  
  
8.  Dans la zone en bas de la boîte de dialogue, tapez votre annotation.  
  
9. Cliquez sur **Ajouter une annotation**. L’annotation s’affiche dans le volet **Annotations** .  
  
### <a name="to-annotate-a-transaction-in-version-management-administrators-only"></a>Pour annoter une transaction dans la zone Gestion des versions (administrateurs uniquement)  
  
1.  Dans la page d’accueil de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , cliquez sur **Gestion des versions**.  
  
2.  Dans la barre de menus, cliquez sur **Transactions**.  
  
3.  Dans le volet **Transactions** , cliquez sur la ligne de la grille correspondant à la transaction que vous souhaitez annoter.  
  
4.  Dans la zone **Annotation** du volet **Annotations de transaction** , tapez votre annotation.  
  
5.  Cliquez sur **OK**.  
  
## <a name="see-also"></a>Voir aussi  
 [Annotations &#40;Master Data Services&#41;](../../2014/master-data-services/annotations-master-data-services.md)   
 [Transactions &#40;Master Data Services&#41;](../../2014/master-data-services/transactions-master-data-services.md)  
  
  
