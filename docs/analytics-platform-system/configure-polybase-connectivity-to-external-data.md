---
title: Configurer la connectivité Polybase
description: Explique comment configurer Polybase en parallèle Data Warehouse pour se connecter à des sources de données d’objet blob de stockage Hadoop ou Microsoft Azure externe. Utilisez Polybase pour exécuter des requêtes qui intègrent des données provenant de plusieurs sources, notamment Hadoop, le stockage d’objets BLOB Azure et les Data Warehouse parallèles.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3b754fb2de33a230bc7d27f239b2778d2849fd5a
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401276"
---
# <a name="what-is-polybase"></a>Qu’est-ce que PolyBase ?
Polybase permet à votre système de plateforme d’analyse (APS) de traiter des requêtes Transact-SQL qui peuvent lire et écrire des données dans des sources de données externes. Les mêmes requêtes qui accèdent à des données externes peuvent également inclure des tables de relation dans vos APS. Cela vous permet de combiner des données provenant de sources externes à des données relationnelles de valeur élevée dans vos bases de données APS.

![Logique Polybase](media/polybase/polybase-logical.png)

Polybase sur APS prend en charge la lecture et l’écriture dans le système de fichiers Hadoop (HDFS) et le stockage d’objets BLOB Azure. Polybase a également la possibilité de pousser certains calculs vers des nœuds Hadoop en tant que tâches MapReduce pour optimiser les performances globales des requêtes. Polybase sur APS peut fonctionner sur des fichiers texte délimités, ORC et parquet. Pour une description complète et ses fonctionnalités, voir [qu’est-ce que Polybase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) .

> [!NOTE]
> Actuellement, les APS prennent uniquement en charge le stockage d’objets BLOB Azure à usage général v1 localement redondant (LRS).

## <a name="features-and-limitations"></a>Fonctionnalités et limitations
Consultez [fonctionnalités et](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary) limitations pour obtenir un résumé des fonctionnalités Polybase disponibles et des limitations connues sur les points d’accès et autres produits SQL Server.

> [!NOTE] 
> Le reste des Articles liés à Polybase décrivent comment configurer Polybase sur APS 2016 (AU6) et versions ultérieures.

## <a name="see-also"></a>Voir aussi
- [Hadoop](polybase-configure-hadoop.md)
- [Stockage d’objets BLOB Azure](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
