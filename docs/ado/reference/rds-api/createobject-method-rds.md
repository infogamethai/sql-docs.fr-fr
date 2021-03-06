---
title: CreateObject, méthode (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6b50714cdff536418e759828d972c16abd7d7a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964544"
---
# <a name="createobject-method-rds"></a>CreateObject, méthode (RDS)
Crée le proxy pour l’objet métier cible et retourne un pointeur vers elle. Les packages et marshale données proxy pour le stub côté serveur pour les communications avec l’objet métier envoyer des demandes et les données sur Internet. Pour les objets de composant in-process, aucun proxy ne sont utilisés, un pointeur vers l’objet est fourni.  
  
> [!IMPORTANT]
>  Depuis Windows 8 et Windows Server 2012, composants de serveur Services Bureau à distance ne sont plus inclus dans le système d’exploitation Windows (voir Windows 8 et [Guide de compatibilité de Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) pour plus de détails). Composants du client RDS seront supprimées dans une future version de Windows. Évitez d'utiliser cette fonctionnalité dans de nouveaux travaux de développement, et prévoyez de modifier les applications qui utilisent actuellement cette fonctionnalité. Les applications qui utilisent des services Bureau à distance doivent migrer vers [Service de données WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntaxe  
 Service de données distant prend en charge les protocoles suivants : HTTP, HTTPS (HTTP sur Secure Socket Layer), DCOM et in-process.  
  
|Protocol|Syntaxe|  
|--------------|------------|  
|HTTP|Objet de jeu = DataSpace.CreateObject (« ProgId », « https\://awebsrvr »)|  
|HTTPS|Objet de jeu = DataSpace.CreateObject (« ProgId », « https\://awebsrvr »)|  
|DCOM|Objet de jeu = DataSpace.CreateObject (« ProgId », « computername »)|  
|In-process|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>Paramètres  
 *Objet*  
 Une variable objet qui correspond à un objet qui est du type spécifié dans *ProgID*.  
  
 *Espace de données*  
 Une variable objet qui représente un [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objet utilisé pour créer une instance du nouvel objet.  
  
 *ProgID*  
 Un **chaîne** valeur qui contient l’identificateur programmatique spécifiant un objet métier côté serveur qui implémente les règles d’entreprise de votre application.  
  
 *awebsrvr* ou *Nom_Ordinateur*  
 Un **chaîne** valeur qui représente une URL qui identifie le serveur Web des Internet Information Services (IIS) où une instance de l’objet métier du serveur est créée.  
  
## <a name="remarks"></a>Notes  
 Le *protocole HTTP* est le protocole Web standard ; *HTTPS* est un protocole Web sécurisé. Utilisez le *du protocole DCOM* lorsque vous exécutez un réseau local sans protocole HTTP. Le *intra-processus* protocole est une bibliothèque de liens dynamiques (DLL) locale ; il n’utilise pas de réseau.  
  
## <a name="applies-to"></a>S'applique à  
 [DataSpace, objet (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Objet DataFactory, méthode de requête et exemple CreateObject, méthode (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [DataSpace et la méthode CreateObject, exemple (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [CreateRecordset, méthode (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


