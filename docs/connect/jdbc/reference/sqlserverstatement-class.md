---
title: SQLServerStatement, classe | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec24963c-8b51-4838-91e9-1fbfa2347451
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 89547655fd734ca9e6e340d94832dea5816f2733
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970379"
---
# <a name="sqlserverstatement-class"></a>SQLServerStatement, classe
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Représente l'implémentation de base de la fonctionnalité d'instruction JDBC.  
  
 **Package :** com.microsoft.sqlserver.jdbc  
  
 **Implémente :** [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
public class SQLServerStatement  
```  
  
## <a name="remarks"></a>Notes  
 La classe SQLServerStatement fournit également un certain nombre de méthodes d’implémentation de classe de base pour l’instruction préparée JDBC et les instructions pouvant être appelées. Le rôle de base de la classe SQLServerStatement est d’exécuter des instructions SQL, puis de retourner des nombres de mises à jour et des jeux de résultats à l’application utilisateur.  
  
 Cette classe prend en charge la désencapsulation dans la classe SQLServerStatement, l’interface ISQLServerStatement et l’interface java. Sql. Statement. Pour plus d’informations, consultez [wrappers et interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Voir aussi  
 [SQLServerStatement, membres](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Informations de référence sur l'API du pilote JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
