---
title: Interopérabilité des instructions SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed366acde11778342387d3bcb152a6619a6a3778
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138869"
---
# <a name="interoperability-of-sql-statements"></a>Interopérabilité des instructions SQL
Comme le reste d’une application, les instructions SQL puissent être interopérable ou propres au SGBD. Et comme le reste de l’application, le choix du mode interopérables instructions SQL doivent être varie selon le type d’application. Les applications personnalisées sont moins susceptibles d’utiliser des instructions SQL interopérables, car elles sont généralement conçues pour exploiter les fonctions d’un ou deux éventuellement SGBD. Applications génériques utilisent des instructions SQL interopérables, car ils sont conçus pour fonctionner avec un large éventail de SGBD. Et applications verticales généralement situent quelque part entre les deux, exigeant un certain niveau de fonctionnalités, mais sinon à l’aide des instructions SQL interopérables.  
  
 Cette section contient les rubriques suivantes.  
  
-   [Choix d’une grammaire SQL](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [Construction d’instructions SQL interopérables](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
