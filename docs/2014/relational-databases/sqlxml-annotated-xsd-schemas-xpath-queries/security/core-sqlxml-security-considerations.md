---
title: Considérations sur la sécurité SQLXML de base | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- security [SQLXML], about security
ms.assetid: 330cd2ff-d5d5-4c8e-8f93-0869c977be94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc25af8e18e826ce6b8323d714f090ac3d571a97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010546"
---
# <a name="core-sqlxml-security-considerations"></a>Considérations de base relatives à la sécurité SQLXML
  Vous trouverez ci-après des instructions de sécurité relatives à l'utilisation de SQLXML pour l'accès aux données.  
  
-   Le fournisseur SQLXMLOLEDB expose une propriété `StreamFlags` qui vous permet de définir des indicateurs spécifiant les fonctionnalités SQLXML qui doivent être activées ou désactivées pour chaque instance spécifique. Vous pouvez utiliser cette propriété pour personnaliser votre utilisation de SQLXML et vous assurer que seuls les composants de votre choix sont activés. Pour plus d’informations, consultez [fournisseur SQLXMLOLEDB &#40;SQLXML 4.0&#41;](../../../database-engine/dev-guide/sqlxmloledb-provider-sqlxml-4-0.md).  
  
-   Lorsque des erreurs SQLXML se produisent et sont retournées, elles peuvent contenir des informations sur le schéma de base de données, notamment des noms de table, des noms de colonne ou des informations de type. Faites preuve de vigilance lorsque vous traitez ces erreurs afin que les informations concernant votre installation [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ne puissent pas être facilement détectées par des utilisateurs à qui ces informations ne sont pas destinées ou qui n'en ont pas besoin.  
  
-   En cas d'utilisation pour interroger [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou envoyer des mises à jour, SQLXML n'impose aucune limite sur la quantité de données pouvant être échangées et ne contrôle pas la taille des données dans une charge utile SQLXML avant de tenter de la traiter. Lorsque vous développez votre application à l'aide de SQLXML, c'est à vous qu'il incombe de vérifier que le système dispose de suffisamment de mémoire pour traiter les données. Par exemple, lorsque vous interrogez des données du serveur, vous devez vérifier que le client dispose de suffisamment de place en mémoire pour les recevoir. De même, si vous chargez des données sur le serveur, vous devez vérifier que le serveur dispose d'une quantité suffisante de mémoire et d'espace de stockage sur disque pour traiter et stocker les données.  
  
-   SQLXML génère dynamiquement des requêtes et des commandes de mise à jour [!INCLUDE[tsql](../../../includes/tsql-md.md)], et les envoie à [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en vue de leur exécution. SQLXML ne peut procéder autrement pour interroger et mettre à jour le serveur. Les résultats seront reçus en tant que flux (de données XML) ou en tant qu'ensemble de lignes.  
  
-   Lors de la réception des résultats de la requête, SQLXML n'exécute aucune action sur la base du contenu des données reçues. Aucun traitement supplémentaire n'est effectué en fonction du type ou du contenu des données. Les données ne sont jamais traitées sous forme de code servant à exécuter des actions.  
  
-   Lors de l'exécution de modèles XML, SQLXML traduit les requêtes XPath et DBObject contenues dans le modèle soumis dans les commandes [!INCLUDE[tsql](../../../includes/tsql-md.md)] qui sont exécutées ensuite sur [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ces commandes affectent uniquement les données existantes. Les commandes générées par SQLXML ne modifient jamais la structure de la base de données. Les utilisateurs doivent émettre des commandes explicites pour modifier la structure de la base de données, par exemple en les incluant dans un bloc `sql:query` d'un modèle.  
  
-   Lors de l'exécution de requêtes DBObject et d'instructions XPath sur des fichiers de mappage, SQLXML ne modifie en aucune façon les données dans la base de données.  
  
-   SQLXML peut apporter des modifications de mise en forme aux données en question en fonction des différences entre les modèles de données XML et [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Par exemple, le format pour spécifier une heure est différent. SQLXML tente de résoudre ces différences. En conséquence, une perte de certaines informations de précision est envisageable.  
  
-   SQLXML n'impose aucune limite sur la durée nécessaire pour traiter les données. Le traitement continuera jusqu'à ce qu’une erreur se produit ou le traitement est terminé.  
  
-   SQLXML n'écrit pas dans le système de fichiers. Si les utilisateurs souhaitent enregistrer les données qu'ils extraient de la base de données, ils doivent le faire dans leur code.  
  
-   SQLXML permet aux utilisateurs d'exécuter toute requête SQL sur la base de données. Étant donné que cette fonctionnalité ouvre essentiellement la base de données SQL sans provision à tous les utilisateurs, elle ne doit jamais être exposée à une source non sécurisée ou non contrôlée.  
  
-   Lors de l'exécution de codes de mise à jour (updategrams), SQLXML traduit les blocs `updg:sync` en commandes DELETE, UPDATE et INSERT selon l'instance de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ces commandes affectent uniquement les données existantes. Les commandes générées par SQLXML ne modifient jamais la base de données. Les utilisateurs doivent émettre des commandes explicites pour modifier la structure de la base de données, par exemple en les incluant dans un bloc `sql:query` d'un modèle.  
  
-   Lors de l'exécution de codes de différence (diffgrams), SQLXML les traduit en commandes DELETE, UPDATE et INSERT par rapport à l'instance de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ces commandes affectent uniquement les données existantes. Les commandes générées par SQLXML ne modifient jamais la base de données. Les utilisateurs doivent émettre des commandes explicites pour modifier la structure de la base de données, par exemple en les incluant dans un bloc `sql:query` d'un modèle.  
  
## <a name="see-also"></a>Voir aussi  
 [Considérations relatives à la sécurité SQLXML 4.0](sqlxml-4-0-security-considerations.md)  
  
  
