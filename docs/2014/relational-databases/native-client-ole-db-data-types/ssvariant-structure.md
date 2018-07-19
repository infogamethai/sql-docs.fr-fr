---
title: Structure SSVARIANT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52ea23ff970d094330aaf046f9ebdd843c8b4956
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429038"
---
# <a name="ssvariant-structure"></a>Structure SSVARIANT
  La structure `SSVARIANT`, qui est définie dans sqlncli.h, correspond à une valeur DBTYPE_SQLVARIANT dans le fournisseur OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 `SSVARIANT` est une union de discrimination. Selon la valeur du membre vt, le consommateur peut identifier le membre à lire. les valeurs VT correspondent aux [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] types de données. Par conséquent, la structure `SSVARIANT` peut contenir tout type SQL Server. Pour plus d’informations sur la structure de données pour les types OLE DB standard, consultez [indicateurs de Type](http://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Notes  
 Lorsque DataTypeCompat==80, plusieurs sous-types `SSVARIANT` deviennent des chaînes. Par exemple, les valeurs vt suivantes apparaissent dans `SSVARIANT` en tant que VT_SS_WVARSTRING :  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Lorsque DateTypeCompat == 0, ces types s'affichent sous leur forme native.  
  
 Pour plus d’informations sur SSPROP_INIT_DATATYPECOMPATIBILITY, consultez [Using Connection String Keywords with SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Le fichier sqlncli.h contient des macros d'accès de type Variant qui simplifient l'annulation de la référence des types de membres dans la structure `SSVARIANT`. Un exemple est V_SS_DATETIMEOFFSET, que vous pouvez utiliser comme suit :  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Pour obtenir le jeu complet de macros d'accès pour chaque membre de la structure `SSVARIANT`, consultez le fichier sqlncli.hi.  
  
 Le tableau ci-dessous décrit les membres de la structure `SSVARIANT` :  
  
|Membre|Indicateur de type OLE DB|Type de données OLE DB C|Valeur vt|Commentaires|  
|------------|---------------------------|------------------------|--------------|--------------|  
|VT|SSVARTYPE|||Spécifie le type de valeur contenu dans la structure `SSVARIANT`.|  
|bTinyIntVal|DBTYPE_UI1|`BYTE`|`VT_SS_UI1`|Prend en charge la `tinyint` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.|  
|sShortIntVal|DBTYPE_I2|`SHORT`|`VT_SS_I2`|Prend en charge la `smallint` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.|  
|lIntVal|DBTYPE_I4|`LONG`|`VT_SS_I4`|Prend en charge la `int` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.|  
|llBigIntVal|DBTYPE_I8|`LARGE_INTEGER`|`VT_SS_I8`|Prend en charge la `bigint` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.|  
|fltRealVal|DBTYPE_R4|`float`|`VT_SS_R4`|Prend en charge la `real` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.|  
|dblFloatVal|DBTYPE_R8|`double`|`VT_SS_R8`|Prend en charge la `float` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.|  
|cyMoneyVal|DBTYPE_CY|`LARGE_INTEGER`|**VT_SS_MONEY VT_SS_SMALLMONEY**|Prend en charge la `money` et **smallmoney** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] types de données.|  
|fBitVal|DBTYPE_BOOL|`VARIANT_BOOL`|`VT_SS_BIT`|Prend en charge la `bit` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.|  
|rgbGuidVal|DBTYPE_GUID|`GUID`|`VT_SS_GUID`|Prend en charge la `uniqueidentifier` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.|  
|numNumericVal|DBTYPE_NUMERIC|`DB_NUMERIC`|`VT_SS_NUMERIC`|Prend en charge la `numeric` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.|  
|dDateVal|DBTYPE_DATE|`DBDATE`|`VT_SS_DATE`|Prend en charge la `date` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|`DBTIMESTAMP`|`VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2`|Prend en charge la `smalldatetime`, `datetime`, et `datetime2` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] types de données.|  
|Time2Val|DBTYPE_DBTIME2|`DBTIME2`|`VT_SS_TIME2`|Prend en charge la `time` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.<br /><br /> Inclut les membres suivants :<br /><br /> *tTime2Val* (`DBTIME2`)<br /><br /> *bScale* (`BYTE`) spécifie l’échelle pour *tTime2Val* valeur.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|`DBTIMESTAMP`|`VT_SS_DATETIME2`|Prend en charge la `datetime2` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.<br /><br /> Inclut les membres suivants :<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (`BYTE`) spécifie l’échelle pour *tsDataTimeVal* valeur.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|`DBTIMESTAMPOFFSET`|`VT_SS_DATETIMEOFFSET`|Prend en charge la `datetimeoffset` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type de données.<br /><br /> Inclut les membres suivants :<br /><br /> *tsoDateTimeOffsetVal* (`DBTIMESTAMPOFFSET`)<br /><br /> *bScale* (`BYTE`) spécifie l’échelle pour *tsoDateTimeOffsetVal* valeur.|  
|NCharVal|Aucun indicateur de type OLE DB correspondant.|`struct _NCharVal`|`VT_SS_WVARSTRING,`<br /><br /> `VT_SS_WSTRING`|Prend en charge la `nchar` et **nvarchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] types de données.<br /><br /> Inclut les membres suivants :<br /><br /> *sActualLength* (`SHORT`) spécifie la longueur réelle de la chaîne vers laquelle *pwchNCharVal* points. N'inclut pas le zéro de fin.<br /><br /> *sMaxLength* (`SHORT`) spécifie la longueur maximale de la chaîne vers laquelle *pwchNCharVal* points.<br /><br /> *pwchNCharVal* (`WCHAR` \*) pointeur vers la chaîne.<br /><br /> Membres non utilisés : *rgbReserved*, *dwReserved*, et *pwchReserved*.|  
|CharVal|Aucun indicateur de type OLE DB correspondant.|`struct _CharVal`|`VT_SS_STRING,`<br /><br /> `VT_SS_VARSTRING`|Prend en charge la `char` et **varchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] types de données.<br /><br /> Inclut les membres suivants :<br /><br /> *sActualLength* (`SHORT`) spécifie la longueur réelle de la chaîne vers laquelle *pchCharVal* points. N'inclut pas le zéro de fin.<br /><br /> *sMaxLength* (`SHORT`) spécifie la longueur maximale de la chaîne vers laquelle *pchCharVal* points.<br /><br /> *pchCharVal* (`CHAR` \*) pointeur vers la chaîne.<br /><br /> Membres non utilisés :<br /><br /> *rgbReserved*, *dwReserved*, et *pwchReserved*.|  
|BinaryVal|Aucun indicateur de type OLE DB correspondant.|`struct _BinaryVal`|`VT_SS_VARBINARY,`<br /><br /> `VT_SS_BINARY`|Prend en charge la `binary` et **varbinary** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] types de données.<br /><br /> Inclut les membres suivants :<br /><br /> *sActualLength* (`SHORT`) indique la longueur réelle des données vers lesquelles *prgbBinaryVal* points.<br /><br /> *sMaxLength* (`SHORT`) spécifie la longueur maximale des données vers lesquelles *prgbBinaryVal* points.<br /><br /> *prgbBinaryVal* (`BYTE` \*) pointeur vers les données binaires.<br /><br /> Membre non utilisé : *dwReserved*.|  
|UnknownType|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
  
## <a name="see-also"></a>Voir aussi  
 [Types de données &#40;OLE DB&#41;](data-types-ole-db.md)  
  
  