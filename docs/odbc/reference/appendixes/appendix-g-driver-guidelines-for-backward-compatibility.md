---
title: 'Annexe G : Conseils sur les pilotes pour la compatibilité descendante | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a07e936617100c56f8fa873df1b490e1d61e3f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909953"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>Annexe G : Conseils sur les pilotes pour la compatibilité descendante
Cette annexe fournit des informations pour les writers de pilote travaillant sur ODBC 3. *x* pilotes devant prendre en charge d’ODBC 2. *x* applications. Pour plus d’informations sur la compatibilité descendante, consultez [la compatibilité descendante et conformité aux normes](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Cette section contient les rubriques suivantes.  
  
-   [Curseurs de bloc, curseurs avec défilement et compatibilité descendante pour les pilotes ODBC 3.x](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) -nouvelles fonctionnalités sont des fonctionnalités qui existent dans ODBC 3. *x* et non dans ODBC 2. *x*. ODBC 3. *x* pilotes ne disposent généralement pas à vous soucier de la compatibilité descendante avec les nouvelles fonctionnalités, car ODBC 2. *x* applications jamais les utilisent. Les seul exceptions sont les fonctionnalités liées à **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, et **SQLExtendedFetch**; pour plus d’informations plus d’informations, consultez, plus loin dans cette annexe.  
  
-   [Mappage des fonctions déconseillées](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) -fonctionnalités en double sont des fonctions qui sont implémentées différemment dans ODBC 3. *x* et ODBC 2. *x*. ODBC 3. *x* pilotes n’ont pas à vous soucier de la compatibilité descendante avec les fonctionnalités en doublon, car le Gestionnaire de pilotes est toujours mappée ODBC 2. *x* fonctionnalités à ODBC 3. *x* fonctionnalités lors de l’appel d’un ODBC 3. *x* pilote. Par conséquent, une application ODBC 3. *x* pilote ne voit que ODBC 3. *x* fonctionnalités. Pour plus d’informations sur ces mappages, consultez, plus loin dans cette annexe.  
  
-   [Changements de comportement et pilotes ODBC 3.x](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) -changements de comportement sont les fonctionnalités qui sont gérées différemment dans ODBC 3. *x* et ODBC 2. *x*. ODBC 3. *x* pilotes ont soucier des changements de comportement et d’agir en réponse à l’attribut d’environnement SQL_ATTR_ODBC_VERSION définie par l’application.
