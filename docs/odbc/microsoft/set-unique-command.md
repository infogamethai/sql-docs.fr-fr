---
title: SET UNIQUE, commande | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29598ed97cba8be04a0c08727cffc40e663becba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063616"
---
# <a name="set-unique-command"></a>SET UNIQUE, commande
Spécifie si les enregistrements avec les valeurs de clés d’index en double sont conservées dans un fichier d’index.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>Arguments  
 ON  
 Spécifie que n’importe quel enregistrement avec une valeur de clé d’index dupliquées ne pas être inclus dans le fichier d’index. Seul le premier enregistrement avec la valeur de clé d’index d’origine est inclus dans le fichier d’index.  
  
 OFF  
 (Valeur par défaut). Spécifie que les enregistrements avec les valeurs de clé d’index dupliquées inclus dans le fichier d’index.  
  
## <a name="remarks"></a>Notes  
 Un fichier d’index conserve son paramètre de valeur UNIQUE lorsque vous émettez la RÉINDEXATION. Pour plus d’informations, consultez [INDEX](../../odbc/microsoft/index-command.md).
