---
title: Adostreamconstruction, Interface | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70a6dd02722a34159b345a83b32897aa8c38d0ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920788"
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction, interface
Le **ADOStreamConstruction** interface est utilisée pour construire une ADO **Stream** objet à partir d’un OLE DB **IStream** objet dans une application C/C++.  
  
## <a name="properties"></a>Properties  
  
|||  
|-|-|  
|[Stream, propriété](../../../ado/reference/ado-api/stream-property.md)|En lecture/écriture. Obtient/définit une OLE DB **Stream** objet.|  
  
## <a name="methods"></a>Méthodes  
 Aucune.  
  
## <a name="events"></a>Events  
 Aucune.  
  
## <a name="remarks"></a>Notes  
 Étant donné un OLE DB **IStream** objet (`pStream`), la construction de ADO **Stream** objet (`adoStr`) s’élève à trois opérations ci-après :  
  
1.  Créer un ADO **Stream** objet :  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  Requête la **IADOStreamConstruction** interface sur le **Stream** objet :  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 Appelez le `IADOStreamConstruction::get_Stream` méthode de propriété pour définir le OLE DB **IStream** objet sur le ADO **Stream** objet :  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 La résultante `adoStr` objet représente maintenant le ADO **Stream** objet construit à partir d’OLE DB **IStream** objet.  
  
## <a name="requirements"></a>Configuration requise  
 **Version :** ADO 2.0 ou une version ultérieure  
  
 **Bibliothèque :** msado15.dll  
  
 **UUID :** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Voir aussi  
 [Informations de référence sur l’API ADO](../../../ado/reference/ado-api/ado-api-reference.md)
