---
title: Applications conformes aux normes et les pilotes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4980cfe64a5a8e8404c6b5b0bdc8b1aba484f0c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107333"
---
# <a name="standards-compliant-applications-and-drivers"></a>Applications et pilotes conformes aux normes
Une application conforme aux normes ou le pilote est celui qui est conforme à la spécification d’IAO groupe Open « gestion des données : Interface de niveau d’appel SQL (CLI) » et la norme ISO/IEC 9075-Interface de niveau d’appel 3:1995 (E) (SQL/CLI).  
  
 ODBC *3.x* garantit les fonctionnalités suivantes :  
  
-   Une application écrite dans les spécifications Open Group et ISO CLI fonctionne avec une application ODBC *3.x* pilote ou un pilote conforme aux normes lorsqu’il est compilé avec ODBC *3.x* en-tête des fichiers et lié à ODBC *3.x* bibliothèques, et quand il accède au pilote via ODBC *3.x* Gestionnaire de pilotes.  
  
-   Un pilote écrit dans les spécifications Open Group et ISO CLI fonctionne avec une application ODBC *3.x* application ou une application conforme aux normes lorsqu’il est compilé avec ODBC *3.x* en-tête des fichiers et lié avec ODBC *3.x* bibliothèques, et lorsque l’application accède au pilote via ODBC *3.x* Gestionnaire de pilotes.  
  
 Pilotes et les applications conformes aux normes sont compilées avec l’indicateur de compilation ODBC_STD.  
  
 Applications conformes aux normes présentent le comportement suivant :  
  
-   Si une application conforme aux normes appelle **SQLAllocEnv** (qui peut se produire car **SQLAllocEnv** est une fonction valide dans l’Open Group et ISO CLI), l’appel est mappé à  **SQLAllocHandleStd** au moment de la compilation. Par conséquent, au moment de l’exécution, l’application appelle **SQLAllocHandleStd**. Au cours de traitement de cet appel, le Gestionnaire de pilotes définit l’attribut d’environnement SQL_ATTR_ODBC_VERSION à SQL_OV_ODBC3. Un appel à **SQLAllocHandleStd** équivaut à un appel à **SQLAllocHandle** avec un *HandleType* de SQL_HANDLE_ENV et un appel à **SQLSetEnvAttr** à la valeur SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3.  
  
-   Si une application conforme aux normes appelle **SQLBindParam** (qui peut se produire car **SQLBindParam** est une fonction valide dans l’Open Group et ISO CLI), ODBC *3.x* Gestionnaire de pilotes mappe l’appel à l’appel équivalent dans **SQLBindParameter**. (Consultez [SQLBindParam, mappage](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) dans l’annexe g : Pilote des instructions pour la compatibilité descendante.)  
  
-   Pour s’aligner avec la CLI ISO, ODBC *3.x* fichiers d’en-tête contiennent des alias pour les types d’informations utilisés dans les appels à **SQLGetInfo**. Une application conforme aux normes peut utiliser ces alias au lieu de ODBC *3.x* types d’informations. Pour plus d’informations, consultez la rubrique suivante, [fichiers d’en-tête](../../../odbc/reference/develop-app/header-files.md).  
  
-   Une application conforme aux normes doit vérifier qu’il prend en charge de toutes les fonctionnalités sont prises en charge dans le pilote, avec qu'elle fonctionnera. Définition de l’attribut d’instruction SQL_ATTR_CURSOR_SCROLLABLE à SQL_SCROLLABLE et en affectant l’attribut d’instruction SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE ou SQL_SENSITIVE sont les fonctionnalités qui sont disponibles en tant que fonctionnalités facultatives dans les normes mais ne sont ne pas inclus dans le système ODBC *3.x* Core niveau et par conséquent ne peut pas être pris en charge par tous les ODBC *3.x* pilotes. Si une application conforme aux normes utilise ces fonctionnalités, il doit vérifier que le pilote qui fonctionne avec les prend en charge.
