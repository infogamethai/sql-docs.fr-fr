---
title: Se connecter à Stockage Microsoft Azure (Restauration) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 94860f25b8cb53ab3c273da2e020d0d6a506ad0b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70155618"
---
# <a name="connect-to-microsoft-azure-storage-restore"></a>Se connecter à Stockage Microsoft Azure (Restauration)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La boîte de dialogue vous permet de spécifier les informations de connexion au compte de stockage Azure pour récupérer les fichiers qui y sont stockés. Après avoir spécifié les informations requises, cliquez sur **Connexion** pour établir la connexion au stockage Azure.  
  
## <a name="azure-storage-account"></a>Compte Stockage Azure  
 **Compte de stockage**  
 Sélectionnez, entrez ou collez le nom du compte de stockage Azure que vous souhaitez utiliser. La liste déroulante répertorie les comptes utilisés précédemment.  
  
 **Clé de compte**  
 Spécifiez la clé d’accès du compte de stockage Azure.  
  
 Case à cocher**Utiliser des points de terminaisons sécurisés (HTTPS)**  
 Sélectionnez cette option pour établir une connexion sécurisée au stockage Azure (recommandé).  
  
 Case à cocher**Enregistrer la clé de compte**  
 Cochez cette case si vous souhaitez que SQL Server se souvienne de la clé d'accès de ce compte de stockage.  
  
### <a name="sql-credential"></a>Informations d'identification SQL  
 **Sélectionner des informations d'identification existantes**  
 Sélectionnez des informations d'identification SQL existantes correspondant au compte de stockage et à la clé d'accès.  
  
 **Créer de nouvelles informations d'identification**  
 Sélectionnez cette option pour créer de nouvelles informations d'identification en utilisant les informations du compte de stockage et de la clé d'accès. Spécifiez le nom des nouvelles informations d'identification dans le champ **Nom d'identification** .  
  
  
