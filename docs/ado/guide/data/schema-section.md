---
title: Section de schéma | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b6e591ecc9f366f3914986b0ae11e0e301b782d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924293"
---
# <a name="schema-section"></a>Section de schéma
La section de schéma est requise. Comme le montre l’exemple précédent, ADO écrit des métadonnées détaillées concernant chaque colonne pour préserver la sémantique des valeurs de données autant que possible pour la mise à jour. Toutefois, pour charger le code XML, ADO requiert uniquement les noms des colonnes et l’ensemble de lignes auquel elles appartiennent. Voici un exemple de schéma minimal :  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"  
    xmlns:rs="urn:schemas-microsoft-com:rowset"  
    xmlns:z="#RowsetSchema">  
  <s:Schema id="RowsetSchema">  
    <s:ElementType name="row" content="eltOnly">  
      <s:AttributeType name="ShipperID"/>  
      <s:AttributeType name="CompanyName"/>  
      <s:AttributeType name="Phone"/>  
      <s:Extends type="rs:rowbase"/>  
    </s:ElementType>  
  </s:Schema>  
  <rs:data>  
...  
  </rs:data>  
</xml>  
```  
  
 Dans l’exemple précédent, ADO traite les données sous forme de chaînes de longueur variable, car aucune information de type n’est incluse dans le schéma.  
  
## <a name="creating-aliases-for-column-names"></a>Création d’alias pour les noms de colonnes  
 L’attribut rs : name vous permet de créer un alias pour un nom de colonne afin qu’un nom convivial peut apparaître dans les informations de colonne exposées par l’ensemble de lignes et un nom plus court peut être utilisé dans la section de données. Par exemple, le schéma précédent peut être modifié pour les mapper n° messager s1, CompanyName et s2, Phone et s3 comme suit :  
  
```  
<s:Schema id="RowsetSchema">   
<s:ElementType name="row" content="eltOnly" rs:updatable="true">   
<s:AttributeType name="s1" rs:name="ShipperID" rs:number="1" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s2" rs:name="CompanyName" rs:number="2" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s3" rs:name="Phone" rs:number="3" ...>   
...  
</s:AttributeType>   
...  
</s:ElementType>   
</s:Schema>  
```  
  
 Puis, dans la section de données, la ligne utilise l’attribut de nom (non rs : name) pour faire référence à cette colonne :  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 Création d’alias pour les noms de colonnes est nécessaire chaque fois qu’un nom de colonne n’est pas un attribut valide ou le nom de balise dans XML. Par exemple, « LastName » doit avoir un alias car les noms avec des espaces incorporés sont des attributs non valides. La ligne suivante ne sera pas correctement traitée par l’analyseur XML, vous devez donc créer un alias à un autre nom qui n’a pas un espace incorporé.  
  
```  
<row last name="Jones"/>  
```  
  
 La valeur utilisée pour l’attribut name doit être utilisée régulièrement chaque fois que la colonne est référencée dans le schéma et les données des sections du document XML. L’exemple suivant illustre l’utilisation cohérente de s1 :  
  
```  
<s:Schema id="RowsetSchema">  
  <s:ElementType name="row" content="eltOnly">  
    <s:attribute type="s1"/>  
    <s:attribute type="CompanyName"/>  
    <s:attribute type="s3"/>  
    <s:extends type="rs:rowbase"/>  
  </s:ElementType>  
  <s:AttributeType name="s1" rs:name="ShipperID" rs:number="1"   
    rs:maydefer="true" rs:writeunknown="true">  
    <s:datatype dt:type="i4" dt:maxLength="4" rs:precision="10"   
      rs:fixedlength="true" rs:maybenull="true"/>  
  </s:AttributeType>  
</s:Schema>  
<rs:data>  
  <z:row s1="1" CompanyName="Speedy Express" s3="(503) 555-9831"/>  
</rs:data>  
```  
  
 De même, car il n’est aucun alias ne défini pour `CompanyName` dans l’exemple précédent, `CompanyName` doit être utilisé de manière cohérente dans tout le document.  
  
## <a name="data-types"></a>Types de données  
 Vous pouvez appliquer un type de données à une colonne avec l’attribut dt : type. Pour le guide de référence pour les types XML autorisés, consultez la section Types de données de la [spécification W3C XML-Data](http://www.w3.org/TR/1998/NOTE-XML-data/). Vous pouvez spécifier un type de données de deux manières : spécifiez l’attribut dt : type directement sur la définition de colonne ou utiliser la construction s : DataType comme élément imbriqué de la définition de colonne. Par exemple,  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 est équivalent à  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 Si vous omettez l’attribut dt : type entièrement à partir de la définition de la ligne, par défaut, le type de colonne sera une chaîne de longueur variable.  
  
 Si vous disposez des informations de type plus que simplement le nom du type (par exemple, dt : maxLength), il est plus lisible à utiliser l’élément enfant s : DataType. Il s’agit simplement d’une convention, et n’est pas obligatoire.  
  
 Les exemples suivants montrent davantage comment inclure des informations de type dans votre schéma.  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!-or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!-- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!-- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!-- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 Il existe une utilisation subtile de l’attribut rs : fixedlength dans le deuxième exemple. Une colonne avec l’attribut rs : fixedlength la valeur true signifie que les données doivent avoir la longueur définie dans le schéma. Dans ce cas, une valeur valide pour title_id est « 123456 », en l’état « 123 ». Toutefois, « 123 » ne serait pas valide parce que sa longueur est 3, 6 pas. Consultez Guide du programmeur OLE DB pour obtenir une plus de la propriété fixedlength.  
  
## <a name="handling-nulls"></a>Gestion des valeurs null  
 Valeurs NULL sont gérées par l’attribut rs : maybenull. Si cet attribut est défini true, le contenu de la colonne peut contenir une valeur null. En outre, si la colonne est introuvable dans une ligne de données, l’utilisateur lit les données dans l’ensemble de lignes ::GetData() un état null. Prendre en compte les définitions de colonne suivantes à partir de la table expéditeurs.  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 Permet la définition `CompanyName` pour avoir la valeur null, mais `ShipperID` ne peut pas contenir une valeur null. Si la section de données contenue la ligne suivante, le fournisseur de persistance définirait l’état des données pour le `CompanyName` colonne à la constante d’état OLE DB DBSTATUS_S_ISNULL :  
  
```  
<z:row ShipperID="1"/>  
```  
  
 Si la ligne a été complètement vide, comme suit, le fournisseur de persistance retourne l’état OLE DB DBSTATUS_E_UNAVAILABLE pour `ShipperID` et DBSTATUS_S_ISNULL pour CompanyName.  
  
```  
<z:row/>   
```  
  
 Notez qu’une chaîne de longueur nulle n’est pas identique à la valeur null.  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 Pour la ligne précédente, le fournisseur de persistance retournera un état OLE DB DBSTATUS_S_OK pour les deux colonnes. Le `CompanyName` dans ce cas est simplement « » (une chaîne de longueur nulle).  
  
 Pour plus d’informations sur OLE DB construit disponibles pour une utilisation dans le schéma d’un document XML pour OLE DB, consultez la définition de « urn : schemas-microsoft-rowset » et le Guide du programmeur OLE DB.  
  
## <a name="see-also"></a>Voir aussi  
 [Persistance des enregistrements au format XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
