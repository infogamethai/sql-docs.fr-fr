---
title: Sqlfreeenv, mappage | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeEnv
ms.assetid: c0f76455-d072-4bae-bee7-452277dfa479
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef89943f95a6492614972c3e89fe2129becc1aa5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086422"
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv, mappage
Lorsqu’une application appelle **SQLFreeEnv** via une application ODBC *3.x* pilote, l’appel à  
  
```  
SQLFreeEnv(henv)   
```  
  
 est mappé à  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 avec le *gérer* affectée à la valeur de l’argument *henv*.
