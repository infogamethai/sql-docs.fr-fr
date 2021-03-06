---
title: Préparer les données de Trace d’entrée | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: c14fd3d2-5770-47c2-a851-cc13ddbc9bf5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7af5d166ec3bc059bc2628512564d92fd4cc6cad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149993"
---
# <a name="prepare-the-input-trace-data"></a>Préparer les données de trace d'entrée
  Avant de pouvoir démarrer une relecture distribuée avec la fonctionnalité [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributed Replay, vous devez préparer les données de trace d'entrée en initialisant l'étape de prétraitement de l'outil d'administration de relecture distribuée. Dans l'étape de prétraitement, Distributed Replay Controller traite les données de trace et génère un fichier intermédiaire :  
  
 ![Étape de prétraitement Distributed replay](../../database-engine/media/preprocess.gif "étape de prétraitement Distributed replay")  
  
 Pour plus d'informations sur l'étape de prétraitement, consultez [SQL Server Distributed Replay](sql-server-distributed-replay.md).  
  
> [!NOTE]  
>  Les données de trace d'entrée doivent être capturées dans une version de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatible avec Distributed Replay. Les données de trace d'entrée doivent également être compatibles avec le serveur cible sur lequel vous souhaitez relire les données de trace. Pour plus d'informations sur les conditions requises en matière de version, consultez [Distributed Replay Requirements](distributed-replay-requirements.md).  
  
### <a name="to-prepare-the-input-trace-data"></a>Pour préparer les données de trace d'entrée  
  
1.  **(Facultatif) Modifier les paramètres de configuration de prétraitement**: Si vous souhaitez modifier les paramètres de configuration de prétraitement, tels que s’il faut filtrer les sessions système ou configurer la durée d’inactivité maximale, vous devez modifier le `<PreprocessModifiers>` élément du fichier de configuration de prétraitement XML, `DReplay.exe.preprocess.config`. Si vous modifiez le fichier de configuration de prétraitement, nous vous recommandons de modifier une copie plutôt que l'original. Pour modifier des paramètres, suivez la procédure suivante :  
  
    1.  Faites une copie du fichier par défaut de configuration de prétraitement, `DReplay.exe.preprocess.config`, et renommez le nouveau fichier. Le fichier par défaut de configuration de prétraitement se trouve dans le dossier d'installation de l'outil d'administration.  
  
    2.  Modifiez les paramètres de configuration de prétraitement dans le nouveau fichier de configuration.  
  
    3.  Quand vous initialisez l’étape de prétraitement (étape suivante), utilisez le paramètre *config_file* de l’option **preprocess** pour spécifier l’emplacement du fichier de configuration modifié.  
  
     Pour plus d'informations sur le fichier de configuration de prétraitement, consultez [Configurer Distributed Replay](configure-distributed-replay.md).  
  
2.  **Initialiser l’étape de prétraitement**: Pour préparer les données de trace d’entrée, vous devez exécuter l’outil d’administration avec le **prétraiter** option. Pour plus d’informations, consultez [Option preprocess &#40;outil d’administration Distributed Replay&#41;](preprocess-option-distributed-replay-administration-tool.md).  
  
    1.  Ouvrez l'utilitaire d'invite de commandes Windows (`CMD.exe`) et accédez à l'emplacement d'installation de l'outil d'administration Distributed Replay (`DReplay.exe`).  
  
    2.  (Facultatif) Utilisez le paramètre *controller* , **-m**, pour spécifier le contrôleur, si le service du contrôleur s’exécute sur un ordinateur différent de l’outil d’administration.  
  
    3.  Utilisez le paramètre *input_trace_file* , **-i**, pour spécifier l’emplacement et le nom des fichiers de trace d’entrée.  
  
    4.  Utilisez le paramètre *controller_working_directory* , **-d**, pour spécifier l’emplacement où le fichier intermédiaire doit être enregistré sur le contrôleur.  
  
    5.  (Facultatif) Utilisez le paramètre *config_file* , **-c**, pour spécifier l’emplacement du fichier de configuration de prétraitement. Utilisez ce paramètre pour pointer sur le nouveau fichier de configuration, si vous avez modifié une copie du fichier de configuration de prétraitement par défaut.  
  
    6.  (Facultatif) Utilisez le paramètre *status_interval* , **-f**, pour spécifier si vous voulez que l’outil d’administration affiche des messages d’état à une fréquence autre que 30 secondes.  
  
     Par exemple, l’initialisation de l’étape de prétraitement sur le même ordinateur que le service contrôleur, pour un fichier de trace situé dans `c:\trace1.trc`, un répertoire de travail du contrôleur situé dans `c:\WorkingDir` et un message d’état affiché selon la valeur par défaut de 30 secondes, requiert la syntaxe : `dreplay preprocess -i c:\trace1.trc -d c:\WorkingDir`  
  
3.  Une fois l'étape de prétraitement terminée, le fichier intermédiaire est stocké dans le répertoire de travail du contrôleur. Pour initialiser l’étape de relecture d’événements, vous devez exécuter l’outil d’administration avec l’option **replay** . Pour plus d’informations, consultez [Relire les données de trace](replay-trace-data.md).  
  
## <a name="see-also"></a>Voir aussi  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Distributed Replay Requirements](distributed-replay-requirements.md)   
 [Options de ligne de commande de l’outil d’administration &#40;Distributed Replay Utility&#41;](administration-tool-command-line-options-distributed-replay-utility.md)   
 [Configure Distributed Replay](configure-distributed-replay.md)  
  
  
