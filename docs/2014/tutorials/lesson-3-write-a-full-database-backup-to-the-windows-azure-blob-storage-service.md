---
title: 'Leçon 3 : Écrire une sauvegarde de base de données complète dans le service de stockage d’objets BLOB Azure | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 454c8296-64e9-46ed-b141-5ebfbc8a4fe2
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 1d5a749c61a3bc97de841e1149dd1539cbc990f2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153475"
---
# <a name="lesson-3-write-a-full-database-backup-to-the-azure-blob-storage-service"></a>Leçon 3 : Écrire une sauvegarde de base de données complète dans le service de stockage d’objets BLOB Azure
  Cette leçon illustre l’utilisation de l’instruction TSQL pour effectuer une sauvegarde de base de données complète dans le service de stockage d’objets BLOB Azure.  
  
## <a name="perform-a-full-database-backup-to-the-azure-blob-storage-service"></a>Effectuer une sauvegarde de base de données complète dans le service de stockage d’objets BLOB Azure  
 Pour créer une sauvegarde de base de données complète, procédez comme suit :  
  
1.  Se connecter à [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Dans l' **Explorateur d'objets**, connectez-vous à l'instance de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
3.  Dans la barre de menus standard, cliquez sur **Nouvelle requête**.  
  
4.  Copiez et collez l'exemple suivant dans la fenêtre de requête, modifiez-le si nécessaire, puis cliquez sur **Exécuter**.  
  
    ```  
    BACKUP DATABASE[AdventureWorks2012]   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/   
    WITH CREDENTIAL = 'mycredential';  
    /* name of the credential you created in the previous step */   
    GO  
  
    ```  
  
5.  Dans l'Explorateur d'objets, connectez-vous au stockage Azure. Recherchez le conteneur et les fichiers de sauvegarde récemment créés.  
  
## <a name="next-lesson"></a>Leçon suivante  
 [Leçon 4 : Effectuez une restauration à partir d’une sauvegarde](../../2014/tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)complète de base de données.  
  
  
