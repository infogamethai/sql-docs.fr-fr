---
title: Mappage de type de données dans ITableDefinition | Microsoft Docs
description: Mappage de types de données dans ITableDefinition
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- OLE DB Driver for SQL Server, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
author: pmasl
ms.author: pelopes
ms.openlocfilehash: abe874a50e8534291a67393dfaf3485c96405b02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015852"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mappage de type de données dans ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Lors de la création de tables avec la fonction **ITableDefinition::CreateTable**, le consommateur du pilote OLE DB pour SQL Server peut spécifier des types de données [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dans le membre *pwszTypeName* du tableau DBCOLUMNDESC qui est passé. Si le consommateur spécifie le type de données d’une colonne par nom, le mappage des types de données OLE DB, représenté par le membre *wType* de la structure DBCOLUMNDESC, est ignoré.  
  
 Lors de la spécification de nouveaux types de données de colonne avec des types de données OLE DB avec le membre *wType* de la structure DBCOLUMNDESC, le pilote OLE DB pour SQL Server mappe les types de données OLE DB comme suit.  
  
|Type de données OLE DB|SQL Server<br /><br /> type de données|Autres informations|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image** ou **varbinary(max)**|Le pilote OLE DB pour SQL Server inspecte le membre *ulColumnSize* de la structure DBCOLUMNDESC. En fonction de la valeur et de la version [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de l’instance, le pilote OLE DB pour SQL Server mappe le type à **image**.<br /><br /> Si la valeur de *ulColumnSize* est inférieure à la longueur maximale d’une colonne de type de données **binary**, le pilote OLE DB pour SQL Server inspecte le membre *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH est VARIANT_TRUE, le pilote OLE DB pour SQL Server mappe le type à **Binary**. Si la valeur de la propriété est VARIANT_FALSE, le pilote OLE DB pour SQL Server mappe le type à **varbinary**. Dans les deux cas, le membre *ulColumnSize* de DBCOLUMNDESC détermine la largeur de la colonne SQL Server créée.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**Int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|Le pilote OLE DB pour SQL Server inspecte les membres *bPrecision* et *bScale* de DBCOLUMDESC pour déterminer la précision et l’échelle pour la colonne **numeric**.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text** ou **varchar(max)**|Le pilote OLE DB pour SQL Server inspecte le membre *ulColumnSize* de la structure DBCOLUMNDESC. En fonction de la valeur et de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] version de l’instance, le pilote OLE DB pour SQL Server mappe le type à du **texte**.<br /><br /> Si la valeur de *ulColumnSize* est inférieure à la longueur maximale d’une colonne avec un type de données de caractères multi-octets, le pilote OLE DB pour SQL Server inspecte le membre *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH a la valeur VARIANT_TRUE, le pilote OLE DB pour SQL Server mappe le type à **char**. Si la valeur de la propriété est VARIANT_FALSE, le pilote OLE DB pour SQL Server mappe le type à **varchar**. Dans les deux cas, le membre *ulColumnSize* de DBCOLUMNDESC détermine la largeur de la colonne [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] créée.|  
|DBTYPE_UDT|**UDT**|Les informations suivantes sont utilisées dans les structures **DBCOLUMNDESC** par **ITableDefinition::CreateTable** quand des colonnes UDT sont nécessaires :<br /><br /> *pwSzTypeName* est ignoré.<br /><br /> *rgPropertySets* doit inclure un jeu de propriétés **DBPROPSET_SQLSERVERCOLUMN** comme décrit dans la section sur **DBPROPSET_SQLSERVERCOLUMN**, dans [utilisation de types définis par l’utilisateur](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** ou **nvarchar(max)**|Le pilote OLE DB pour SQL Server inspecte le membre *ulColumnSize* de la structure DBCOLUMNDESC. En fonction de la valeur, le pilote OLE DB pour SQL Server mappe le type à **ntext**.<br /><br /> Si la valeur de *ulColumnSize* est inférieure à la longueur maximale d’une colonne avec un type de données de caractères Unicode, le pilote OLE DB pour SQL Server inspecte le membre *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH est VARIANT_TRUE, le pilote OLE DB pour SQL Server mappe le type à **nchar**. Si la valeur de la propriété est VARIANT_FALSE, le pilote OLE DB pour SQL Server mappe le type à **nvarchar**. Dans les deux cas, le membre *ulColumnSize* de DBCOLUMNDESC détermine la largeur de la colonne [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] créée.|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  Lors de la création d’une table, le pilote OLE DB pour SQL Server mappe seulement les valeurs d’énumération des types de données OLE DB spécifiées dans le tableau précédent. Toute tentative de création d'une table avec une colonne de tout autre type de données OLE DB génère une erreur.  

## <a name="see-also"></a>Voir aussi  
 [Types &#40;de données OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
