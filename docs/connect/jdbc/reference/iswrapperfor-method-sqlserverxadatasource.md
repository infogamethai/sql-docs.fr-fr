---
title: Méthode isWrapperFor (SQLServerXADataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d612461d-4c3f-46db-b968-ff4c80b2aa7c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e32cbf975d156aae723dfbff105fe51e039dc1b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977027"
---
# <a name="iswrapperfor-method-sqlserverxadatasource"></a>Méthode isWrapperFor (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indique si cet objet est un wrapper pour l'interface spécifiée.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Paramètres  
 *iface*  
  
 **Classe** définissant une interface.  
  
## <a name="return-value"></a>Valeur retournée  
 **true** si cet objet implémente l’interface ou encapsule un objet qui implémente l’interface. Dans le cas contraire, la valeur est **false**.  
  
## <a name="exceptions"></a>Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notes  
 La méthode [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) et la méthode [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) sont définies par l’interface java.sql.Wrapper, introduite dans les spécifications de JDBC 4.0.  
  
 Si cette méthode retourne la valeur True, l’appel de [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) avec le même argument réussit.  
  
 Pour plus d’informations, consultez [wrappers et interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Unwrap, &#40;méthode SQLServerXADataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)   
 [SQLServerXADataSource, méthodes](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource, membres](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource, classe](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
