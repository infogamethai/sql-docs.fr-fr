---
title: updateBinaryStream, méthode (int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1db3a975-c108-45d1-8c0d-14a094f391bd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a1b69d4f4e1845b4ec86297c06298c1302becea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985374"
---
# <a name="updatebinarystream-method-int-javaioinputstream"></a>Méthode updateBinaryStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Met à jour la colonne désignée avec la valeur de flux binaire.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
public void updateBinaryStream(int columnIndex,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Paramètres  
 *columnIndex*  
  
 **Entier** qui indique l’index de colonne.  
  
 *x*  
  
 Objet InputStream.  
  
## <a name="exceptions"></a>Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notes  
 Cette méthode updateBinaryStream est spécifiée par la méthode updateBinaryStream dans l’interface java. Sql. ResultSet.  
  
 L’utilisation de cette méthode pour les types de données **image**, **Text**et **ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] peut avoir un impact sur les performances.  
  
 Cette méthode passe les octets à partir d’un objet InputStream à des colonnes binaires [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sélectionnées, telles que binary, varbinary, varbinary(max), image, xml et udt. La mise à jour de colonnes de caractères n'est pas prise en charge avec cette méthode. Pour mettre à jour des colonnes de caractères avec InputStream, utilisez la méthode [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md).  
  
## <a name="see-also"></a>Voir aussi  
 [updateBinaryStream, méthode &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet, membres](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet, classe](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
