---
title: Types de données d’instance Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eec13d8d-c15a-4542-bfc4-da66b1a6bfe0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d72ece429ae04e8cb6ee3af3acd872fa751d3a57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62835451"
---
# <a name="oracle-cdc-instance-data-types"></a>Types de données d'instance Oracle CDC
  L'instance Oracle CDC prend en charge la plupart des types de données Oracle. Les sections suivantes décrivent les types de données pris en charge et les types de données non pris en charge.  
  
## <a name="supported-data-types"></a>Types de données pris en charge  
 Le tableau suivant décrit les types de données Oracle qui peuvent être capturés et leur mappage par défaut aux types de données SQL Server dans les tables de modifications. Lorsque vous ajoutez une instance de capture pour une table Oracle source, vous pouvez remplacer certains de ces mappages.  
  
|Type de données de base de données Oracle|Type de données de SQL Server|  
|-------------------------------|--------------------------|  
|BINARY_FLOAT|real|  
|BINARY_DOUBLE|FLOAT|  
|CHAR|NVARCHAR|  
|DATE|DATETIME|  
|FLOAT|FLOAT|  
|INT|NUMERIC (38)|  
|INTERVAL|DATETIME|  
|NCHAR|NVARCHAR|  
|NUMBER|FLOAT|  
|NAVARCHAR2|NVARCHAR|  
|RAW|VARBINARY|  
|real|FLOAT|  
|TIMESTAMP|DATETIME2|  
|TIMESTAMP WITH TIME ZONE|VARCHAR (37)|  
|TIMESTAMP WITH LOCAL TIME ZONE|VARCHAR (37)|  
|VARCHAR2|VARCHAR|  
|XMLTYPE|NVARCHAR (MAX)|  
  
## <a name="non-supported-data-types"></a>Types de données non pris en charge  
 Les tables Oracle sources avec des colonnes de types de données Oracle suivants ne peuvent pas être capturées. Les colonnes capturées avec ces types de données s'affichent en tant que colonnes NULL ; toutefois, une modification de leur valeur est indiquée dans le masque de modification des tables capturées.  
  
-   LONG  
  
-   XMLTYPE  
  
-   BLOB  
  
-   CLOB  
  
 Les tables Oracle sources avec des colonnes de types de données Oracle suivants ne peuvent pas être capturées.  
  
-   BFILE  
  
-   ROWID  
  
-   REF  
  
-   UROWID  
  
-   Table imbriquée  
  
 Si les types de données suivants sont présents dans une table, ils empêchent le LogMinder d'obtenir les données de colonne de la table :  
  
-   Types de données définis par l'utilisateur  
  
-   VARRAY  
  
## <a name="see-also"></a>Voir aussi  
 [Concepteur de capture de données modifiées pour Oracle par Attunity](change-data-capture-designer-for-oracle-by-attunity.md)   
 [Instance Oracle CDC](the-oracle-cdc-instance.md)  
  
  
