---
title: Informations de référence sur les fichiers d’entrée XML (Assistant Paramétrage du moteur de base de données) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0572c0aa0b4a49a3c0ce471cb8194124fef73cdb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105784"
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>Référence des fichiers d'entrée XML (Assistant Paramétrage du moteur de base de données)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] L’Assistant Paramétrage peut utiliser un fichier d’entrée XML pour paramétrer une base de données. Ce fichier XML désigne les bases de données, les tables, les fichiers ou tables de charge de travail et les options de paramétrage à utiliser pendant la session de paramétrage. Vous pouvez également utiliser ce fichier pour indiquer une configuration spécifiée par l'utilisateur afin d'effectuer une évaluation de simulation.  
  
 Un fichier d’entrée XML de l’Assistant Paramétrage du [!INCLUDE[ssDE](../../includes/ssde-md.md)] contient une hiérarchie d’éléments XML, chaque élément XML comprenant le texte ou d’autres éléments qui spécifient les paramètres de la session de paramétrage. Le fichier d’entrée XML de l’Assistant Paramétrage du [!INCLUDE[ssDE](../../includes/ssde-md.md)] doit être conforme aux normes pour le XML correctement formé. Tous les éléments respectent la casse. Les éléments sont spécifiés à l'aide de la casse Pascal, ce qui signifie que le premier caractère est en majuscules, tout comme la première lettre des mots concaténés suivants.  
  
 Toutes les valeurs d'éléments doivent respecter les conventions d'affectation de noms XML. Pour plus d’informations sur ces conventions, consultez [XML Textual Content](https://go.microsoft.com/fwlink/?LinkId=7614) (Contenu textuel XML) dans la bibliothèque MSDN.  
  
 Notez que ce Guide de référence n'est pas complet. Pour plus d'informations sur tous les éléments que vous pouvez utiliser pour définir une entrée XML, reportez-vous au schéma DTASchema.xsd de l'Assistant Paramétrage du [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="xml-declaration"></a>Déclaration XML  
  
-   [Données XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>Élément racine DTAXML  
  
-   [DTAXML, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>Éléments DTAInput  
  
-   [DTAInput, élément &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)  
  
-   [Server, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/server-element-dta.md)  
  
-   [Workload, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/workload-element-dta.md)  
  
-   [TuningOptions, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
-   [Configuration, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/configuration-element-dta.md)  
  
## <a name="server-elements"></a>Éléments de serveur  
  
-   [Name, élément pour les serveurs &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/name-element-for-server-dta.md)  
  
-   [Database, élément pour les serveurs &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>Éléments de charge de travail  
  
-   [File, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/file-element-dta.md)  
  
-   [Élément Database &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/database-element-for-workload-dta.md)  
  
-   [EventString, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>Éléments d'options de paramétrage  
  
-   [TuningTimeInMin, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/tuningtimeinmin-element-dta.md)  
  
-   [StorageBoundInMB, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/storageboundinmb-element-dta.md)  
  
-   [TestServer, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/testserver-element-dta.md)  
  
-   [FeatureSet, élément &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partitioning, élément &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [DropOnlyMode, élément &#40;DTA&#41;](../../tools/dta/droponlymode-element-dta.md)  
  
-   [KeepExisting, élément &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md)  
  
-   [OnlineIndexOperation, élément &#40;DTA&#41;](../../tools/dta/onlineindexoperation-element-dta.md)  
  
-   [DatabaseToConnect, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>Éléments de configuration  
  
-   [Server, élément pour les configurations &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/server-element-for-configuration-dta.md)  
  
-   [Database, élément pour les configurations &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/database-element-for-configuration-dta.md)  
  
-   [Recommendation, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/recommendation-element-dta.md)  
  
-   [Create, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/create-element-dta.md)  
  
-   [Index, élément &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/index-element-dta.md)  
  
-   [Name, élément pour les index &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/name-element-for-index-dta.md)  
  
-   [Column, élément pour les index &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/column-element-for-index-dta.md)  
  
-   [Name, élément pour les colonnes &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/name-element-for-column-dta.md)  
  
-   [Filegroup, élément pour les index &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>Éléments de base de données  
  
-   [Name, élément pour les bases de données &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/name-element-for-database-dta.md)  
  
-   [Schema, élément pour les bases de données &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/schema-element-for-database-dta.md)  
  
-   [Name, élément pour les schémas &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/name-element-for-schema-dta.md)  
  
-   [Table, élément pour les schémas &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/table-element-for-schema-dta.md)  
  
-   [Name, élément pour les tables &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/name-element-for-table-dta.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
