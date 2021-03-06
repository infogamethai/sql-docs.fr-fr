---
title: En cours d’exécution du Script SQL carnet d’adresse | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5adc631a3c3f7a66c02f9ebfe541fa5e923deb0a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922239"
---
# <a name="running-the-address-book-sql-script"></a>Exécution du script SQL Carnet d’adresses
> [!IMPORTANT]
>  Depuis Windows 8 et Windows Server 2012, composants de serveur Services Bureau à distance ne sont plus inclus dans le système d’exploitation Windows (voir Windows 8 et [Guide de compatibilité de Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) pour plus de détails). Composants du client RDS seront supprimées dans une future version de Windows. Évitez d'utiliser cette fonctionnalité dans de nouveaux travaux de développement, et prévoyez de modifier les applications qui utilisent actuellement cette fonctionnalité. Les applications qui utilisent des services Bureau à distance doivent migrer vers [Service de données WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Vous devez utiliser l’utilitaire de ligne de commande ISQL/Query Analyzer ou SQL Server Enterprise Manager pour exécuter le script SQL inclus (Sampleemp.sql) qui :  
  
-   Crée une base de données, AddrBookDB, sur l’appareil par défaut.  
  
-   Se connecte à la base de données AddrBookDB.  
  
-   Crée une table d’employés.  
  
-   Remplit la table avec les exemples de données.  
  
-   Exécute une instruction SELECT simple pour vérifier le remplissage de la table de base de données.  
  
-   Configure un compte d’utilisateur appelé « adcdemo » avec un mot de passe de « adcdemo ».  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Pour exécuter le script Sampleemp.sql dans Microsoft SQL Server 6.5  
  
1.  Cliquez sur **Démarrer**, pointez sur **programmes**, puis pointez sur **Microsoft SQL Server 6.5**. Cliquez sur **SQL Enterprise Manager**.  
  
2.  À partir de la **outils** menu, cliquez sur **outil de requête SQL**.  
  
3.  Cliquez sur **charger un Script SQL** et accédez à c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
4.  Sélectionnez le fichier Sampleemp.sql. Cliquez sur **Ouvrir**.  
  
5.  Cliquez sur le **exécuter la requête** bouton (la flèche verte dans la barre d’outils).  
  
6.  Une fois qu’il s’exécute, fermez le **requête** et **Enterprise Manager** windows.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Pour exécuter le script Sampleemp.sql dans Microsoft SQL Server 7.0  
  
1.  Cliquez sur **Démarrer**, pointez sur **programmes**, puis pointez sur **Microsoft SQL Server 7.0**. Cliquez sur **Enterprise Manager**.  
  
2.  N’oubliez pas que le serveur SQL Server que vous souhaitez utiliser est sélectionné dans la liste des serveurs inscrits dans Enterprise Manager.  
  
3.  À partir de la **outils** menu, cliquez sur **Analyseur de requêtes SQL Server**.  
  
4.  Cliquez sur le **charger un Script SQL** bouton (le dossier ouvert sur la barre d’outils) et accédez à c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
5.  Sélectionnez le fichier Sampleemp.sql. Cliquez sur **Ouvrir**.  
  
6.  Cliquez sur le **exécuter la requête** bouton (la flèche verte dans la barre d’outils) ou **F5**.  
  
7.  Une fois qu’il s’exécute, fermez le **requête**, **Analyseur de requêtes**, et **Enterprise Manager** windows.  
  
## <a name="see-also"></a>Voir aussi  
 [Exécution de l’exemple d’application Carnet d’adresses](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


