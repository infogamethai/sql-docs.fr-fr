---
title: Requêtes XQuery impliquant un ordre | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- XQuery, sequence
- ordered expressions [XQuery]
ms.assetid: 4f1266c5-93d7-402d-94ed-43f69494c04b
author: rothja
ms.author: jroth
ms.openlocfilehash: 4fc30086978e26f53f7a4fdbab8a731ac2334181
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946110"
---
# <a name="xqueries-involving-order"></a>Requêtes XQuery impliquant un ordre
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Le concept de séquence n'existe pas dans les bases de données relationnelles. Il est, par exemple, impossible de créer une requête telle que « Obtenir le premier client de la base de données ». Toutefois, vous pouvez interroger un document XML et extraire le premier \<client > élément. Vous récupérez alors toujours le même client.  
  
 Cette rubrique présente les requêtes s'appuyant sur l'ordre dans lequel les nœuds apparaissent dans le document.  
  
## <a name="examples"></a>Exemples  
  
### <a name="a-retrieve-manufacturing-steps-at-the-second-work-center-location-for-a-product"></a>R. Récupération des étapes de fabrication sur le deuxième poste de travail pour un produit  
 Pour un modèle de produit spécifique, la requête suivante récupère les étapes de fabrication sur le deuxième poste de travail dans l'ordre des postes de travail que comprend le processus de fabrication.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    <ManuStep ProdModelID = "{sql:column("Production.ProductModel.ProductModelID")}"  
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
     <Location>  
       { (//AWMI:root/AWMI:Location)[2]/@* }  
       <Steps>  
         { for $s in (//AWMI:root/AWMI:Location)[2]//AWMI:step  
           return  
              <Step>  
               { string($s) }  
              </Step>  
         }  
        </Steps>  
      </Location>  
     </ManuStep>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Notez les points suivants dans la requête précédente :  
  
-   Les expressions entre accolades sont remplacées par le résultat de son évaluation. Pour plus d’informations, consultez [Construction XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md).  
  
-   **@\*** Récupère tous les attributs du deuxième poste de travail.  
  
-   L’itération FLWOR (pour... RETURN) récupère tous les <`step`> emplacement du centre les éléments enfants du deuxième travail.  
  
-   Le [fonction SQL :Column() (XQuery)](../xquery/xquery-extension-functions-sql-column.md) contient la valeur relationnelle dans le code XML qui est en cours de construction.  
  
 Voici le résultat obtenu :  
  
```  
<ManuStep ProdModelID="7" ProductModelName="HL Touring Frame">  
  <Location LocationID="20" SetupHours="0.15"   
              MachineHours="2"  LaborHours="1.75" LotSize="1">  
  <Steps>  
   <Step>Assemble all frame components following blueprint 1299.</Step>  
     ...  
  </Steps>  
 </Location>  
</ManuStep>    
```  
  
 La requête précédente récupère uniquement les nœuds de texte. Si vous souhaitez que la totalité <`step`> élément retourné à la place, supprimez le **string()** fonction à partir de la requête :  
  
### <a name="b-find-all-the-material-and-tools-used-at-the-second-work-center-location-in-the-manufacturing-of-a-product"></a>B. Recherche des matières et outils utilisés sur le deuxième poste de travail au cours de la fabrication d'un produit  
 Pour un modèle de produit spécifique, la requête suivante récupère les outils et les matières utilisés sur le deuxième poste de travail dans l'ordre des postes de travail que comprend le processus de fabrication.  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <Location>  
      { (//AWMI:root/AWMI:Location)[1]/@* }  
       <Tools>  
         { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:tool  
           return  
              <Tool>  
                { string($s) }  
              </Tool>  
          }  
        </Tools>  
        <Materials>  
            { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:material  
              return  
                 <Material>  
                    { string($s) }  
                 </Material>  
             }  
         </Materials>  
  </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Notez les points suivants dans la requête précédente :  
  
-   La requête construit le < Loca`tion`> élément et récupère son attribut de valeurs à partir de la base de données.  
  
-   Elle utilise deux itérations FLWOR (for...return) : la première pour récupérer les outils et la deuxième pour récupérer les matières.  
  
 Voici le résultat obtenu :  
  
```xml
<Location LocationID="10" SetupHours=".5"   
          MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
    <Tool>router with a carbide tip 15</Tool>  
    <Tool>Forming Tool FT-15</Tool>  
  </Tools>  
  <Materials>  
    <Material>aluminum sheet MS-2341</Material>  
  </Materials>  
</Location>  
```  
  
### <a name="c-retrieve-the-first-two-product-feature-descriptions-from-the-product-catalog"></a>C. Récupération des descriptions des deux premiers composants d'un produit à partir du catalogue du produit  
 Pour un modèle de produit spécifique, la requête récupère les descriptions de deux fonctionnalité première à partir de la <`Features`> élément dans le catalogue de modèle de produit.  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <ProductModel ProductModelID= "{ data( (/p1:ProductDescription/@ProductModelID)[1] ) }"  
                   ProductModelName = "{ data( (/p1:ProductDescription/@ProductModelName)[1] ) }" >  
       {  
         for $F in /p1:ProductDescription/p1:Features  
         return   
           $F/*[position() <= 2]   
       }  
     </ProductModel>  
      ') as x  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Notez les points suivants dans la requête précédente :  
  
 Le corps de la requête construit du code XML qui inclut le <`ProductModel`> élément qui possède les attributs ProductModelID et ProductModelName.  
  
-   La requête utilise une boucle FOR... RETURN pour récupérer les descriptions de fonctionnalité de modèle de produit. Le **position()** fonction est utilisée pour récupérer les deux premières caractéristiques.  
  
 Voici le résultat obtenu :  
  
```xml
<ProductModel ProductModelID="19" ProductModelName="Mountain 100">  
 <p1:Warranty   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
  <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
 <p2:Maintenance   
  xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p2:NoOfYears>10</p2:NoOfYears>  
  <p2:Description>maintenance contact available through your dealer   
            or any AdventureWorks retail store.  
  </p2:Description>  
 </p2:Maintenance>  
</ProductModel>   
```  
  
### <a name="d-find-the-first-two-tools-used-at-the-first-work-center-location-in-the-manufacturing-process-of-the-product"></a>D. Recherche des deux premiers outils utilisés sur le premier poste de travail du processus de fabrication du produit  
 Pour un modèle de produit spécifique, la requête suivante récupère les deux premiers outils utilisés sur le premier poste de travail dans l'ordre des postes de travail que comprend le processus de fabrication. La requête est spécifiée sur les instructions de fabrication stockées dans le **Instructions** colonne de la **Production.ProductModel** table.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   for $Inst in (//AWMI:root/AWMI:Location)[1]  
   return   
     <Location>  
       { $Inst/@* }  
       <Tools>  
         { for $s in ($Inst//AWMI:step//AWMI:tool)[position() <= 2]  
           return  
             <Tool>  
               { string($s) }  
             </Tool>  
         }  
       </Tools>  
     </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Voici le résultat obtenu :  
  
```xml
<Location LocationID="10" SetupHours=".5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
  </Tools>  
</Location>   
```  
  
### <a name="e-find-the-last-two-manufacturing-steps-at-the-first-work-center-location-in-the-manufacturing-of-a-specific-product"></a>E. Recherche des deux dernières étapes de fabrication sur le premier poste de travail au cours de la fabrication d'un produit spécifique  
 La requête utilise le **last()** fonction pour récupérer les deux dernières étapes de fabrication.  
  
```sql
SELECT Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Voici le résultat obtenu :  
  
```xml
<LastTwoManuSteps>  
   <Last-1Step>When finished, inspect the forms for defects per   
               Inspection Specification .</Last-1Step>  
   <LastStep>Remove the frames from the tool and place them in the   
             Completed or Rejected bin as appropriate.</LastStep>  
</LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Données XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Références relatives au langage Xquery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Construction XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
