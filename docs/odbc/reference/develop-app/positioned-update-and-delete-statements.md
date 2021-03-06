---
title: Mise à jour et des instructions Delete positionnées | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b37bdfae5f97a453477768aca39b801c06c0701
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023292"
---
# <a name="positioned-update-and-delete-statements"></a>Instructions de mise à jour et de suppression positionnées
Les applications peuvent mettre à jour ou supprimer la ligne actuelle dans un jeu de résultats avec une mise à jour positionnée ou instruction. Mise à jour et delete positionnées instructions sont prises en charge par certaines sources de données, mais pas tous. Pour déterminer si un prend en charge de source de données positionné instructions update et delete, une application appelle **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 *InfoType* (selon le type du curseur). Notez que la bibliothèque de curseurs ODBC simule la mise à jour positionnée et supprimer des instructions.  
  
 Pour utiliser une mise à jour positionnée ou l’instruction delete, l’application doit créer un jeu de résultats avec un **Sélectionnez pour mettre à jour** instruction. La syntaxe de cette instruction est :  
  
 **SELECT** [**ALL** &#124; **DISTINCT**] *select-list*  
  
 **À partir de** *liste de références de table*  
  
 [**Où** *condition de recherche*]  
  
 **POUR la mise à jour de** [*nom-colonne* [ **,** *nom-colonne*]...]  
  
 L’application puis place le curseur sur la ligne d’être mis à jour ou supprimées. Il peut le faire en appelant **SQLFetchScroll** pour récupérer un ensemble de lignes contenant la ligne requise et l’appel **SQLSetPos** pour positionner le curseur de jeu de lignes sur cette ligne. L’application exécute ensuite la mise à jour positionnée ou une instruction delete sur une autre instruction que l’instruction utilisée par le jeu de résultats. La syntaxe de ces instructions est :  
  
 **Mise à jour** *nom de la table*  
  
 **Définissez** *identificateur de colonne* **=** {*expression* &#124; **NULL**}  
  
 [ **,** *identificateur de colonne* **=** {*expression* &#124; **NULL**}]...  
  
 **WHERE CURRENT OF** *nom de curseur*  
  
 **DELETE FROM** *nom de la table* **WHERE CURRENT OF** *nom de curseur*  
  
 Notez que ces instructions requièrent un nom de curseur. L’application peut spécifier un nom de curseur avec **SQLSetCursorName** avant l’exécution de l’instruction qui crée le résultat de définie ou pouvez laisser la source de données automatiquement générer un nom de curseur lorsque le curseur est créé. Dans ce cas, l’application récupère ce nom de curseur pour une utilisation dans les instructions de suppression et de mise à jour positionnée en appelant **SQLGetCursorName**.  
  
 Par exemple, le code suivant permet à un utilisateur à faire défiler la table Customers et supprimer des enregistrements de client ou mettre à jour leurs adresses et les numéros de téléphone. Il appelle **SQLSetCursorName** pour spécifier un nom de curseur avant qu’il crée le jeu de résultats de clients et utilise trois descripteurs d’instruction : *hstmtCust* du jeu de résultats, *hstmtUpdate* pour une instruction de mise à jour positionnée, et *hstmtDelete* pour un texte positionné instruction delete. Bien que le code peut lier des variables distinctes pour les paramètres dans l’instruction de mise à jour positionnée, il met à jour les mémoires tampons d’ensemble de lignes et lie les éléments de ces mémoires tampons. Cela permet de conserver les tampons de l’ensemble de lignes synchronisées avec les données mises à jour.  
  
```  
#define POSITIONED_UPDATE 100  
#define POSITIONED_DELETE 101  
  
SQLUINTEGER    CustIDArray[10];  
SQLCHAR        NameArray[10][51], AddressArray[10][51],   
               PhoneArray[10][11];  
SQLINTEGER     CustIDIndArray[10], NameLenOrIndArray[10],   
               AddressLenOrIndArray[10],  
               PhoneLenOrIndArray[10];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLHSTMT       hstmtCust, hstmtUpdate, hstmtDelete;  
  
// Set the SQL_ATTR_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmtCust, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmtCust, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]),  
            NameLenOrIndArray);  
SQLBindCol(hstmtCust, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
         AddressLenOrIndArray);  
SQLBindCol(hstmtCust, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Set the cursor name to Cust.  
SQLSetCursorName(hstmtCust, "Cust", SQL_NTS);  
  
// Prepare positioned update and delete statements.  
SQLPrepare(hstmtUpdate,  
   "UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust",  
   SQL_NTS);  
SQLPrepare(hstmtDelete, "DELETE FROM Customers WHERE CURRENT OF Cust", SQL_NTS);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmtCust,  
   "SELECT CustID, Name, Address, Phone FROM Customers FOR UPDATE OF Address, Phone",  
   SQL_NTS);  
  
// Fetch and display the first 10 rows.  
SQLFetchScroll(hstmtCust, SQL_FETCH_NEXT, 0);  
DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray, AddressArray,  
            AddressLenOrIndArray, PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
  
// Call GetAction to get an action and a row number from the user.  
while (GetAction(&Action, &RowNum)) {  
   switch (Action) {  
  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmtCust, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray, PhoneArray,  
                     PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case POSITIONED_UPDATE:  
         // Get the new data and place it in the rowset buffers.  
         GetNewData(AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                     PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Bind the elements of the arrays at position RowNum-1 to the   
         // parameters of the positioned update statement.  
         SQLBindParameter(hstmtUpdate, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           50, 0, AddressArray[RowNum - 1], sizeof(AddressArray[0]),  
                           &AddressLenOrIndArray[RowNum - 1]);  
         SQLBindParameter(hstmtUpdate, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           10, 0, PhoneArray[RowNum - 1], sizeof(PhoneArray[0]),  
                           &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned update statement to update the row.  
         SQLExecute(hstmtUpdate);  
         break;  
  
      case POSITIONED_DELETE:  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned delete statement to delete the row.  
         SQLExecute(hstmtDelete);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmtCust);  
```
