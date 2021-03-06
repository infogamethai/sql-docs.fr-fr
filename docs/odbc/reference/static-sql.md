---
title: SQL statique | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e6d053e4d2a5520432c4c1debbafb35fdb17bc4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016739"
---
# <a name="static-sql"></a>SQL statique
Embedded SQL illustré [Embedded SQL exemple](../../odbc/reference/embedded-sql-example.md) SQL statique est appelée. Elle est appelée SQL statique, car les instructions SQL dans le programme sont statiques ; Autrement dit, ils ne changent pas chaque fois que le programme est exécuté. Comme décrit dans la section précédente, ces instructions sont compilées lors de la compilation le reste du programme.  
  
 SQL statique fonctionne bien dans de nombreuses situations et peut être utilisé dans n’importe quelle application pour laquelle l’accès aux données peut être déterminée au moment du design programme. Par exemple, un programme de saisie de commandes utilise toujours la même instruction pour insérer une nouvelle commande et un système de réservation des compagnies aériennes utilise toujours la même instruction pour modifier l’état d’un siège disponibles à réservé. Chacune de ces instructions est généralisé via l’utilisation de variables de l’hôte ; des valeurs différentes peuvent être insérés dans une commande client et les sièges différents peuvent être réservées. Étant donné que ces instructions peuvent être codées en dur dans le programme, ces programmes ont l’avantage que les instructions doivent être analysées, validées et optimisé qu’une seule fois, au moment de la compilation. Cela entraîne un code relativement rapide.
