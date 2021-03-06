---
title: srv_paramset (API de procédure stockée étendue) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramset
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramset
ms.assetid: 2a509206-a1b8-4b20-b0a2-ef680cef7bd8
author: rothja
ms.author: jroth
ms.openlocfilehash: c3ec0de44aacbcfb2d4e6b96d7525da900017e01
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253552"
---
# <a name="srv_paramset-extended-stored-procedure-api"></a>srv_paramset (API de procédure stockée étendue)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Utilisez plutôt l’intégration du CLR.  
  
 Définit la valeur d'un paramètre de retour d'appel de procédure stockée distante. Cette fonction a été remplacée par la fonction **srv_paramsetoutput**.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
int srv_paramset (  
SRV_PROC *  
srvproc  
,  
int  
n  
,   
void *  
data  
,  
int  
len   
);  
```  
  
## <a name="arguments"></a>Arguments  
 *srvproc*  
 Pointeur vers la structure SRV_PROC qui correspond au handle d'une connexion cliente particulière (dans ce cas, le handle qui a reçu l'appel de procédure stockée distante). La structure contient des informations que la bibliothèque d'API de procédure stockée étendue utilise pour gérer les communications et les données entre l'application et le client.  
  
 *n*  
 Indique le numéro du paramètre à définir. Le premier paramètre est 1.  
  
 *métadonnée*  
 Pointeur vers la valeur de données à renvoyer au client en tant que paramètre de retour de procédure stockée distante.  
  
 *Len*  
 Spécifie la longueur réelle des données à retourner. Si le type de données du paramètre est de longueur constante et qu’il n’autorise pas les valeurs NULL (par exemple, *srvbit* ou *srvint1*), *len* est ignoré.  
  
## <a name="returns"></a>Returns  
 SUCCEED si la valeur de paramètre a été correctement définie ; sinon, FAIL. FAIL est retourné quand il n’y a pas de procédure stockée distante en cours, quand il n’y a aucun *n*ième paramètre de procédure stockée distante, quand le paramètre n’est pas un paramètre de retour et quand l’argument *len* n’est pas légal.  
  
 Si *len* a pour valeur 0, il retourne NULL. Pour retourner la valeur NULL au client, la seule façon est d’attribuer la valeur 0 à *len*.  
  
 Cette fonction retourne les valeurs suivantes, si le paramètre est l’un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] des types de données.  
  
|Nouveaux types de données|Longueur de données de retour|  
|--------------------|------------------------|  
|**BITN**|**Null :** _Len_ = 0, Data = GI, RET = 0<br /><br /> **Zéro :** NON APPLICABLE<br /><br /> **>= 255 :** NON APPLICABLE<br /><br /> **<255 :** NON APPLICABLE|  
|**BIGVARCHAR**|**Null :** _Len_ = 0, Data = GI, RET = 1<br /><br /> **Zero :** _Len_ = GI, Data = GI, RET = 0<br /><br /> **>= 255 :** _Len_ = max8k, Data = valide, RET = 0<br /><br /> **<255 :** _Len_ = <8 Ko, Data = valide, RET = 1|  
|**BIGCHAR**|**Null :** _Len_ = 0, Data = GI, RET = 1<br /><br /> **Zero :** _Len_ = GI, Data = GI, RET = 0<br /><br /> **>= 255 :** _Len_ = max8k, Data = valide, RET = 0<br /><br /> **<255 :** _Len_ = <8 Ko, Data = valide, RET = 1|  
|**BIGBINARY**|**Null :** _Len_ = 0, Data = GI, RET = 1<br /><br /> **Zero :** _Len_ = GI, Data = GI, RET = 0<br /><br /> **>= 255 :** _Len_ = max8k, Data = valide, RET = 0<br /><br /> **<255 :** _Len_ = <8 Ko, Data = valide, RET = 1|  
|**BIGVARBINARY**|**Null :** _Len_ = 0, Data = GI, RET = 1<br /><br /> **Zero :** _Len_ = GI, Data = GI, RET = 0<br /><br /> **>= 255 :** _Len_ = max8k, Data = valide, RET = 0<br /><br /> **<255 :** _Len_ = <8 Ko, Data = valide, RET = 1|  
|NCHAR|**Null :** _Len_ = 0, Data = GI, RET = 1<br /><br /> **Zero :** _Len_ = GI, Data = GI, RET = 0<br /><br /> **>= 255 :** _Len_ = max8k, Data = valide, RET = 0<br /><br /> **<255 :** _Len_ = <8 Ko, Data = valide, RET = 1|  
|NVARCHAR|**Null :** _Len_ = 0, Data = GI, RET = 1<br /><br /> **Zero :** _Len_ = GI, Data = GI, RET = 0<br /><br /> **>= 255 :** _Len_ = max8k, Data = valide, RET = 0<br /><br /> **<255 :** _Len_ = <8 Ko, Data = valide, RET = 1|  
|**Text**|**Null :** _Len_ = IG, données = IG, RET = 0<br /><br /> **Zero :** _Len_ = GI, Data = GI, RET = 0<br /><br /> **>= 255 :** _Len_ = IG, données = IG, RET = 0<br /><br /> 255 : _Len_ = IG, données = IG, RET = 0 ** \<**|  
|RET = Valeur de retour de srv_paramset.||  
|IG = La valeur sera ignorée.||  
|valide = Tout pointeur valide vers des données.||  
  
## <a name="remarks"></a>Remarques  
 Les paramètres contiennent les données passées entre les clients et l'application avec des procédures stockées distantes. Le client peut spécifier certains paramètres en tant que paramètres de retour. Ces paramètres de retour peuvent contenir des valeurs que l'application serveur ODS (Open Data Services) repasse au client. L'utilisation de paramètres de retour est analogue au passage de paramètres par référence.  
  
 Vous ne pouvez pas définir la valeur de retour pour un paramètre qui n'a pas été appelé en tant que paramètre de retour. Vous pouvez utiliser **srv_paramstatus** pour déterminer comment le paramètre a été appelé.  
  
 Cette fonction définit la valeur de retour pour un paramètre, mais n'envoie pas vraiment la valeur de retour au client. Tous les paramètres de retour, que leurs valeurs de retour aient été définies avec **srv_paramset** ou non, sont automatiquement envoyés au client quand **srv_senddone** est appelé avec l’indicateur d’état défini avec la valeur SRV_DONE_FINAL.  
  
 Quand un appel de procédure stockée distante est effectué avec des paramètres, ceux-ci peuvent être passés par nom ou par position (sans nom). Si l'appel de procédure stockée distante est effectué avec certains paramètres passés par nom et certains passés par position, une erreur se produit. Le gestionnaire de SRV_RPC est toujours appelé, mais il apparaît comme s’il n’y avait aucun paramètre, et **srv_rpcparams** retourne 0.  
  
> [!IMPORTANT]  
>  Il est préférable d'examiner avec soin le code source des procédures stockées étendues et de tester les DLL compilées avant de les installer sur un serveur de production. Pour plus d'informations sur l'examen et les tests de sécurité, consultez ce [site Web de Microsoft](https://www.microsoft.com/msrc?rtc=1).  
  
## <a name="see-also"></a>Voir aussi  
 [srv_paramsetoutput &#40;API de procédure stockée étendue&#41;](../../relational-databases/extended-stored-procedures-reference/srv-paramsetoutput-extended-stored-procedure-api.md)  
  
  
