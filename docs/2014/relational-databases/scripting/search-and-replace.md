---
title: Recherche et remplacement
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- match case [SQL Server]
- undo operations
- searches [SQL Server Management Studio]
- replacing text
- quick search and replaces [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], undo
- Query Editor [SQL Server Management Studio], searching
- regular expressions [SQL Server Management Studio]
- finding text [SQL Server Management Studio]
- text [SQL Server], search and replace operations
- finding [SQL Server Management Studio]
- locating text
- Query Editor [SQL Server Management Studio], replacing text
- Find and Replace dialog box
- wildcard options [SQL Server Management Studio]
- match whole word [SQL Server]
- searches [SQL Server Management Studio], replacing
ms.assetid: 3641c7b3-3e3e-4ddd-af82-c15b50004f94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 631b6864529e903516857f68ea421365c144afef
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243301"
---
# <a name="search-and-replace"></a>Recherche et remplacement
  Il existe plusieurs méthodes différentes pour rechercher et remplacer du texte. Dans le menu **Edition** , la commande **Rechercher et remplacer** propose quatre options : **Recherche rapide**, **Remplacement rapide**, **Rechercher dans les fichiers**ou **Remplacer dans les fichiers**. Chaque option ouvre une version de la boîte de dialogue **Rechercher et remplacer** . Vous pouvez également effectuer une recherche sans l'aide de l'une de ces boîtes de dialogue. Pour ce faire, il vous suffit d'utiliser les touches de raccourci clavier de la recherche incrémentielle. Ces techniques vous permettent de contrôler la portée de l'opération de recherche et de remplacement et de choisir la méthode de révision des occurrences trouvées et des remplacements.  
  
 Tenez compte des informations suivantes lorsque vous recherchez et remplacez du texte :  
  
-   Les options définies dans la boîte de dialogue **Rechercher et remplacer** affectent toutes les recherches. Ces options comprennent **Respecter la casse**, **Mot entier**, **Rechercher vers le haut**, **Rechercher le texte masqué**, **Caractères génériques**, **Expressions régulières**, **Regarder dans tous les documents ouverts**et **Regarder dans le projet en cours**. Les options ne sont pas toutes disponibles dans toutes les versions de la boîte de dialogue **Rechercher et remplacer** .  
  
-   La **commande Annuler** est disponible uniquement pour les documents restés ouverts après une opération de remplacement.  
  
-   **Undo** pour une opération **remplacer tout** qui s’étend sur plusieurs fichiers est considérée comme une action en bloc unique dans tous les fichiers affectés. Par conséquent, vous ne pouvez pas annuler des modifications dans certains fichiers et les conserver dans d'autres.  
  
 En règle générale, vous ne pouvez pas rechercher des éléments avec des vues graphiques.  
  
## <a name="see-also"></a>Voir aussi  
 [Effectuer une recherche incrémentielle dans un document actif](search-an-active-document-incrementally.md)   
 [Rechercher des documents de manière interactive](search-documents-interactively.md)   
 [Rechercher des documents à l’aide des listes de résultats](search-documents-using-results-lists.md)   
 [Rechercher du texte avec des caractères génériques](search-text-with-wildcards.md)   
 [Rechercher du texte avec des expressions régulières](search-text-with-regular-expressions.md)  
  
  
