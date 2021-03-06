---
title: Fonctions constructeur (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- constructor functions [XQuery]
ms.assetid: 98562d0e-d0e0-4f62-b001-90acbac67277
author: rothja
ms.author: jroth
ms.openlocfilehash: 7f64c9ff6664410983d9c3ce7ebdbf07e493ca03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038991"
---
# <a name="constructor-functions-xquery"></a>Fonctions constructeur (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  À partir d'une entrée spécifiée, les fonctions constructeur créent des instances de n'importe quel type atomique XSD intégré ou défini par l'utilisateur.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
TYP($atomicvalue as xdt:anyAtomicType?  
  
) as TYP?  
  
```  
  
## <a name="arguments"></a>Arguments  
 *$strval*  
 Chaîne à convertir.  
  
 *TYP*  
 Tout type XSD intégré.  
  
## <a name="remarks"></a>Notes  
 Les constructeurs sont pris en charge pour les types XSD de base et dérivés. Toutefois, les sous-types de **xs : Duration**, qui inclut **xdt : yearmonthduration et xdt : daytimeduration**, et **xs : QName**, **xs : NMTOKEN**, et **xs : notation** ne sont pas pris en charge. Les types atomiques définis par l'utilisateur présents dans les collections de schémas associées sont également disponibles, sous réserve qu'ils soient directement ou indirectement dérivés des types ci-après.  
  
#### <a name="supported-base-types"></a>Types de base pris en charge  
 Les types de base pris en charge sont les suivants :  
  
-   xs:string  
  
-   xs:boolean  
  
-   xs:decimal  
  
-   xs:float  
  
-   xs:double  
  
-   xs:duration  
  
-   xs:dateTime  
  
-   xs:time  
  
-   xs:date  
  
-   xs:gYearMonth  
  
-   xs:gYear  
  
-   xs:gMonthDay  
  
-   xs:gDay  
  
-   xs:gMonth  
  
-   xs:hexBinary  
  
-   xs:base64Binary  
  
-   xs:anyURI  
  
#### <a name="supported-derived-types"></a>Types dérivés pris en charge  
 Les types dérivés pris en charge sont les suivants :  
  
-   xs:normalizedString  
  
-   xs:token  
  
-   xs:language  
  
-   xs:Name  
  
-   xs:NCName  
  
-   xs:ID  
  
-   xs:IDREF  
  
-   xs:ENTITY  
  
-   xs:integer  
  
-   xs:nonPositiveInteger  
  
-   xs:negativeInteger  
  
-   xs:long  
  
-   xs:int  
  
-   xs:short  
  
-   xs:byte  
  
-   xs:nonNegativeInteger  
  
-   xs:unsignedLong  
  
-   xs:unsignedInt  
  
-   xs:unsignedShort  
  
-   xs:unsignedByte  
  
-   xs:positiveInteger  
  
 En outre, SQL Server prend en charge l'assemblage de constantes pour les appels de fonction de construction des façons suivantes :  
  
-   Si l'argument est un littéral de chaîne, l'expression est évaluée pendant la compilation. Lorsque la valeur ne satisfait pas aux contraintes de type, une erreur statique est déclenchée.  
  
-   Si l'argument est un littéral d'un autre type, l'expression est évaluée pendant la compilation. Lorsque la valeur ne satisfait pas aux contraintes de type, la séquence vide est renvoyée.  
  
## <a name="examples"></a>Exemples  
 Cette rubrique fournit des exemples de XQuery relatifs à des instances XML stockés dans différentes **xml** colonnes de type dans la base de données AdventureWorks.  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>R. Utilisation de la fonction XQuery dateTime() pour extraire les anciennes descriptions de produits  
 Dans cet exemple, un exemple de document XML est attribué au préalable un **xml** variable de type. Ce document contient trois exemples <`ProductDescription`> éléments, chacun d’eux contenant un <`DateCreated`> élément enfant.  
  
 La variable est ensuite interrogée afin que ne soient extraites que les descriptions de produits créées avant une date spécifique. À des fins de comparaison, la requête utilise le **:DateTime()** fonction constructeur à taper les dates.  
  
```  
declare @x xml  
set @x = '<root>  
<ProductDescription ProductID="1" >  
  <DateCreated DateValue="2000-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription  ProductID="2" >  
  <DateCreated DateValue="2001-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription ProductID="3" >  
  <DateCreated DateValue="2002-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
</root>'  
  
select @x.query('  
     for $PD in  /root/ProductDescription  
     where xs:dateTime(data( ($PD/DateCreated/@DateValue)[1] )) < xs:dateTime("2001-01-01T00:00:00Z")  
     return  
        element Product  
       {   
        ( attribute ProductID { data($PD/@ProductID ) },  
        attribute DateCreated { data( ($PD/DateCreated/@DateValue)[1] ) } )  
        }  
 ')  
```  
  
 Notez les points suivants dans la requête précédente :  
  
-   FOR... Structure de boucle WHERE est utilisée pour récupérer le \<ProductDescription > élément répondant à la condition spécifiée dans la clause WHERE.  
  
-   Le **dateTime()** fonction constructeur sert à construire **dateTime** tapez des valeurs afin qu’ils puissent être comparées correctement.  
  
-   La requête construit ensuite le document XML obtenu. Étant donné que vous construisez une séquence d'attributs, des virgules et des parenthèses sont utilisées dans la construction XML.  
  
 Voici le résultat obtenu :  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Construction XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [Fonctions XQuery impliquant le type de données xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
