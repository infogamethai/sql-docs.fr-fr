---
title: 'Étape 3 : Preuve de concept pour la connexion à SQL avec ADO.NET | Microsoft Docs'
description: Contient C# des exemples de code pour la connexion à SQL Server, l’exécution d’une requête et l’insertion d’une ligne.
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: rothja
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aebe3dc6-3ee4-4d11-8e43-5d32b3f91490
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: 2819697746f810e0c0b19a9ab7d076fa79c15a2f
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451815"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-adonet"></a>Étape 3 : Preuve de concept pour la connexion à SQL à l’aide d’ADO.NET

![Download-DownArrow-Circled](../../ssdt/media/download.png)[Télécharger ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

- Article précédent :&nbsp;&nbsp;&nbsp;[Étape 2 : Créer une base de données SQL pour le développement ADO.NET](step-2-create-sql-database-ado-net-development.md)  
- Article suivant :&nbsp;&nbsp;&nbsp;[Étape 4 : Connexion résiliente à SQL avec ADO.NET](step-4-connect-resiliently-sql-ado-net.md)  

  
Cet C# exemple de code doit être considéré comme une preuve de concept uniquement. L’exemple de code est simplifié par souci de clarté et ne représente pas nécessairement les meilleures pratiques recommandées par Microsoft.  
  
## <a name="step-1-connect"></a>Étape 1 : se connecter
  
La méthode **SqlConnection. Open** est utilisée pour se connecter à votre base de données SQL.  


```csharp
// C# , ADO.NET  
using System;
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  

                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
Press any key to finish...  
****/  
```  


## <a name="step-2-execute-a-query"></a>Étape 2 : Exécuter une requête  
  
La méthode SqlCommand. ExecuteReader :  
  
- Émet l’instruction SQL SELECT au système SQL.  
- Retourne une instance de SqlDataReader pour fournir l’accès aux lignes de résultat.  
  
  
  
```csharp
using System;  // C# , ADO.NET  
using DT = System.Data;            // System.Data.dll  
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  
  
                Program.SelectRows(connection);  
  
                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
  
        static public void SelectRows(QC.SqlConnection connection)  
        {  
            using (var command = new QC.SqlCommand())  
            {  
                command.Connection = connection;  
                command.CommandType = DT.CommandType.Text;  
                command.CommandText = @"  
SELECT  
    TOP 5  
        COUNT(soh.SalesOrderID) AS [OrderCount],  
        c.CustomerID,  
        c.CompanyName  
    FROM  
                        SalesLT.Customer         AS c  
        LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh  
            ON c.CustomerID = soh.CustomerID  
    GROUP BY  
        c.CustomerID,  
        c.CompanyName  
    ORDER BY  
        [OrderCount] DESC,  
        c.CompanyName; ";  
  
                QC.SqlDataReader reader = command.ExecuteReader();  
  
                while (reader.Read())  
                {  
                    Console.WriteLine("{0}\t{1}\t{2}",  
                        reader.GetInt32(0),  
                        reader.GetInt32(1),  
                        reader.GetString(2));  
                }  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
1       29736   Action Bicycle Specialists  
1       29638   Aerobic Exercise Company  
1       29546   Bulk Discount Store  
1       29741   Central Bicycle Specialists  
1       29612   Channel Outlet  
Press any key to finish...  
****/  
```  
  
  
  
## <a name="step-3-insert-a-row"></a>Étape 3 : insérer une ligne  
  
  
Cet exemple montre comment effectuer les opérations suivantes :  
  
- Exécutez une instruction SQL INSERT en toute sécurité en passant des paramètres.  
  - L’utilisation de paramètres protège contre les attaques par injection SQL.  
- Récupérez la valeur générée automatiquement.  
  
  
  
```csharp
using System;  // C# , ADO.NET  
using DT = System.Data;            // System.Data.dll  
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  
  
                Program.InsertRows(connection);  
  
                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
  
        static public void InsertRows(QC.SqlConnection connection)  
        {  
            QC.SqlParameter parameter;  
  
            using (var command = new QC.SqlCommand())  
            {  
                command.Connection = connection;  
                command.CommandType = DT.CommandType.Text;  
                command.CommandText = @"  
INSERT INTO SalesLT.Product  
        (Name,  
        ProductNumber,  
        StandardCost,  
        ListPrice,  
        SellStartDate  
        )  
    OUTPUT  
        INSERTED.ProductID  
    VALUES  
        (@Name,  
        @ProductNumber,  
        @StandardCost,  
        @ListPrice,  
        CURRENT_TIMESTAMP  
        ); ";  
  
                parameter = new QC.SqlParameter("@Name", DT.SqlDbType.NVarChar, 50);  
                parameter.Value = "SQL Server Express 2014";  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@ProductNumber", DT.SqlDbType.NVarChar, 25);  
                parameter.Value = "SQLEXPRESS2014";  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@StandardCost", DT.SqlDbType.Int);  
                parameter.Value = 11;  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@ListPrice", DT.SqlDbType.Int);  
                parameter.Value = 12;  
                command.Parameters.Add(parameter);  
  
                int productId = (int)command.ExecuteScalar();  
                Console.WriteLine("The generated ProductID = {0}.", productId);  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
The generated ProductID = 1000.  
Press any key to finish...  
****/  
```
