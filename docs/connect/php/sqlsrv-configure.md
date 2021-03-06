---
title: sqlsrv_configure | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_configure
apitype: NA
helpviewer_keywords:
- sqlsrv_configure
- API Reference, sqlsrv_configure
ms.assetid: 9393f975-a4ef-4c50-b4dd-14892fc55cc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b98533dcc1589e07bc8ae37562bf6734077a78f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935806"
---
# <a name="sqlsrvconfigure"></a>sqlsrv_configure
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Modifie les paramètres de gestion des erreurs et les options de journalisation.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sqlsrv_configure( string $setting, mixed $value )  
```  
  
#### <a name="parameters"></a>Paramètres  
*$setting*: nom du paramètre à configurer. Consultez le tableau ci-dessous pour obtenir la liste des paramètres.  
  
*$value*: valeur à appliquer au paramètre spécifié dans le paramètre *$setting* . Les valeurs possibles pour ce paramètre dépendent du paramètre spécifié. Le tableau suivant répertorie les combinaisons possibles :  
  
|Paramètre|Valeurs possibles pour le paramètre $value (entier équivalent entre parenthèses)|Valeur par défaut|  
|-----------|------------------------------------------------------------------------------|-----------------|  
|ClientBufferMaxKBSize<sup>1</sup>|Nombre non négatif jusqu’à la limite de mémoire PHP.<br /><br />Zéro et les nombres négatifs ne sont pas autorisés.|10 240 Ko|  
|LogSeverity<sup>2</sup>|SQLSRV_LOG_SEVERITY_ALL (-1)<br /><br />SQLSRV_LOG_SEVERITY_ERROR (1)<br /><br />SQLSRV_LOG_SEVERITY_NOTICE (4)<br /><br />SQLSRV_LOG_SEVERITY_WARNING (2)|SQLSRV_LOG_SEVERITY_ERROR (1)|  
|LogSubsystems<sup>2</sup>|SQLSRV_LOG_SYSTEM_ALL (-1)<br /><br />SQLSRV_LOG_SYSTEM_CONN (2)<br /><br />SQLSRV_LOG_SYSTEM_INIT (1)<br /><br />SQLSRV_LOG_SYSTEM_OFF (0)<br /><br />SQLSRV_LOG_SYSTEM_STMT (4)<br /><br />SQLSRV_LOG_SYSTEM_UTIL (8)|SQLSRV_LOG_SYSTEM_OFF (0)|  
|WarningsReturnAsErrors<sup>3</sup>|**true** (1) ou **false** (0)|**true** (1)|  
  
## <a name="return-value"></a>Valeur retournée  
Si **sqlsrv_configure** est appelé avec un paramètre ou une valeur non pris en charge, la fonction retourne **false**. Sinon, elle retourne **true**.  
  
## <a name="remarks"></a>Notes  
(1) Pour plus d’informations sur les requêtes côté client, voir [Types de curseurs &#40;pilote SQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md).  
  
(2) Pour plus d’informations sur la journalisation de l’activité, voir [Journalisation de l’activité](../../connect/php/logging-activity.md).  
  
(3) Pour plus d’informations sur la configuration de la gestion des erreurs et des avertissements, voir [Guide pratique pour configurer la gestion des erreurs et des avertissements avec le pilote SQLSRV](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md).  
  
## <a name="see-also"></a>Voir aussi  
[Informations de référence sur l’API du pilote SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Guide de programmation pour les pilotes Microsoft pour PHP pour SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md) 
  
