---
title: Requêtes XQuery impliquant une hiérarchie | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
author: rothja
ms.author: jroth
ms.openlocfilehash: 8aa762af8e08c72f7f00369219771c371ce39aac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946106"
---
# <a name="xqueries-involving-hierarchy"></a>Requêtes XQuery impliquant une hiérarchie
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La plupart des **xml** colonnes de type le **AdventureWorks** base de données sont des documents semi-structurés. Par conséquent, les documents stockés dans chaque ligne peuvent avoir un aspect différent. Les exemples de requêtes fournis dans cette rubrique montrent comment extraire des informations de ces divers documents.  
  
## <a name="examples"></a>Exemples  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>R. Extraction, à partir des instructions de fabrication, des postes de travail ainsi que de la première étape de fabrication réalisée sur ces différents postes  
 Pour le modèle de produit 7, la requête construit le document XML qui comprend le <`ManuInstr`> élément, avec **ProductModelID** et **ProductModelName** attributs et un ou plusieurs <`Location`> éléments enfants.  
  
 Chaque <`Location`> élément possède son propre ensemble d’attributs et d’un <`step`> élément enfant. Cela <`step`> élément enfant est la première étape de fabrication sur le poste de travail.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   \<ManuInstr  ProdModelID = "{sql:column("Production.ProductModel.ProductModelID") }"   
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
            {   
              for $wc in //AWMI:root/AWMI:Location  
              return  
                <Location>  
                 {$wc/@* }  
                 <step1> { string( ($wc//AWMI:step)[1] ) } </step1>  
                </Location>  
            }  
          </ManuInstr>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Notez les points suivants dans la requête précédente :  
  
-   Le **espace de noms** mot clé dans le [prologue XQuery](../xquery/modules-and-prologs-xquery-prolog.md) définit un préfixe d’espace de noms. Ce préfixe est utilisé ultérieurement dans le corps de requête.  
  
-   Les jetons de basculement de contexte, {) et (}, sont utilisés pour faire passer la requête de la construction XML à sa propre évaluation.  
  
-   Le **SQL :Column()** est utilisé pour inclure une valeur relationnelle dans le code XML qui est en cours de construction.  
  
-   Lors de la construction du <`Location`> élément, $wc/@* récupère tous les attributs emplacement du centre de travail.  
  
-   Le **string()** fonction retourne la valeur de chaîne dans le <`step`> élément.  
  
 Voici un extrait du résultat :  
  
```xml
<ManuInstr ProdModelID="7" ProductModelName="HL Touring Frame">  
   <Location LocationID="10" SetupHours="0.5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
     <step1>Insert aluminum sheet MS-2341 into the T-85A   
             framing tool.</step1>  
   </Location>  
   <Location LocationID="20" SetupHours="0.15"   
            MachineHours="2" LaborHours="1.75" LotSize="1">  
      <step1>Assemble all frame components following   
             blueprint 1299.</step1>  
   </Location>  
...  
</ManuInstr>   
```  
  
### <a name="b-find-all-telephone-numbers-in-the-additionalcontactinfo-column"></a>B. Recherche de tous les numéros de téléphone de la colonne AdditionalContactInfo  
 La requête suivante récupère les numéros de téléphone supplémentaires pour un contact client spécifique en parcourant la hiérarchie entière pour le <`telephoneNumber`> élément. Étant donné que le <`telephoneNumber`> élément peut apparaître n’importe où dans la hiérarchie, la requête utilise l’opérateur descendant- and -self (/ /) dans la recherche.  
  
```sql
SELECT AdditionalContactInfo.query('  
 declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
```  
  
 Voici le résultat obtenu :  
  
```xml
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  112-111-1111  
\</act:number>  
```  
  
 Pour récupérer uniquement les numéros de téléphone de premier niveau, en particulier le <`telephoneNumber`> éléments enfants de <`AdditionalContactInfo`>, l’expression FOR de la requête passe à  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber` .  
  
## <a name="see-also"></a>Voir aussi  
 [Principes fondamentaux de XQuery](../xquery/xquery-basics.md)   
 [Construction XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [Données XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
