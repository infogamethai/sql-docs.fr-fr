---
title: Configurations matérielle et logicielle requises pour l’installation de SQL Server | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Setup [SQL Server], software
- software [SQL Server]
- installing SQL Server, software
- operating systems [SQL Server], SQL Server requirements
- Setup [SQL Server], cross-language support
- operating systems [SQL Server], cross-language support
- network connections [SQL Server], requirements
- disk space [SQL Server], SQL Server installations
- WOW [SQL Server]
- Setup [SQL Server], hardware
- dependencies [SQL Server], SQL Server installations
- cluster hardware requirements [SQL Server]
- endpoints [SQL Server], SQL Server installations
- Internet [SQL Server], SQL Server installations
- hardware [SQL Server]
- Windows on Windows [SQL Server]
- installing SQL Server, hardware
- Setup Configuration Checker
- SCC [SQL Server]
- operating systems [SQL Server]
- space [SQL Server], SQL Server installations
- system configuration checker
- installing SQL Server, cross-language support
- Internet [SQL Server]
- space [SQL Server]
- extended system support [SQL Server]
- 64-bit edition [SQL Server]
- failover clustering [SQL Server]
- failover clustering [SQL Server], hardware requirements
- 32-bit edition [SQL Server]
- locales [SQL Server], SQL Server installations
- cross-language support
- disk space [SQL Server]
- localized SQL Server versions
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 88ed55a3c2890864e3e9623f3fa53ca3e747350c
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536185"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>Configurations matérielle et logicielle requises pour l’installation de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Cet article liste les configurations matérielle et logicielle minimales pour installer et exécuter [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] sur le système d’exploitation Windows.

