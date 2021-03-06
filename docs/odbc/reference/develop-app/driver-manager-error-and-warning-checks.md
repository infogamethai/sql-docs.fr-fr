---
title: Erreur du Gestionnaire de pilotes et les vérifications de l’avertissement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d0b136b9748de1991888abb0c19bc0d2ac65ea0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046971"
---
# <a name="driver-manager-error-and-warning-checks"></a>Vérifications des erreurs et avertissements du gestionnaire de pilotes
Le Gestionnaire de pilotes complètement ou partiellement implémente plusieurs fonctions et par conséquent vérifie pour tout ou partie des erreurs et avertissements dans ces fonctions.  
  
-   Implémente le Gestionnaire de pilotes **SQLDataSources** et **SQLDrivers** et recherche toutes les erreurs et avertissements dans ces fonctions.  
  
-   Le Gestionnaire de pilotes vérifie si un pilote implémente **SQLGetFunctions**. Si le pilote n’implémente pas **SQLGetFunctions**, le Gestionnaire de pilote implémente et vérifie toutes les erreurs et avertissements qu’il contient.  
  
-   Le Gestionnaire de pilotes implémente partiellement **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**,  **SQLFreeHandle**, **SQLGetDiagRec**, et **SQLGetDiagField** et recherche d’erreurs dans ces fonctions. Elle peut retourner les mêmes erreurs car le pilote pour certaines de ces fonctions, car tous deux effectuent des opérations similaires. Par exemple, le Gestionnaire de pilotes ou le pilote peut retourner SQLSTATE IM008 (échoué de la boîte de dialogue) si une est impossible d’afficher une boîte de dialogue de connexion pour **SQLDriverConnect**.
