---
title: Générer des données dans les exemples SQL WideWorldImporters
ms.date: 04/04/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 0f880ea881b53c2600fb1fffdf7da5d16ab8d423
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056285"
---
# <a name="wideworldimporters-data-generation"></a>Génération de données WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Les versions commercialisées des bases de données WideWorldImporters et WideWorldImportersDW ont des données du 1er janvier 2013, jusqu’à la date de génération des bases de données.

Lorsque vous utilisez ces exemples de bases de données, vous souhaiterez peut-être inclure des exemples de données plus récents.

## <a name="data-generation-in-wideworldimporters"></a>Génération de données dans WideWorldImporters

Pour générer des exemples de données jusqu’à la date actuelle :

1. Si vous ne l’avez pas fait, installez une version propre de la base de données WideWorldImporters. Pour obtenir des instructions d’installation, consultez [installation et configuration](wide-world-importers-oltp-install-configure.md).
2. Exécutez l’instruction suivante dans la base de données :

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    Cette instruction ajoute des exemples de données de vente et d’achat à la base de données, jusqu’à la date actuelle. Il affiche la progression de la génération des données par jour. La génération de données peut prendre environ 10 minutes pour chaque année nécessitant des données. En raison d’un facteur aléatoire dans la génération de données, il existe des différences entre les données générées entre les exécutions.

    Pour augmenter ou diminuer la quantité de données générées pour les commandes par jour, modifiez la valeur du paramètre `@AverageNumberOfCustomerOrdersPerDay`. Utilisez les paramètres `@SaturdayPercentageOfNormalWorkDay` et `@SundayPercentageOfNormalWorkDay` pour déterminer le volume des commandes pour les jours du week-end.

## <a name="import-generated-data-in-wideworldimportersdw"></a>Importer des données générées dans WideWorldImportersDW

Pour importer des exemples de données jusqu’à la date actuelle dans la base de données OLAP WideWorldImportersDW :

1. Exécutez la logique de génération de données dans la base de données OLTP WideWorldImporters en suivant les étapes décrites dans la section précédente.
2. Si vous ne l’avez pas encore fait, installez une version propre de la base de données WideWorldImportersDW. Pour obtenir des instructions d’installation, consultez [installation et configuration](wide-world-importers-oltp-install-configure.md).
3. Réamorcez la base de données OLAP en exécutant l’instruction suivante dans la base de données :

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. Exécutez le package *Daily ETL. ispac* SQL Server Integration Services pour importer les données dans la base de données OLAP. Pour savoir comment exécuter le travail ETL, consultez [Workflow ETL wideworldimporters](wide-world-importers-perform-etl.md).

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>Générer des données dans WideWorldImportersDW pour le test des performances

WideWorldImportersDW peut augmenter arbitrairement la taille des données pour les tests de performances. Par exemple, il peut augmenter la taille des données à utiliser avec l’indexation ColumnStore en cluster.

L’une des difficultés consiste à conserver la taille du téléchargement suffisamment petite pour un téléchargement facile, mais suffisamment grand pour présenter les fonctionnalités de performances de SQL Server. Par exemple, les avantages significatifs pour les index ColumnStore sont atteints uniquement lorsque vous travaillez avec un grand nombre de lignes. 

Vous pouvez utiliser la procédure `Application.Configuration_PopulateLargeSaleTable` pour augmenter le nombre de lignes dans la table `Fact.Sale`. Les lignes sont insérées dans l’année civile 2012 afin d’éviter toute collision avec les données des importateurs mondiaux existantes qui commencent le 1er janvier 2013.

### <a name="procedure-details"></a>Détails de la procédure

#### <a name="name"></a>Nom

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Paramètres

  `@EstimatedRowsFor2012` **bigint** (avec 12 millions comme valeur par défaut)

#### <a name="result"></a>Résultat

Approximativement, le nombre requis de lignes est inséré dans la table `Fact.Sale` de l’année 2012. La procédure limite artificiellement le nombre de lignes à 50 000 par jour. Vous pouvez modifier cette limitation, mais la limitation vous aide à éviter les surinflations accidentelles de la table.

La procédure applique également l’indexation ColumnStore en cluster si elle n’a pas déjà été appliquée.