[!INCLUDE[sscurrent](../../includes/sssqlv14-md.md)] prend en charge [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] sur Linux. Pour obtenir des informations, consultez [Configurations matérielle et logicielle requises pour [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sur Linux](../../linux/sql-server-linux-setup.md#system). 

**Essayez :**  
  
- Téléchargez SQL Server à partir du [**Centre d’évaluation**.](https://www.microsoft.com/evalcenter/evaluate-sql-server-2019-rc) 
  
<!-- 
- Spin up a Virtual Machine with [**SQL Server 2017**](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) already installed.  
-->
  
**Les remarques suivantes s’appliquent à toutes les éditions :**  
  
- Le programme d'installation de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloquera les installations sur les lecteurs en lecture seule, mappés ou compressés.  
  
- L’installation échoue si vous lancez le programme d’installation par le biais d’une connexion Bureau à distance en utilisant un support sur une ressource locale du client Connexion Bureau à distance. Pour effectuer une installation à distance, le support doit se trouver sur un partage réseau ou être installé en local sur l’ordinateur physique ou la machine virtuelle. Le support d’installation de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] peut soit se trouver sur un partage réseau, sur un lecteur mappé ou sur un lecteur local, soit être présenté à une machine virtuelle sous la forme d’un fichier ISO.
- Le programme d'installation de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installe les composants logiciels suivants requis par le produit :  
  
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    - Fichiers de support du programme d’installation de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  

##  <a name="hwswr"></a> Configurations matérielle et logicielle requises  
La configuration requise suivante s’applique à toutes les installations :  
  
|Composant|Condition requise|  
|---------------|-----------------|  
|Système d’exploitation|Windows 10 TH1 1507 ou ultérieur<br/><br>Windows Server 2016 ou ultérieur<br/><br/>
|.NET Framework|Les systèmes d’exploitation minimaux incluent la version minimale du .NET Framework.|  
|Logiciel réseau|Les systèmes d'exploitation pris en charge pour [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] possèdent un logiciel réseau intégré. Les instances par défaut et les instances nommées d’une installation autonome prennent en charge les protocoles réseau suivants : Mémoire partagée, canaux nommés et TCP/IP.<br/><br/> |  
|Disque dur|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] requiert un minimum de 6 GO d'espace disque disponible.<br/><br/> L'espace disque nécessaire varie selon les composants [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] que vous installez. Pour plus d’informations, consultez [Espace disque nécessaire](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) plus loin dans cet article. Pour plus d'informations sur les types de stockage pris en charge pour les fichiers de données, consultez [Storage Types for Data Files](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes).|  
|Moniteur|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] requiert un moniteur avec une résolution Super-VGA (800 x 600) ou supérieure.|  
|Internet|Les fonctionnalités Internet requièrent un accès à Internet (des frais peuvent s'appliquer).|  

> [!NOTE]
> L'exécution de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] sur un ordinateur virtuel est plus lente que le fonctionnement en mode natif en raison de la surcharge de la virtualisation.  

> [!IMPORTANT]
> La fonctionnalité PolyBase comporte d’autres exigences matérielles et logicielles. Pour plus d’informations, consultez [Prise en main de PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
##  <a name="pmosr"></a> Processeur, mémoire et système d’exploitation requis  
 Les spécifications de mémoire et de processeur suivantes s'appliquent à toutes les éditions de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]:  
  
|Composant|Condition requise|  
|---------------|-----------------|  
|Mémoire \*|**Minimum :**<br/><br/> Éditions Express : 512 MO<br/><br/> Toutes les autres éditions : 1 Go<br/><br/> **Recommandé :**<br/><br/> Éditions Express : 1 Go<br/><br/> Toutes les autres éditions : au moins 4 GO, qui doivent être augmentés au fur et à mesure de l’augmentation de la taille de la base de données pour garantir des performances optimales.|  
|Vitesse du processeur|**Minimum :** processeur x64, 1,4 GHz<br/><br/> **Recommandé :** 2.0 GHz ou plus rapide|  
|Type de processeur|Processeur x64 : AMD Opteron, AMD Athlon 64, Intel Xeon avec prise en charge d’Intel EM64T, Intel Pentium IV avec prise en charge d’EM64T|  
  
> [!NOTE]  
> L’installation de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] est prise en charge uniquement sur les processeurs x64. Elle n’est plus prise en charge sur les processeurs x86.  
  
 \* La mémoire minimale pour installer le composant [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] dans [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) est de 2 Go de RAM, ce qui est différent de la mémoire minimale exigée pour [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]. Pour obtenir des informations sur l'installation de DQS, consultez [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  

**Prise en charge de Server Core :**

L’installation de SQL Server 2019 en mode Server Core est prise en charge par les éditions suivantes de Windows Server :

|                              |
| :------------------------  |
| Windows Server 2019 Core | 
| Windows Server 2016 Core |
| &nbsp; | 

Pour plus d’informations sur l’installation de SQL Server en mode Server Core, consultez [Installer SQL Server sur Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  

###  <a name="TOP_Principal"></a> Compatibilité de système d’exploitation   

Le tableau suivant indique les éditions de SQL Server 2019 qui sont compatibles avec les différentes versions de Windows :  
  

| Édition de SQL Server :               | Enterprise | Développeur | Standard | Web | Express |  
| :------------------------       | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    Oui     |    Oui    |    Oui   | Oui |   Oui   |
| Windows Server 2019 Standard      |    Oui     |    Oui    |    Oui   | Oui |   Oui   |
| Windows Server 2019 Essentials    |    Oui     |    Oui    |    Oui   | Oui |   Oui   |
| Windows Server 2016 Datacenter    |    Oui     |    Oui    |    Oui   | Oui |   Oui   |
| Windows Server 2016 Standard      |    Oui     |    Oui    |    Oui   | Oui |   Oui   |
| Windows Server 2016 Essentials    |    Oui     |    Oui    |    Oui   | Oui |   Oui   |
| &nbsp; | &nbsp; |


##  <a name="CrossLanguageSupport"></a> Prise en charge de langues différentes  
 Pour plus d’informations sur la prise en charge de plusieurs langues et sur les considérations relatives à l’installation de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dans les langues localisées, consultez [Versions linguistiques locales dans SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md)  
  
##  <a name="HardDiskSpace"></a> Espace disque nécessaire  
 Pendant l'installation de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)], Windows Installer crée des fichiers temporaires sur le lecteur système. Avant d'exécuter le programme d'installation ou de mise à niveau de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vérifiez que vous disposez d'au moins 6,0 Go d'espace disponible sur le lecteur système pour ces fichiers. Cette configuration requise s'applique même lorsque vous installez tous les composants [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sur un lecteur différent du lecteur par défaut.  
  
 L'espace disque nécessaire peut varier selon la configuration du système et les fonctionnalités installées. Le tableau suivant présente l'espace disque nécessaire pour les composants [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] .  
  
|**Fonctionnalité**|**Espace disque nécessaire**|  
|-----------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] et fichiers de données, réplication, recherche en texte intégral et Data Quality Services|1 480 Mo|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (dans la configuration ci-dessus) avec R Services (dans la base de données)|2 744 Mo|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (dans la configuration ci-dessus) avec service de requête PolyBase pour données externes|4 194 Mo|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] et fichiers de données|698 Mo|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967 Mo|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] (Autonome)|280 Mo|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|1 203 Mo|  
|Complément[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Add-in for SharePoint Products|325 Mo|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121 Mo|  
|Connectivité des outils clients|328 Mo|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306 Mo|  
|Composants clients (autres que la documentation en ligne de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] et les outils Integration Services)|445 Mo|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280 Mo|  
|Composants de la documentation en ligne[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pour afficher et gérer le contenu d’aide*|27 Mo|  
|Toutes les fonctionnalités|8 030 Mo|  
  
 *L’espace disque requis pour le contenu de la documentation en ligne téléchargé est de 200 Mo.  
  
##  <a name="StorageTypes"></a> Types de stockage pour les fichiers de données  
 Les types de stockage pris en charge pour les fichiers de données sont :  
  
- Disque local 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prend actuellement en charge les lecteurs de disque dont les tailles de secteur natif standard s’élève à 512 octets et 4 Ko.  Les disques durs dont les tailles de secteur est supérieure à 4 Ko peuvent provoquer des erreurs quand vous essayez d’y stocker des fichiers de données [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Consultez [Limites des tailles de secteur de disque dur prises en charge dans SQL Server](https://support.microsoft.com/kb/926930) pour plus d’informations sur la prise en charge des tailles de secteur de disque dur dans [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
    - L'installation du cluster de basculement[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prend en charge uniquement le disque local pour l'installation des fichiers tempdb. Assurez-vous que le chemin d'accès spécifié pour les données tempdb et les fichiers journaux sont valides sur tous les nœuds du cluster. Pendant le basculement, si les répertoires tempdb ne sont pas disponibles sur le nœud de basculement cible, la ressource [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ne sera pas en ligne.
- Stockage partagé  
- [Espaces de stockage direct \(S2D\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)  
- Partage de fichiers SMB  
    - Le stockage de fichiers SMB n'est pas pris en charge pour les fichiers de données d' [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pour les installations autonomes ou en clusters. Utilisez un stockage attaché direct, un réseau de zone de stockage ou des espaces de stockage direct (S2D) à la place. 
    - Le stockage SMB peut être hébergé par un serveur de fichiers Windows ou un dispositif de stockage SMB tiers. Si vous utilisez un serveur de fichiers Windows, il doit s'agir de la version 2008 ou ultérieure. Pour plus d'informations sur l'installation de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en utilisant le partage de fichiers SMB comme option de stockage, consultez [Installer SQL Server avec le partage de fichiers SMB en tant qu'option de stockage](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
  
  
##  <a name="DC_support"></a> Installation de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sur un contrôleur de domaine  
 Pour des raisons de sécurité, nous recommandons de ne pas installer [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] sur un contrôleur de domaine. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ne bloquera pas l'installation sur un ordinateur qui est contrôleur de domaine, mais les limitations suivantes s'appliquent :  
  
- Vous ne pouvez pas exécuter les services [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sur un contrôleur de domaine sous un compte de service local.    
- Après avoir installé sur un ordinateur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vous ne pouvez pas modifier l'ordinateur d'un membre de domaine en un contrôleur de domaine. Vous devez désinstaller [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avant de modifier l'ordinateur hôte en un contrôleur de domaine.    
- Après avoir installé sur un ordinateur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vous ne pouvez pas modifier l'ordinateur d'un contrôleur de domaine en un membre de domaine. Vous devez désinstaller [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avant de modifier l'ordinateur hôte en un membre de domaine.   
- Les instances de cluster de basculement[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ne sont pas prises en charge quand les nœuds du cluster sont des contrôleurs de domaine.   
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] n’est pas pris en charge sur un contrôleur de domaine en lecture seule. Le programme d'installation de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ne peut pas créer de groupes de sécurité ni configurer de comptes de service [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sur un contrôleur de domaine en lecture seule. Dans ce scénario, le programme d'installation échoue. 
- Une instance de cluster de basculement [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] n’est pas prise en charge dans un environnement au sein duquel un contrôleur de domaine en lecture seule est accessible. 
  
## <a name="see-also"></a>Voir aussi  
 [Planification d'une installation SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Considérations sur la sécurité pour une installation SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   

