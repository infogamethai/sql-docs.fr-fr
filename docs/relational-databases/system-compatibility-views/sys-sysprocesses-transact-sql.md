---
title: sys. sysprocesses (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysprocesses_TSQL
- sys.sysprocesses_TSQL
- sys.sysprocesses
- sysprocesses
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysprocesses compatibility view
- sysprocesses system table
ms.assetid: 60a36d36-54b3-4bd6-9cac-702205a21b16
author: rothja
ms.author: jroth
ms.openlocfilehash: d9da0f09c2506e0d596a485aee112f9f188b6d12
ms.sourcegitcommit: ef830f565ee07dc7d4388925cc3c86c5d2cfb4c7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2019
ms.locfileid: "74947151"
---
# <a name="syssysprocesses-transact-sql"></a>sys.sysprocesses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contient des informations sur les processus en cours d'exécution sur une instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il peut s'agir de processus client ou système. Pour accéder à sysprocesses, vous devez vous trouver dans le contexte de base de données master ou utiliser le nom en trois parties master.dbo.sysprocesses.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|spid|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ID de session.|  
|kpid|**smallint**|ID de thread Windows.|  
|blocked|**smallint**|ID de la session qui bloque la demande. Si cette colonne est NULL, la demande n'est pas bloquée, ou les informations de session de la session bloquant la demande ne sont pas disponibles (ou ne peuvent pas être identifiées).<br /><br /> -2 = La ressource qui bloque la demande appartient à une transaction distribuée orpheline.<br /><br /> -3 = La ressource qui bloque la demande appartient à une transaction de récupération différée.<br /><br /> -4 = L'ID de session du propriétaire du verrou qui bloque la demande n'a pas pu être déterminé en raison de transitions d'état de verrou interne.|  
|waittype|**binaire (2)**|Réservé.|  
|waittime|**bigint**|Temps d'attente total (en millisecondes).<br /><br /> 0 = Le processus n'est pas en attente.|  
|lastwaittype|**nchar (32)**|Chaîne indiquant le nom du dernier type d'attente ou celui du type d'attente actuel.|  
|waitresource|**nchar (256)**|Description textuelle d'une ressource de verrouillage.|  
|dbid|**smallint**|ID de la base de données actuellement utilisée par le processus.|  
|uid|**smallint**|ID de l'utilisateur qui a exécuté la commande. Déborde ou retourne la valeur NULL si le nombre d'utilisateurs et de rôles dépasse 32 767.|  
|cpu|**tiers**|Temps UC cumulé pour l'exécution du processus. L'entrée est mise à jour pour tous les processus, indépendamment de la valeur de l'option SET STATISTICS TIME (ON ou OFF).|  
|physical_io|**bigint**|Nombre total d'opérations d'écriture et de lecture sur disque pour le processus.|  
|memusage|**tiers**|Nombre de pages du cache de procédures actuellement allouées à ce processus. Un nombre négatif indique que le processus libère de la mémoire allouée par un autre processus.|  
|login_time|**Date/heure**|Heure à laquelle le processus client s'est connecté au serveur.|  
|last_batch|**Date/heure**|Dernière exécution par un processus client d'un appel de procédure stockée distante ou d'une instruction EXECUTE.|  
|ecid|**smallint**|ID du contexte d'exécution utilisé pour identifier de façon unique les sous-threads exécutés pour le compte d'un seul et même processus.|  
|open_tran|**smallint**|Nombre de transactions en cours pour le processus.|  
|status|**nchar (30)**|État de l'ID processus. Les valeurs possibles sont les suivantes :<br /><br /> **dormant** réinitialisation de la session. =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **Running** = la session exécute un ou plusieurs lots. Lorsque la fonctionnalité MARS (Multiple Active Result Sets) est activée, une session peut exécuter plusieurs traitements. Pour plus d’informations, consultez [Utilisation de MARS &#40;Multiple Active Result Sets&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).<br /><br /> **Background** = la session exécute une tâche en arrière-plan, telle qu’une détection de blocage.<br /><br /> **Rollback** = la session a une restauration de transaction en cours.<br /><br /> **Pending** = la session attend qu’un thread de travail soit disponible.<br /><br /> **Runnable** = la tâche de la session est dans la file d’attente exécutable d’un planificateur en attendant d’obtenir un quantum de temps.<br /><br /> **Spinloop** = la tâche de la session attend qu’un SpinLock soit libéré.<br /><br /> **Suspended** = la session attend la fin d’un événement, tel que des e/s.|  
|sid|**binaire (86)**|GUID (Globally Unique Identifier) de l'utilisateur.|  
|hostname|**nchar (128)**|Nom de la station de travail.|  
|program_name|**nchar (128)**|Nom du logiciel d'application.|  
|hostprocess|**nchar (10)**|Numéro d'identification du processus de la station de travail.|  
|cmd|**nchar (26)**|Commande en cours d’exécution.|  
|nt_domain|**nchar (128)**|Domaine Windows du client (s'il utilise l'authentification Windows) ou d'une connexion approuvée.|  
|nt_username|**nchar (128)**|Nom d'utilisateur Windows pour le processus (s'il utilise l'authentification Windows) ou une connexion approuvée.|  
|net_address|**nchar (12)**|Identificateur unique affecté à la carte réseau de la station de travail de chaque utilisateur. Lorsqu'un utilisateur se connecte, cet identificateur est inséré dans la colonne net_address.|  
|net_library|**nchar (12)**|Colonne dans laquelle est enregistrée la bibliothèque réseau du client. Chaque processus client arrive sur une connexion réseau. Les connexions réseau ont une bibliothèque réseau associée qui leur permet de se connecter.|  
|loginame|**nchar (128)**|Nom de connexion.|  
|context_info|**binaire (128)**|Données stockées dans un lot à l'aide de l'instruction SET CONTEXT_INFO.|  
|sql_handle|**binaire (20)**|Représente le lot ou l'objet en cours d'exécution.<br /><br /> **Remarque** Cette valeur est dérivée de l’adresse du lot ou de la mémoire de l’objet. Cette valeur n'est pas calculée à l'aide de l'algorithme de hachage de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|stmt_start|**tiers**|Décalage de début de l'instruction SQL en cours pour la colonne sql_handle spécifiée.|  
|stmt_end|**tiers**|Décalage de fin de l'instruction SQL actuelle pour la colonne sql_handle spécifiée.<br /><br /> -1 = L'instruction en cours s'exécute jusqu'à la fin des résultats renvoyés par la fonction fn_get_sql pour la colonne sql_handle spécifiée.|  
|request_id|**tiers**|ID de la demande. Utilisé pour identifier les requêtes qui s'exécutent dans une session spécifique.|
|page_resource |**Binary(8** |**S’applique à**:[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br /><br /> Représentation hexadécimale sur 8 octets de la ressource de page si `waitresource` la colonne contient une page. |  
  
## <a name="remarks"></a>Remarques  
 Si un utilisateur dispose de l'autorisation VIEW SERVER STATE sur le serveur, il voit toutes les sessions en cours d'exécution dans l'instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; sinon, il ne voit que la session actuelle.  
  
## <a name="see-also"></a>Voir aussi  
 [Fonctions et vues de gestion dynamique liées à l’exécution &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Mappage de tables système à des vues système &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vues de compatibilité &#40;&#41;Transact-SQL](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
