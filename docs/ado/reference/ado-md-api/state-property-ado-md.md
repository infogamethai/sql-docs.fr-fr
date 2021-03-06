---
title: State, propriété (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c11bb74b62d54b1e2489cba5dd7cd35ee376a41
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949155"
---
# <a name="state-property-ado-md"></a>State, propriété (ADO MD)
Indique l’état actuel de l’ensemble de cellules.  
  
## <a name="return-values"></a>Valeurs de retour  
 Retourne un **Long** entier indiquant l’état actuel de la [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) de l’objet et est en lecture seule. Les valeurs suivantes sont valides : **adStateClosed** (0) et **adStateOpen** (1).  
  
## <a name="remarks"></a>Notes  
 Pour utiliser le [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) les noms de constantes, vous devez disposer de la bibliothèque de types ADO référencée dans votre projet. Consultez [à l’aide d’ADO avec ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) pour plus d’informations.  
  
## <a name="applies-to"></a>S'applique à  
 [Cellset, objet (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Close, méthode (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open, méthode (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
