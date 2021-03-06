---
title: Types de données SQL Server et SSIS pris en charge pour les domaines DQS
description: Décrit les quatre types de données pour les domaines Data Quality Services (DQS) (données, Decimal, Integer et String) dans SQL Server.
ms.custom: seo-lt-2019
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
author: swinarko
ms.author: sawinark
ms.openlocfilehash: cff5cf3a2a6095b79537571d63ee428c500789c6
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558165"
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>Types de données SQL Server et SSIS pris en charge pour les domaines DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Il existe de nombreux types de données dans SQL Server et SQL Server Integration Services (SSIS), mais seulement quatre types de données pour les domaines DQS : Date, Décimal, Entier et Chaîne. Les types de données SQL Server et SSIS ne sont pas tous pris en charge dans DQS. Vous ne pouvez mapper vos données source à un domaine DQS en vue d'y effectuer des activités portant sur la qualité des données que si le type de données source est pris en charge dans DQS et qu'il correspond au type de données du domaine DQS. Cette rubrique fournit des informations relatives aux types de données SQL Server et SSIS qui sont pris en charge et disponibles en vue d'un mappage à chacun des quatre types de données de domaine dans DQS.  
  
> [!NOTE]  
>  Dans les fichiers .xlsx et .xls, le type de données de la colonne source est déterminé par le type de données prédominant des huit premières lignes. Si une cellule n'est pas conforme à ce type de données, elle recevra une valeur NULL. De la même manière, dans les fichiers .csv, le type de données de la colonne source est déterminé par le type de données prédominant des huit premières lignes.  
  
##  <a name="SQLServer"></a>Types de données SQL Server pris en charge 
 Le tableau suivant fournit des informations sur les types de données SQL Server pris en charge pour chaque type de données de domaine DQS :  
  
|Type de données de domaine DQS|Type de données SQL Server pris en charge|  
|--------------------------|------------------------------------|  
|Date|date|  
|Décimal|décimal<br /><br /> float<br /><br /> money<br /><br /> numeric<br /><br /> real<br /><br /> smallmoney|  
|Integer|bigint<br /><br /> int<br /><br /> smallint<br /><br /> tinyint|  
|String|char<br /><br /> nchar<br /><br /> nvarchar<br /><br /> varchar|  
  
 Les autres types de données SQL Server ne sont pas pris en charge dans DQS. Pour plus d’informations sur les types de données SQL Server, consultez [Types de données &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
##  <a name="SSIS"></a>Types de données SSIS pris en charge  
 Le tableau suivant fournit des informations sur les types de données SSIS pris en charge pour chaque type de données de domaine DQS :  
  
|Type de données de domaine DQS|Type de données SSIS pris en charge|  
|--------------------------|------------------------------|  
|Date|DT_DATE|  
|Décimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Integer|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|String|DT_STR<br /><br /> DT_WSTR|  
  
 Les autres types de données SSIS ne sont pas pris en charge dans DQS Pour plus d'informations sur tous les types de données SSIS, consultez [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Gestion d'un domaine](../data-quality-services/managing-a-domain.md)  
  
  
