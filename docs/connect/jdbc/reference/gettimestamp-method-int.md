---
title: Méthode getTimestamp (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTimestamp (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a9fd6496-c72e-4cc6-b46a-4aa9f13f90ff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b9a349122b907ff535de8ba3f90e0746465d244
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978824"
---
# <a name="gettimestamp-method-int"></a>Méthode getTimestamp (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Récupère la valeur du paramètre désigné en tant qu'objet java.sql.Timestamp dans le langage de programmation Java en fonction de l'index de paramètre.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
public java.sql.Timestamp getTimestamp(int index)  
```  
  
#### <a name="parameters"></a>Paramètres  
 *index*  
  
 **Entier** qui indique l’index du paramètre.  
  
## <a name="return-value"></a>Valeur retournée  
 Objet d’horodatage.  
  
## <a name="exceptions"></a>Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notes  
 Cette méthode getTimestamp est spécifiée par la méthode getTimestamp de l’interface java.sql.CallableStatement.  
  
 Cette méthode retourne des valeurs seulement à partir des colonnes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** et **smalldatetime**.  
  
## <a name="see-also"></a>Voir aussi  
 [getTimestamp, méthode &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement, membres](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement, classe](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
