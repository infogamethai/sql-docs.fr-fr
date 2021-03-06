---
title: L’accès concurrentiel optimiste | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f5f4b7101718ea8372c9635a064dc81e1d8f6c1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023392"
---
# <a name="optimistic-concurrency"></a>Accès concurrentiel optimiste
*L’accès concurrentiel optimiste* tire son nom l’hypothèse optimiste que collisions entre les transactions seront produit rarement, une collision d’on dit avoir eu lieu lorsqu’une autre transaction met à jour ou supprime une ligne de données entre le moment où il est en lecture par la transaction en cours et le temps, il est mis à jour ou supprimé. Il est l’opposé de *d’accès concurrentiel pessimiste,* ou de verrouillage, dans lequel le développeur d’applications est convaincu que ces collisions sont très courants.  
  
 Dans l’accès concurrentiel optimiste, une ligne est restée déverrouillé jusqu'à ce que le moment est venu pour mettre à jour ou le supprimer. À ce stade, la ligne est relue et vérifiée pour voir si elle a été modifiée depuis sa dernière lecture. Si la ligne a changé, la mise à jour ou suppression échoue et doit être tentée à nouveau.  
  
 Pour déterminer si une ligne a été modifiée, sa nouvelle version est vérifiée par rapport à une version mise en cache de la ligne. La vérification peut être basée sur la version de ligne, telles que la colonne timestamp dans SQL Server, ou les valeurs de chaque colonne dans la ligne. Nombreux SGBD ne prennent pas en charge les versions de ligne.  
  
 L’accès concurrentiel optimiste peut être implémentée par la source de données ou de l’application. Dans les deux cas, l’application doit utiliser un niveau d’isolement de transaction faible tels que Read Committed ; à l’aide d’un niveau plus élevé nie la concurrence accrue obtenue à l’aide de l’accès concurrentiel optimiste.  
  
 Si l’accès concurrentiel optimiste est implémenté par la source de données, l’application définit l’attribut d’instruction SQL_ATTR_CONCURRENCY SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES. Pour mettre à jour ou supprimer une ligne, il exécute une mise à jour positionnée ou d’une instruction delete ou d’appels **SQLSetPos** comme il le ferait avec l’accès concurrentiel pessimiste ; la source de données ou le pilote retourne SQLSTATE 01001 (conflit d’opération de curseur) si le mettre à jour ou suppression échoue en raison d’une collision.  
  
 Si l’application elle-même implémente l’accès concurrentiel optimiste, elle définit l’attribut d’instruction SQL_ATTR_CONCURRENCY sur SQL_CONCUR_READ_ONLY pour lire une ligne. Si elle compare les versions de ligne et ne connaît pas la colonne de version de ligne, elle appelle **SQLSpecialColumns** avec l’option SQL_ROWVER pour déterminer le nom de cette colonne.  
  
 L’application met à jour ou supprime la ligne en augmentant l’accès concurrentiel pour SQL_CONCUR_LOCK (pour accéder en écriture à la ligne) et l’exécution d’une **mise à jour** ou **supprimer** instruction avec un **où**  clause qui spécifie la version ou de valeurs de la ligne avait lorsque l’application le lire. Si la ligne a changé depuis lors, l’instruction échoue. Si le **où** clause n’identifie pas la ligne, l’instruction peut également mettre à jour ou supprimer des autres lignes ; les versions de ligne soit toujours identifient des lignes, mais les valeurs de ligne identifient de lignes uniquement si elles incluent la clé primaire.
