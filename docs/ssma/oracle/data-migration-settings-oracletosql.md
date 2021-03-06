---
title: Paramètres de Migration de données (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 2b435b02060d32e61bc3e75054171023262a87b8
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264214"
---
# <a name="data-migration-settings-oracletosql"></a>Paramètres de migration de données (OracleToSQL)
  
## <a name="data-migration-settings"></a>Paramètres de migration de données  
**Paramètres de Migration de données** permet à l’utilisateur d’écrire des requêtes personnalisées pour la migration de données.  
  
-   Cet onglet est disponible lorsque **étendu d’options de migration de données** a la valeur **afficher** et est masqué lorsque le paramètre est défini sur **masquer** dans Paramètres du projet. Pour plus d’informations sur les paramètres de Migration de projet, consultez [paramètres du projet (Migration)](https://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60) .  
  
-   L’analyse des instructions SQL de personnalisé sera implémenté dans **les paramètres de migration de données** onglet du nœud de la Table.  
  
-   Voici les deux cases à cocher disponibles dans le **les paramètres de Migration de données** reportages. :  
  
    1.  TRUNCATE table SQL Server  
  
    2.  Sélectionnez utilisation personnalisée  
  
1.  **TRUNCATE table SQL Server :**  
     Cette option permet à l’utilisateur d’avoir une vue claire des données migrées à la base de données cible.  
  
    -   Par défaut, cette zone de texte est activée.  
  
    -   Si cette zone de texte est désactivée, puis les données qui sont migrées figurera sur les données existantes à la base de données cible.  
  
2.  **Utilisation personnalisée sélectionnez :**  
     Cette option permet à l’utilisateur de modifier le **sélectionnez** instruction présente (**sélectionnez** instruction permet aux utilisateurs de sélectionner les données à afficher à la base de données cible).  
  
    1.  Par défaut, cette zone de texte est désactivée.  
  
    2.  Si cette zone de texte est activée, elle permet aux utilisateurs de modifier le **sélectionnez** instruction présents.  
  
Il existe deux boutons présents reportages. :  
  
-   **S’appliquent :** Cliquez sur **appliquer** pour appliquer les paramètres qui ont été modifiés.  
  
-   **Annuler :** Cliquez sur **Annuler** pour restaurer les paramètres présents avant que les modifications sont apportées.  
  
## <a name="see-also"></a>Voir aussi  
[Migration de données Oracle vers SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)  
  
