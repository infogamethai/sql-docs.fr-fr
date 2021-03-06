---
title: Allocation d’un descripteur d’instruction ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d50b0a31aed4935c805ca30620575ccff70d4a0b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077199"
---
# <a name="allocating-a-statement-handle-odbc"></a>Allocation d’un handle d’instruction dans ODBC
Avant de l’application peut exécuter une instruction, elle doit allouer un descripteur d’instruction comme suit :  
  
1.  L’application déclare une variable de type HSTMT. Il appelle ensuite **SQLAllocHandle** et transfère l’adresse de cette variable, le handle de la connexion dans laquelle allouer de l’instruction et l’option de SQL_HANDLE_STMT. Exemple :  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  Le Gestionnaire de pilotes alloue une structure dans lequel stocker les informations sur l’instruction et les appels **SQLAllocHandle** dans le pilote avec l’option de SQL_HANDLE_STMT.  
  
3.  Le pilote alloue sa propre structure dans lequel stocker les informations sur l’instruction et retourne le handle d’instruction de pilote pour le Gestionnaire de pilotes.  
  
4.  Le Gestionnaire de pilotes retourne le handle d’instruction de gestionnaire de pilotes à l’application dans la variable d’application.  
  
 Le descripteur d’instruction identifie quelle instruction à utiliser lors de l’appel de fonctions ODBC. Pour plus d’informations sur les descripteurs d’instruction, consultez [descripteurs d’instruction](../../../odbc/reference/develop-app/statement-handles.md).
