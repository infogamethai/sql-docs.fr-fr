---
title: EndOfRecordset, événement (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a83f101d46a94a4ea43a85424677fc1c8da08be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918940"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset, événement (ADO)
Le **EndOfRecordset** événement est appelé lorsqu’une tentative de déplacement vers une ligne après la fin de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Paramètres  
 *fMoreData*  
 Un **VARIANT_BOOL** valeur qui, si la valeur VARIANT_TRUE, indique plus de lignes ont été ajoutées à la **Recordset**.  
  
 *adStatus*  
 Un [il ne](../../../ado/reference/ado-api/eventstatusenum.md) valeur d’état.  
  
 Lorsque **EndOfRecordset** est appelée, ce paramètre est défini sur **adStatusOK** si l’opération qui a provoqué l’événement a réussi. Il est défini sur **adStatusCantDeny** si cet événement ne peut pas demander l’annulation de l’opération qui a provoqué cet événement.  
  
 Avant de **EndOfRecordset** retourne, définissez ce paramètre sur **adStatusUnwantedEvent** pour éviter toute notification.  
  
 *pRecordset*  
 Un **Recordset** objet. Le **Recordset** pour laquelle cet événement s’est produit.  
  
## <a name="remarks"></a>Notes  
 Un **EndOfRecordset** événement peut se produire si le [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) opération échoue.  
  
 Ce gestionnaire d’événements est appelé lorsqu’une tentative est effectuée pour passer à la fin de la **Recordset** objet, peut-être suite à l’appel **MoveNext**. Toutefois, alors que dans ce cas, vous pouvez récupérer plusieurs enregistrements d’une base de données et les ajouter à la fin de la **Recordset**. Dans ce cas, définissez *fMoreData* à VARIANT_TRUE et à retourner **EndOfRecordset**. Appelez ensuite **MoveNext** à nouveau pour accéder aux nouveaux enregistrements récupérés.  
  
## <a name="see-also"></a>Voir aussi  
 [Exemple de modèle d’événements ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Présentation rapide du gestionnaire d’événements ADO](../../../ado/guide/data/ado-event-handler-summary.md)
