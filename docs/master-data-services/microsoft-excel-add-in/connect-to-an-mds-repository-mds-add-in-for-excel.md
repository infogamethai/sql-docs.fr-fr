---
title: Se connecter à un référentiel MDS (Complément MDS pour Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8f427312-4c09-4c8b-b9f9-8b235557a74b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 711c76e4db62c274fe62d2319b3438799954d1c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139368"
---
# <a name="connect-to-an-mds-repository-mds-add-in-for-excel"></a>Se connecter à un référentiel MDS (Complément MDS pour Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Dans le [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], vous devez vous connecter à un référentiel MDS avant de pouvoir charger ou publier des données.  
  
## <a name="prerequisites"></a>Prérequis  
 Pour effectuer cette procédure :  
  
-   Vous devez avoir l'autorisation d'accéder à la zone fonctionnelle **Explorateur** .  
  
### <a name="to-connect-to-an-mds-repository"></a>Pour vous connecter à un référentiel MDS  
  
1.  Dans le Complément MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], sous l’onglet **Données de référence** , dans le groupe **Se connecter et charger** , cliquez sur la flèche du bas sous le bouton **Se connecter** et cliquez sur **Gérer les connexions**.  
  
2.  Dans la boîte de dialogue **Gérer les connexions** , dans la section **Nouvelle connexion** , cliquez sur **Créer une connexion**.  
  
3.  Cliquez sur **Nouveau**.  
  
4.  Dans la boîte de dialogue **Ajouter une nouvelle connexion** , dans le champ **Description** , tapez une description pour votre connexion. Cette connexion s’affiche lorsque vous cliquez sur la flèche sous le bouton **Se connecter** dans la barre d’outils.  
  
5.  Dans la zone **Adresse du serveur MDS**, tapez l’URL de l’application web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], par exemple `https://contoso/mds`.  
  
    > [!NOTE]  
    >  Vérifiez que vous utilisez le nom d’ordinateur ; n’utilisez pas « localhost ».  
  
6.  Cliquez sur **OK**. Le nom est affiché dans la section **Connexions existantes** .  
  
7.  Vous pouvez également cliquer sur **Tester** pour tester la connexion. Une boîte de dialogue de confirmation ou d'erreur s'affiche. Cliquez sur **OK** pour la fermer.  
  
8.  Cliquer sur **Se connecter**. Le volet **Master Data Services** est affiché.  
  
## <a name="next-steps"></a>Étapes suivantes  
  
-   [Exporter des données vers Excel à partir de Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)  
  
-   [Filtrer les données avant l’exportation &#40;Complément MDS pour Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Connexions &#40;Complément MDS pour Excel#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
  
