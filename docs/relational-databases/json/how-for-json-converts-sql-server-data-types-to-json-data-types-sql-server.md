---
title: Conversion par FOR JSON des types de données SQL Server en types de données JSON
ms.date: 07/07/2016
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 537ad4d796792c7d4fce56eda25adcca8b1fea01
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74095798"
---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>Conversion par FOR JSON des types de données SQL Server en types de données JSON (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  La clause **FOR JSON** utilise les règles ci-après pour convertir les types de données SQL Server en types JSON dans la sortie JSON.  
  
|Category|Type de données SQL Server|Type de données JSON|  
|--------------|--------------|---------------|  
|Types caractères et chaînes|char, nchar, varchar, nvarchar|string|  
|Types valeurs numériques|int, bigint, float, decimal, numeric|nombre|  
|Types bits|bit|Booléen (true ou false)|  
|Types dates et heures|date, datetime, datetime2, time, datetimeoffset|string|  
|Types données binaires|varbinary, binary, image, timestamp, rowversion|Chaîne codée en Base64|  
|Types CLR|geometry, geography, autres types CLR|Non pris en charge. Ces types renvoient une erreur.<br /><br /> Dans l’instruction SELECT, utilisez CAST ou CONVERT, ou bien une propriété ou méthode CLR, pour convertir les données sources en type de données SQL Server pouvant être converti correctement en type JSON. Par exemple, utilisez **STAsText()** pour le type geometry, ou **ToString()** pour un type CLR. Le type de la valeur de sortie JSON est ensuite dérivé du type de retour de la conversion que vous appliquez dans l’instruction SELECT.|  
|Autres types|uniqueidentifier, money|string|  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>En savoir plus sur JSON dans SQL Server et Azure SQL Database  
  
### <a name="microsoft-videos"></a>Vidéos Microsoft

Pour obtenir une présentation visuelle de la prise en charge intégrée de JSON dans SQL Server et Azure SQL Database, consultez les vidéos suivantes :

-   [SQL Server 2016 et prise en charge de JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Utilisation de JSON dans SQL Server 2016 et Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON : un pont entre les mondes relationnel et NoSQL](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Voir aussi  
 [Mettre les résultats de requête au format JSON avec FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
