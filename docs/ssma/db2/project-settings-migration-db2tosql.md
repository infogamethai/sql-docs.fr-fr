---
title: Paramètres (Migration) (DB2ToSQL) du projet | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 40c6c1063ff738428072f3198cae8827e78e2390
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060155"
---
# <a name="project-settings-migration-db2tosql"></a>Paramètres du projet (Migration) (DB2ToSQL)
La page de la Migration de la **paramètres du projet** boîte de dialogue contient les paramètres qui personnalisent comment SSMA migre les données de DB2 vers [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Le volet de la Migration est disponible à la fois dans le **paramètres du projet** et **par défaut des paramètres de projet** boîtes de dialogue.  
  
-   Pour spécifier les paramètres pour tous les projets SSMA, sur le **outils** menu, sélectionnez **par défaut des paramètres de projet**, sélectionnez le type de projet de migration pour lequel les paramètres sont requis pour être affichées ou modifiées à partir de **Version cible de migration** déroulante cliquez **général** en bas du volet gauche, puis cliquez sur **Migration**.  
  
-   Pour spécifier les paramètres pour le projet actuel, sur le **outils** menu, sélectionnez **paramètres du projet**, cliquez sur **général** en bas du volet gauche, puis cliquez sur **Migration**.  
  
## <a name="migration-engine"></a>Moteur de migration  
  
|Terme|Définition|  
|--------|--------------|  
|**Moteur de migration**|Spécifie le moteur de base de données utilisé lors de la Migration de données. Migration des données côté client fait référence au client SSMA récupérer les données de la source et l’insertion en bloc ces données dans SQL Server. Migration des données côté serveur fait référence au moteur de migration de données SSMA (programme de copie en bloc) en cours d’exécution sur la zone de SQL Server en tant que l’Agent SQL tâche récupérer des données à partir de la source et en insérant directement dans SQL Server, ce qui évite un client supplémentaire-saut (meilleures performances).<br /><br />**Par défaut en Mode**:  Moteur de Migration de données côté client<br /><br />**Mode optimiste**:  Moteur de Migration de données côté client<br /><br />**Mode plein**:  Moteur de Migration de données côté client|  
  
> [!IMPORTANT]  
> Lorsque le **moteur de Migration** option est définie sur **moteur de Migration de données côté serveur**, un nouveau projet de définition d’option **moteur de Migration de données côté serveur utiliser 32 bits** s’affiche . Il spécifie si l’utilitaire de programme de copie en bloc (BCP) 32 bits ou 64 bits est utilisé pour migrer des données.  
  
## <a name="miscellaneous-options"></a>Options diverses  
  
|Terme|Définition|  
|--------|--------------|  
|**Taille de lot**|Spécifie le lot taille utilisée pendant la migration des données.<br /><br />**Par défaut en Mode**:  10000<br /><br />**Mode optimiste**:  10000<br /><br />**Mode plein**:  10000|  
|**Contraintes de validation**|Spécifie si SSMA doit vérifier les contraintes lors de l’insertion des données dans des tables SQL Server.<br /><br />**Par défaut en Mode**:  False<br /><br />**Mode optimiste**:  False<br /><br />**Mode plein**:  False|  
|**Délai d’attente de Migration de données**|Spécifie le délai d’attente utilisé lors de la migration de données<br /><br />**Par défaut en Mode**:  15<br /><br />**Mode optimiste**:  15<br /><br />**Mode plein**:  15|  
|**Options de Migration des données étendues**|Affiche les options de migration de données supplémentaires pour chaque table dans l’onglet Détail distinct.<br /><br />**Par défaut en Mode**:  Masquer<br /><br />**Mode optimiste**:  Masquer<br /><br />**Mode plein**:  Masquer|  
|**Exécuter les déclencheurs**|Spécifie si SSMA doit exécuter les déclencheurs d’insertion lorsqu’il ajoute des données dans des tables SQL Server.<br /><br />**Par défaut en Mode**:  False<br /><br />**Mode optimiste**:  False<br /><br />**Mode plein**:  False|  
|**Conserver l'identité**|Spécifie si SSMA conserve les valeurs null dans la source de données lorsqu’il ajoute des données à SQL Server, indépendamment des valeurs par défaut qui sont spécifiés dans SQL Server.<br /><br />**Par défaut en Mode**:  True<br /><br />**Mode optimiste**:  True<br /><br />**Mode plein**:  False|  
|**Conserver les valeurs NULL**|Spécifie si SSMA conserve les valeurs null dans la source de données lorsqu’il ajoute des données à SQL Server, indépendamment des valeurs par défaut qui sont spécifiés dans SQL Server.<br /><br />**Par défaut en Mode**:  True<br /><br />**Mode optimiste**:  True<br /><br />**Mode plein**:  True|  
|**Marquer l’opération de suppression de chaîne avec l’erreur**|Si la taille de la colonne cible est inférieure à la longueur de la chaîne source, la valeur sera être supprimée et marquée comme une erreur.<br /><br />**Par défaut en Mode**:  Oui<br /><br />**Mode optimiste**:  Oui<br /><br />**Mode plein**:  Oui|  
|**En cas d’erreur**|Arrête la migration des données lorsqu’une erreur se produit. Il offre trois options :<br /><br />**Arrêter la migration :** Opération de migration de données s’arrête<br /><br />**Passez à la table suivante :** Arrête la migration des données dans la table actuelle et se poursuit à la suivante<br /><br />**Passez à un lot suivant :** Arrête la migration des données dans le lot actuel et se poursuit à la suivante<br /><br />**Par défaut en Mode**: Continuer le lot suivant<br /><br />**Mode optimiste**: Continuer le lot suivant<br /><br />**Mode plein**: Continuer le lot suivant|  
|**Remplacer les dates non pris en charge**|Spécifie si SSMA devrait corriger les dates antérieures au plus tôt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** date (01 janvier 1753).<br /><br />Pour conserver les valeurs de date actuel, sélectionnez **ne rien faire**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] n’accepte pas les dates antérieures au 01 janvier 1753 dans une colonne datetime. Si vous utilisez des dates antérieures, vous devez convertir les valeurs datetime aux valeurs de caractère.<br /><br />Pour convertir les dates antérieures au 01 janvier 1753 avec la valeur NULL, sélectionnez **remplacer par NULL**.<br /><br />Pour remplacer les dates antérieures au 01 janvier 1753 avec une date de prise en charge, sélectionnez **remplacer par le plus proche de date pris en charge**.<br /><br />**Par défaut en Mode**: Ne rien faire<br /><br />**Mode optimiste**: Ne rien faire<br /><br />**Mode plein**: Remplacez par le plus proche de date pris en charge|  
|**Verrou de table**|Spécifie si SSMA verrouille les tables lorsqu’il ajoute des données aux tables pendant la migration de données. Obtient un verrou de mise à jour en bloc pour la durée de l’opération de copie en bloc. Si la valeur est False, un verrou est défini au niveau des lignes.<br /><br />**Par défaut en Mode**:  True<br /><br />**Mode optimiste**:  True<br /><br />**Mode plein**:  True|  
  
## <a name="parallel-data-migration"></a>Migration de données en parallèle  
  
|Terme|Définition|  
|--------|--------------|  
|**Mode de Migration de données en parallèle**|Spécifie le mode utilisé pour les threads de branchement pour permettre la migration de données en parallèle. En mode Auto, SSMA choisit le nombre de threads (10 par défaut) dupliqué pour migrer les données. En mode personnalisé, utilisateur peut spécifier le nombre de threads dupliqué pour migrer des données (valeur minimale est 1 et la valeur maximale est 100). Actuellement, moteur migration client uniquement des données de côté prend en charge la migration de données en parallèle.<br /><br />**Par défaut en Mode**:  Auto<br /><br />**Mode optimiste**:  Auto<br /><br />**Mode plein**:  Auto|  
  
> [!IMPORTANT]  
> Lorsque le **Mode de Migration de données parallèle** option est définie sur **personnalisé**, un nouveau projet de définition d’option **le nombre de threads** s’affiche. Il spécifie le nombre de threads utilisés pour la migration de données.  
  
