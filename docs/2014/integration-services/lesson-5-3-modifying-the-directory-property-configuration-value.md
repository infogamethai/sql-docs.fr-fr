---
title: 'Étape 3 : Modification de la valeur de Configuration de propriété de répertoire | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cb83ac5bb1b811c23b782b01167c437e9b989518
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767361"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>Étape 3 : Modification de la valeur de configuration de la propriété Directory
  Dans cette tâche, vous modifiez le paramètre de configuration (stocké dans le fichier SSISTutorial.dtsConfig) pour la propriété Value de la variable de niveau package `User::varFolderName`. Cette variable met à jour la propriété Directory du conteneur de boucles Foreach. La valeur modifiée pointe vers le `New Sample Data` dossier que vous avez créé dans la tâche précédente. Une fois le paramètre de configuration modifié et le package exécuté, la propriété Directory est mise à jour par la variable, en utilisant la valeur récupérée dans le fichier de configuration au lieu de la valeur de la propriété Directory configurée au départ dans le package.  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>Pour modifier le paramétrage de configuration de la propriété Directory  
  
1.  Dans le Bloc-notes ou dans tout autre éditeur de texte, recherchez et ouvrez le fichier de configuration SSISTutorial.dtsConfig que vous avez créé à l'aide de l'Assistant Configuration de package au cours de la tâche précédente.  
  
2.  Modifiez la valeur de la **ConfiguredValue** élément pour faire correspondre le chemin d’accès de la `New Sample Data` dossier que vous avez créé dans la tâche précédente. N'encadrez pas le chemin d'accès de guillemets. Si le `New Sample Data` dossier est à la racine de votre lecteur (par exemple, C:\\), le code XML mis à jour doit être similaire à l’exemple suivant :  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     Les informations d’en-tête, `GeneratedBy`, `GeneratedFromPackageID`, et **GeneratedDate** sera différente dans votre fichier, bien sûr. L'élément à noter est l'élément `Configuration`. La propriété `Value` de la variable `User::varFolderName` contient maintenant C:\New Sample Data.  
  
3.  Enregistrez les modifications, puis fermez l'éditeur de texte.  
  
## <a name="next-task-in-lesson"></a>Tâche suivante de la leçon  
 [Étape 4 : Tester le Package leçon 5 du didacticiel](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
