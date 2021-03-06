---
title: Expanded-QName (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c50409ea35809c52de718a8281bf76f75a5a0e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004584"
---
# <a name="functions-related-to-qnames---expanded-qname"></a>Fonctions relatives aux QName : expanded-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retourne une valeur du type xs : QName avec l’espace de noms URI spécifié dans le *$paramURI* et le nom local spécifié dans le *$paramLocal*. Si *$paramURI* est une chaîne vide ou la séquence vide, il ne représente aucun espace de noms.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>Arguments  
 *$paramURI*  
 URI d'espace de noms du QName.  
  
 *$paramLocal*  
 Partie du nom local du QName.  
  
## <a name="remarks"></a>Notes  
 Ce qui suit s’applique à la **se solde par** (fonction) :  
  
-   Si le *$paramLocal* valeur spécifiée n’est pas dans la forme lexicale correcte pour le type xs : NCName, la séquence vide est retournée et représente une erreur dynamique.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ne prend en charge la conversion du type xs:QName vers aucun autre type. Pour cette raison, le **se solde par** fonction ne peut pas être utilisée dans la construction XML. Par exemple, lorsque vous construisez un nœud, tel que `<e> expanded-QName(...) </e>`, la valeur doit être non typée. Cela suppose que vous convertissiez la valeur de type xs:QName renvoyée par `expanded-QName()` en xdt:untypedAtomic. Toutefois, cette opération n'est pas prise en charge. Une solution est proposée dans un exemple, plus loin dans cette rubrique.  
  
-   Vous pouvez modifier ou comparer les valeurs de type QName existantes. Par exemple, `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` compare la valeur de l’élément, <`e`>, au QName renvoyé par le **se solde par** (fonction).  
  
## <a name="examples"></a>Exemples  
 Cette rubrique fournit des exemples de XQuery relatifs à des instances XML stockés dans différentes **xml** colonnes de type le [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de données.  
  
### <a name="a-replacing-a-qname-type-node-value"></a>R. Remplacement d'une valeur de nœud de type QName  
 Cet exemple montre comment vous pouvez modifier la valeur d'un nœud d'élément de type QName. Cet exemple illustre les opérations suivantes :  
  
-   Crée une collection de schémas XML qui définit un élément de type QName.  
  
-   Crée une table avec un **xml** colonne de type à l’aide de la collection de schémas XML.  
  
-   Enregistre une instance XML dans la table.  
  
-   Utilise le **modify()** méthode du type de données xml pour modifier la valeur de l’élément de type QName dans l’instance. Le **se solde par** fonction est utilisée pour générer la nouvelle valeur de type QName.  
  
```  
-- If XML schema collection (if exists)  
-- drop xml schema collection SC  
-- go  
-- Create XML schema collection  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="QNameXSD"   
      xmlns:xqo="QNameXSD" elementFormDefault="qualified">  
      <element name="Root" type="xqo:rootType" />  
      <complexType name="rootType">  
            <sequence minOccurs="1" maxOccurs="1">  
                        <element name="ElemQN" type="xs:QName" />  
            </sequence>  
      </complexType>  
</schema>'  
go  
-- Create table.  
CREATE TABLE T( XmlCol xml(SC) )  
-- Insert sample XML instnace  
INSERT INTO T VALUES ('  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 Dans la requête suivante, le <`ElemQN`> valeur de l’élément est remplacé à l’aide de la **modify()** méthode de type de données xml et la valeur de remplacement de XML DML, comme indiqué.  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("https://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 Voici l'ensemble de résultats. Notez que l’élément <`ElemQN`> de QName type a maintenant une nouvelle valeur :  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="https://myURI">p1:myLocalName</ElemQN>  
</Root>  
```  
  
 Les instructions suivantes suppriment les objets utilisés dans l'exemple.  
  
```  
-- Cleanup  
DROP TABLE T  
go  
drop xml schema collection SC  
go  
```  
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>B. Gestion des limites liées à l'utilisation de la fonction expanded-QName()  
 Le **expanded-QName** fonction ne peut pas être utilisée dans la construction XML. L'exemple suivant illustre ce comportement. Pour contourner cette limite, l'exemple insère d'abord un nœud, puis le modifie.  
  
```  
-- if exists drop the table T  
--drop table T  
-- go  
-- Create XML schema collection  
-- DROP XML SCHEMA COLLECTION SC  
-- go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
 -- Create table T with a typed xml column (using the XML schema collection)  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- Insert an XML instance.  
insert into T values ('<root xmlns:a="https://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 La tentative suivante ajoute un autre <`root`> élément mais échoue, car la fonction se solde par n’est pas pris en charge dans la construction XML.  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 Une solution consiste à insérer une instance avec une valeur pour le <`root`> élément, puis le modifier. Dans cet exemple, une valeur initiale nil est utilisée lorsque le <`root`> élément est inséré. La collection de schémas XML dans cet exemple autorise une valeur nil pour le <`root`> élément.  
  
```  
update T SET xmlCol.modify('  
insert <root xsi:nil="true"/> as last into / ')  
go  
-- now replace the nil value with another QName.  
update T SET xmlCol.modify('  
replace value of /root[last()] with expanded-QName("http://ns","someLocalName") ')  
go  
 -- verify   
SELECT * FROM T  
go  
-- result  
<root>b</root>  
```  
  
 `<root xmlns:a="https://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 Vous pouvez comparer la valeur QName, comme le montre la requête ci-après. La requête retourne uniquement le <`root`> les éléments dont les valeurs correspondent le nom qualifié de type valeur retournée par la **se solde par** (fonction).  
  
```  
SELECT xmlCol.query('  
    for $i in /root  
    return  
       if ($i eq expanded-QName("http://ns","someLocalName") ) then  
          $i  
       else  
          ()')  
FROM T  
```  
  
### <a name="implementation-limitations"></a>Limites de mise en œuvre  
 Il existe une limite : Le **se solde par** fonction accepte la séquence vide comme deuxième argument et retourne un résultat vide au lieu de lever une erreur d’exécution lorsque le deuxième argument est incorrect.  
  
## <a name="see-also"></a>Voir aussi  
 [Fonctions relatives aux QName &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
