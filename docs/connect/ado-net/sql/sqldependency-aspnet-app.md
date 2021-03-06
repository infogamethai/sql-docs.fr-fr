---
title: SqlDependency dans une application ASP.NET
description: Montre comment utiliser les notifications de requête à partir d'une application Windows Forms.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2115d087d837118b99ee3ffded9cae0003b6d4e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451963"
---
# <a name="sqldependency-in-an-aspnet-application"></a>SqlDependency dans une application ASP.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Télécharger ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

L’exemple de cette section montre comment utiliser <xref:Microsoft.Data.SqlClient.SqlDependency> indirectement en tirant parti de l’objet ASP.NET <xref:System.Web.Caching.SqlCacheDependency>. L’objet <xref:System.Web.Caching.SqlCacheDependency> utilise un <xref:Microsoft.Data.SqlClient.SqlDependency> pour écouter les notifications et mettre correctement à jour le cache.  
  
> [!NOTE]
>  L’exemple de code suppose que vous avez activé les notifications de requête en exécutant les scripts dans [l’activation des notifications de requête](enable-query-notifications.md).  
  
## <a name="about-the-sample-application"></a>Test de l'exemple d'application  
L’exemple d’application utilise une page web ASP.NET unique pour afficher les références des produits extraites de la base de données SQL Server **AdventureWorks** dans un contrôle <xref:System.Web.UI.WebControls.GridView>. Lors du chargement de la page, le code écrit l’heure actuelle dans un contrôle de <xref:System.Web.UI.WebControls.Label>. Il définit ensuite un objet <xref:System.Web.Caching.SqlCacheDependency> et définit des propriétés sur l’objet <xref:System.Web.Caching.Cache> pour stocker les données du cache pendant trois minutes maximum. Le code se connecte ensuite à la base de données et récupère les données. Lorsque la page est chargée et que l’application est en cours d’exécution, ASP.NET récupère les données du cache, que vous pouvez vérifier en notant que l’heure sur la page ne change pas. Si les données surveillées sont modifiées, ASP.NET invalide le cache et remplit à nouveau le contrôle de `GridView` avec les données actualisées, en mettant à jour l’heure affichée dans le contrôle `Label`.  
  
## <a name="creating-the-sample-application"></a>Création de l’exemple d’application  
Pour créer et exécuter l’exemple d’application, procédez comme suit :  
  
1. Créez un site web ASP.NET.  
  
2. Ajoutez un <xref:System.Web.UI.WebControls.Label> et un contrôle <xref:System.Web.UI.WebControls.GridView> à la page default. aspx.  
  
3. Ouvrez le module de classe de la page et ajoutez les directives suivantes :  
  
    ```csharp  
    using Microsoft.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. Ajoutez le code suivant dans l’événement `Page_Load` de la page :  
  
    [!code-csharp[DataWorks SqlDependency_Start#1](~/../sqlclient/doc/samples/SqlDependency_Start.cs#1)]
  
5. Ajoutez deux méthodes d’assistance, `GetConnectionString` et `GetSQL`. La chaîne de connexion définie utilise une sécurité intégrée. Vous devez vérifier que le compte que vous utilisez dispose des autorisations de base de données nécessaires et que les notifications sont activées dans l’exemple de base de données, **AdventureWorks**.
  
    [!code-csharp[DataWorks SqlDependency_Start#2](~/../sqlclient/doc/samples/SqlDependency_Start.cs#2)]
  
### <a name="testing-the-application"></a>Test de l’application  
L’application met en cache les données affichées sur le formulaire Web et l’actualise toutes les trois minutes en l’absence d’activité. Si une modification est apportée à la base de données, le cache est actualisé immédiatement. Exécutez l’application à partir de Visual Studio, qui charge la page dans le navigateur. L’heure d’actualisation du cache affichée indique à quel moment le cache a été actualisé pour la dernière fois. Attendez trois minutes, puis actualisez la page, provoquant ainsi l’exécution d’un événement de publication (postback). Notez que l’heure affichée sur la page a changé. Si vous actualisez la page en moins de trois minutes, l’heure affichée sur la page reste la même.  
  
À présent, mettez à jour les données dans la base de données, à l’aide d’une commande Transact-SQL UPDATE et actualisez la page. L’heure affichée indique maintenant que le cache a été actualisé avec les nouvelles données de la base de données. Notez que même si le cache est mis à jour, l’heure affichée sur la page n’est pas modifiée tant qu’un événement de publication ne se produit pas.  
  
## <a name="next-steps"></a>Étapes suivantes
- [Notifications de requête dans SQL Server](query-notifications-sql-server.md)
