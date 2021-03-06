---
title: sp_add_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 06dbee74cfb3e2d5e697ea9594d46c98557de8ef
ms.sourcegitcommit: df1f71231f8edbdfe76e8851acf653c25449075e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70810497"
---
# <a name="sp_add_jobschedule-transact-sql"></a>sp_add_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Crée une planification pour un travail de l’agent SQL.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  > [!IMPORTANT]  
  > Dans [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la plupart des fonctionnalités SQL Server Agent sont prises en charge. Pour plus d’informations, consultez [Différences T-SQL entre Azure SQL Database Managed Instance et SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_add_jobschedule [ @job_id = ] job_id, | [ @job_name = ] 'job_name', [ @name = ] 'name'  
     [ , [ @enabled = ] enabled_flag ]  
     [ , [ @freq_type = ] frequency_type ]  
     [ , [ @freq_interval = ] frequency_interval ]  
     [ , [ @freq_subday_type = ] frequency_subday_type ]  
     [ , [ @freq_subday_interval = ] frequency_subday_interval ]  
     [ , [ @freq_relative_interval = ] frequency_relative_interval ]  
     [ , [ @freq_recurrence_factor = ] frequency_recurrence_factor ]  
     [ , [ @active_start_date = ] active_start_date ]  
     [ , [ @active_end_date = ] active_end_date ]  
     [ , [ @active_start_time = ] active_start_time ]  
     [ , [ @active_end_time = ] active_end_time ]  
     [ , [ @schedule_id = ] schedule_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Arguments  
`[ @job_id = ] job_id` numéro d’identification du travail auquel la planification est ajoutée. *job_id* est de type **uniqueidentifier**, sans valeur par défaut.  
  
`[ @job_name = ] 'job_name'` nom du travail auquel la planification est ajoutée. *job_name* est de type **nvarchar (128)** , sans valeur par défaut.  
  
> [!NOTE]  
>  *Job_id* ou *job_name* doivent être spécifiés, mais ne peuvent pas être spécifiés.  
  
`[ @name = ] 'name'` nom de la planification. *Name* est de type **nvarchar (128)** , sans valeur par défaut.  
  
`[ @enabled = ] enabled_flag` indique l’état actuel de la planification. *enabled_flag* est de **type tinyint**, avec **1** comme valeur par défaut (activé). Si la **valeur est 0**, la planification n’est pas activée. Lorsque la planification n'est pas activée, le travail n'est pas exécuté.  
  
`[ @freq_type = ] frequency_type` valeur qui indique quand le travail doit être exécuté. *frequency_type* est de **type int**, avec **0**comme valeur par défaut et peut prendre l’une des valeurs suivantes :  
  
|Valeur|Description|  
|-----------|-----------------|  
|**1**|Une fois|  
|**4**|Tous les jours|  
|**8**|Semaine|  
|**16**|Mois|  
|**32**|Mensuellement, par rapport à *frequency_interval.*|  
|**64**|Lancer lorsque le service de l'Agent [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] démarre.|  
|**128**|Lancer lorsque l'ordinateur est inactif.|  
  
`[ @freq_interval = ] frequency_interval` jour d’exécution du travail. *frequency_interval* est de **type int**, avec 0 comme valeur par défaut, et dépend de la valeur de *frequency_type* , comme indiqué dans le tableau suivant :  
  
|Valeur|Effet|  
|-----------|------------|  
|**1** (une fois)|*frequency_interval* n’est pas utilisé.|  
|**4** (tous les jours)|Tous les *frequency_interval* jours.|  
|**8** (hebdomadaire)|*frequency_interval* est une ou plusieurs des valeurs suivantes (combinées avec un opérateur logique or) :<br /><br /> 1 = Dimanche<br /><br /> 2 = Lundi<br /><br /> 4 = mardi<br /><br /> 8 = mercredi<br /><br /> 16 = jeudi<br /><br /> 32 = vendredi<br /><br /> 64 = samedi|  
|**16** (mensuellement)|Le *frequency_interval* jour du mois.|  
|**32** (par rapport à chaque mois)|*frequency_interval* est l’un des éléments suivants :<br /><br /> 1 = Dimanche<br /><br /> 2 = Lundi<br /><br /> 3 = Mardi<br /><br /> 4 = Mercredi<br /><br /> 5 = Jeudi<br /><br /> 6 = Vendredi<br /><br /> 7 = Samedi<br /><br /> 8 = Jour<br /><br /> 9 = Jour de semaine<br /><br /> 10 = Jour de week-end|  
|**64** (au démarrage du service de l’agent [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])|*frequency_interval* n’est pas utilisé.|  
|**128**|*frequency_interval* n’est pas utilisé.|  
  
`[ @freq_subday_type = ] frequency_subday_type` spécifie les unités de *frequency_subday_interval*. *frequency_subday_type* est de **type int**, sans valeur par défaut, et peut prendre l’une des valeurs suivantes :  
  
|Valeur|Description (unité)|  
|-----------|--------------------------|  
|**0x1**|À une heure spécifiée|  
|**0x4**|Minutes|  
|**0x8**|Heures|  
  
`[ @freq_subday_interval = ] frequency_subday_interval` nombre d' *frequency_subday_type* périodes entre chaque exécution du travail. *frequency_subday_interval* est de **type int**, avec 0 comme valeur par défaut.  
  
`[ @freq_relative_interval = ] frequency_relative_interval` définit plus en détail le *frequency_interval* lorsque *frequency_type* est défini sur **32** (mensuel relatif).  
  
 *frequency_relative_interval* est de **type int**, sans valeur par défaut, et peut prendre l’une des valeurs suivantes :  
  
|Valeur|Description (unité)|  
|-----------|--------------------------|  
|**1**|Première|  
|**2**|Seconde|  
|**4**|Troisième|  
|**8**|Quatrième|  
|**16**|Dernière|  
  
 *frequency_relative_interval* indique l’occurrence de l’intervalle. Par exemple, si *frequency_relative_interval* a la valeur **2**, *frequency_type* a la valeur **32**et *frequency_interval* la valeur **3**, la tâche planifiée se produit le deuxième mardi de chaque mois.  
  
`[ @freq_recurrence_factor = ] frequency_recurrence_factor` nombre de semaines ou de mois entre l’exécution planifiée du travail. *frequency_recurrence_factor* est utilisé uniquement si *frequency_type* a la valeur **8**, **16**ou **32**. *frequency_recurrence_factor* est de **type int**, avec 0 comme valeur par défaut.  
  
`[ @active_start_date = ] active_start_date` date à laquelle l’exécution du travail peut commencer. *active_start_date* est de **type int**, sans valeur par défaut. La date est au format AAAAMMJJ. Si *active_start_date* est défini, la date doit être supérieure ou égale à 19900101.  
  
 Après avoir créé la planification, examinez la date de début et assurez-vous qu'elle est correcte. Pour plus d’informations, consultez la section « planification de la date de début » dans [créer et attacher des planifications à des travaux](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
`[ @active_end_date = ] active_end_date` date à laquelle l’exécution du travail peut être arrêtée. *active_end_date* est de **type int**, sans valeur par défaut. La date est au format AAAAMMJJ.  
  
`[ @active_start_time = ] active_start_time` heure de chaque jour entre *active_start_date* et *active_end_date* pour commencer l’exécution du travail. *active_start_time* est de **type int**, sans valeur par défaut. L'heure est au format HHMMSS et est exprimée sur 24 heures.  
  
`[ @active_end_time = active_end_time_` heure de chaque jour entre *active_start_date* et *active_end_date* pour terminer l’exécution du travail. *active_end_time* est de **type int**, sans valeur par défaut. L'heure est au format HHMMSS et est exprimée sur 24 heures.  
  
`[ @schedule_id = schedule_idOUTPUT` numéro d’identification de planification affecté à la planification si elle est correctement créée. *schedule_id* est une variable de sortie de type **int**, sans valeur par défaut.  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT` un identificateur unique pour la planification. *schedule_uid* est une variable de type **uniqueidentifier**.  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 0 (réussite) ou 1 (échec)  
  
## <a name="result-sets"></a>Jeux de résultats  
 Aucun  
  
## <a name="remarks"></a>Notes  
 Il est désormais possible de gérer la planification des travaux indépendamment des travaux. Pour ajouter une planification à un travail, utilisez **sp_add_schedule** pour créer la planification et **sp_attach_schedule** pour joindre la planification à un travail.  
  
## <a name="permissions"></a>Autorisations  
 Par défaut, les membres du rôle serveur fixe **sysadmin** peuvent exécuter cette procédure stockée. Les autres utilisateurs doivent disposer de l'un des rôles de base de données fixes suivants de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent dans la base de données **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Pour en savoir plus sur les autorisations de ces rôles, consultez [Rôles de base de données fixes de SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
 
 ## <a name="example"></a>Exemple
 L’exemple suivant affecte une planification de travail à `SaturdayReports` qui est exécutée tous les samedis à 2:00.
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>Voir aussi  
 [Créer et attacher des planifications à des travaux](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [Planifier un travail](../../ssms/agent/schedule-a-job.md)   
 [Créer une planification](../../ssms/agent/create-a-schedule.md)   
 [Procédures &#40;stockées SQL Server Agent Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
