---
title: Gestion des erreurs et des Messages | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, about error handling
- errors [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], about messages
- ODBC error handling
- SQL_INVALID_HANDLE return code
- errors [ODBC], about error handling
- messages [ODBC]
ms.assetid: 74ea9630-e482-4a46-bb45-f5234f079b48
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4a4d87ccae235aee1a11e58aff60fe8e34d6205
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207092"
---
# <a name="handling-errors-and-messages"></a>Gestion des erreurs et des messages
  Lorsqu’une application appelle une fonction ODBC, le pilote exécute la fonction et retourne des informations de diagnostic de deux manières : Un code de retour indique la réussite ou l’échec d’une fonction ODBC globale et les enregistrements de diagnostic fournissent des informations détaillées sur la fonction. Les enregistrements de diagnostic comportent un enregistrement d'en-tête et des enregistrements d'état. Au moins un enregistrement de diagnostic, l'enregistrement d'en-tête, est retourné même si la fonction réussit.  
  
 Les informations de diagnostic sont utilisées au moment du développement pour intercepter les erreurs de programmation, telles que les handles non valides et les erreurs de syntaxe dans les instructions SQL codées de manière irréversible. Elles sont également utilisées au moment de l'exécution pour intercepter les avertissements et les erreurs d'exécution, tels que la troncation de données, les violations de règle et les erreurs de syntaxe des instructions SQL saisies par l'utilisateur. La logique du programme repose en général sur des codes de retour.  
  
 Par exemple, après qu’une application appelle **SQLFetch** pour récupérer les lignes dans un jeu de résultats, le code de retour indique si la fin du jeu de résultats a été atteinte (SQL_NO_DATA), si des messages d’information retournés (SQL_SUCCESS_ WITH_INFO), ou si une erreur s’est produite (SQL_ERROR).  
  
 Si le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pilote ODBC Native Client retourne la valeur autre que SQL_SUCCESS, l’application peut appeler **SQLGetDiagRec** pour extraire d’information ou des messages d’erreur. Utilisez **SQLGetDiagRec** pour faire défiler de haut et bas du message défini s’il y a plusieurs messages.  
  
 Le code de retour SQL_INVALID_HANDLE indique toujours une erreur de programmation et ne doit jamais se rencontrer au moment de l'exécution. Tous les autres codes de retour fournissent des informations d'exécution, bien que SQL_ERROR puisse indiquer une erreur de programmation.  
  
 La version d’origine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] API native, DB-Library for C, permet à une application installer la gestion des erreurs de rappel et les fonctions de gestion des messages que retournent des erreurs ou les messages. Certaines instructions [!INCLUDE[tsql](../../includes/tsql-md.md)], telles que PRINT, RAISERROR, DBCC et SET, retournent leurs résultats à la fonction gestionnaire des messages de DB-Library et non dans un jeu de résultats. Toutefois, l'API ODBC n'a aucune fonction de rappel similaire. Lorsque le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pilote ODBC Native Client détecte les messages provenant de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il définit le code de retour ODBC SQL_SUCCESS_WITH_INFO ou SQL_ERROR et retourne le message à une ou plusieurs enregistrements de diagnostic. Par conséquent, une application ODBC doit tester avec soin ces codes de retour et appel **SQLGetDiagRec** pour récupérer des données de message.  
  
 Pour plus d’informations sur le suivi des erreurs, consultez [Suivi de l’accès aux données](https://go.microsoft.com/fwlink/?LinkId=125805). Pour plus d’informations sur les améliorations apportées au suivi d’erreur ajouté dans [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], consultez [l’accès à des informations de Diagnostic dans le journal des événements étendus](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Dans cette section  
  
-   [Traitement des instructions qui génèrent des messages](processing-statements-that-generate-messages.md)  
  
-   [Enregistrements et champs de diagnostic](diagnostic-records-and-fields.md)  
  
-   [Numéros des erreurs natives](native-error-numbers.md)  
  
-   [SQLSTATE &#40;Codes d’erreur ODBC&#41;](sqlstate-odbc-error-codes.md)  
  
-   [Messages d’erreur](error-messages.md)  
  
## <a name="see-also"></a>Voir aussi  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
