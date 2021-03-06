---
title: ReadText, méthode | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d6c174d2e6a659a3b9da8f89816b5bdf90342416
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917370"
---
# <a name="readtext-method"></a>ReadText, méthode
Lit un nombre spécifié de caractères à partir d’un texte [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objet.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Paramètres  
 *NumChars*  
 Facultatif. Un **Long** valeur qui spécifie le nombre de caractères à lire à partir du fichier, ou un [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) valeur. La valeur par défaut est **adReadAll**.  
  
## <a name="return-value"></a>Valeur de retour  
 Le **ReadText** méthode lit un nombre spécifié de caractères, une ligne entière ou l’intégralité du flux à partir d’un **Stream** de l’objet et retourne la chaîne résultante.  
  
## <a name="remarks"></a>Notes  
 Si *NUMCHARS* est supérieur au nombre de caractères présents dans le flux, seuls les caractères restants sont retournés. La chaîne lue n’est pas remplie pour correspondre à la longueur spécifiée par *NUMCHARS*. S’il n’y a aucun caractère reste à lire, une valeur de type variant null est retournée. **ReadText** ne peut pas être utilisé pour lire vers l’arrière.  
  
> [!NOTE]
>  Le **ReadText** méthode est utilisée avec des flux de texte ([Type](../../../ado/reference/ado-api/type-property-ado-stream.md) est **adTypeText**). Pour les flux binaires (**Type** est **adTypeBinary**), utilisez [en lecture](../../../ado/reference/ado-api/read-method.md).  
  
 Les requêtes qui résultent d’une grande quantité de données XML renvoyées par le biais le **ReadText** méthode de l’objet Stream de ActiveX Data Object (ADO) peut prendre beaucoup de temps à s’exécuter ; si cette opération est effectuée dans un composant COM + qui est appelé à partir d’un Page ASP, la session utilisateur peut expirer. ADO convertit les données de l’objet Stream à partir de l’encodage UTF-8 en Unicode ; la réallocation de mémoire fréquent impliquée dans la conversion d’une grande quantité de données à la fois est très longue. Pour résoudre, effectuer des appels répétés à la **ReadText** méthode de ADO command, objet et spécifiez un plus petit nombre de caractères. Les tests ont montré qu’une valeur équivalente à 128 Ko (131 072) est optimale. Temps de réponse réduit que cette valeur est diminuée. Pour plus d’informations, consultez l’article de la Base de connaissances 280067, « PRB : Récupération des Documents XML très volumineux à partir de SQL Server 2000 à l’aide de l’objet ADO stream ReadText, méthode peuvent être lente », dans la Base de connaissances Microsoft à https://support.microsoft.com.  
  
## <a name="applies-to"></a>S'applique à  
 [Stream, objet (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Read, méthode](../../../ado/reference/ado-api/read-method.md)
