---
title: Fonctionnement des conversions de types de données | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ed91f1b38f68715cd174a96cb2f0364fc060482
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027483"
---
# <a name="understanding-data-type-conversions"></a>Présentation des conversions de types de données

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Pour faciliter la conversion des types de données du langage de programmation Java en types de données [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] assure les conversions des types de données requises par la spécification JDBC. Pour une flexibilité accrue, tous les types sont convertibles vers et à partir des types de données **Object**, **String**et **Byte []** .

## <a name="getter-method-conversions"></a>Conversions de méthodes Getter

Le tableau suivant, basé sur les types de données [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], présente le mappage des conversions du pilote JDBC pour les méthodes get\<Type>() de la classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), ainsi que les conversions prises en charge pour les méthodes get\<Type> de la classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).

![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")

Trois catégories de conversions sont prises en charge par les méthodes d'accesseur Get du pilote JDBC :

- **Sans perte (x)** : conversions pour le cas où le type getter est inférieur ou égal au type serveur sous-jacent. Par exemple, lors de l’appel de getBigDecimal sur une colonne décimale de serveur sous-jacente, aucune conversion n’est nécessaire.

- **Convertie (y)** : conversions de types serveur numériques en types du langage Java, où la conversion est standard et suit les règles de conversion du langage Java. Pour ces conversions, la précision est toujours tronquée (jamais arrondie) et les dépassements sont gérés comme un opérateur modulo du type de destination, qui est plus petit. Par exemple, l’appel de getInt sur **une** colonne décimale sous-jacente qui contient «1,9999» retourne «1», **ou** si la valeur décimale sous- **jacente** est «3 milliards», alors l’entier la valeur dépasse «-1294967296».

- **Dépendante des données (z)** : les conversions de types de caractère sous-jacents en types numériques nécessitent que les types caractère contiennent des valeurs pouvant être converties dans ce type. Aucune autre conversion n'a lieu. Si la valeur est trop élevée pour le type getter, elle n’est pas valide. Par exemple, si getInt est appelée sur une colonne varchar(50) contenant « 53 », la valeur est retournée en tant que **int** ; en revanche, si la valeur sous-jacente est « xyz » ou « 3000000000 », une erreur est générée.

Si getString est appelé sur un type de données **Binary**, **varbinary**, **varbinary (max)** ou **image** , la valeur est retournée en tant que valeur de chaîne hexadécimale.

## <a name="updater-method-conversions"></a>Conversions de méthodes Updater

Pour les données typées Java passées aux méthodes \<Type>() de la classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), les conversions suivantes s’appliquent.

![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")

Trois catégories de conversions sont prises en charge par les méthodes updater du pilote JDBC :

- **Sans perte (x)** : conversions pour le cas où le type updater est inférieur ou égal au type serveur sous-jacent. Par exemple, lors de l'appel de updateBigDecimal sur une colonne décimale de serveur sous-jacente, aucune conversion n'est nécessaire.

- **Convertie (y)** : conversions de types serveur numériques en types du langage Java, où la conversion est standard et suit les règles de conversion du langage Java. Pour ces conversions, la précision est toujours tronquée (jamais arrondie) et le dépassement de capacité est géré en tant que modulo du type de destination (type le plus petit). Par exemple, l’appel de updateDecimal sur une colonne **int** sous-jacente qui contient «1,9999» retourne «1», ou si la valeur **décimale** sous-jacente est «3 milliards», la valeur **int** déborde sur «-1294967296».

- **Dépendante des données (z)** : les conversions de types de données sources sous-jacents en types de données de destination nécessitent que les valeurs contenues puissent être converties dans les types de destination. Aucune autre conversion n'a lieu. Si la valeur est trop élevée pour le type getter, elle n’est pas valide. Par exemple, si updateString est appelé sur une colonne int qui contient « 53 », la mise à jour réussit ; toutefois, si la valeur String sous-jacente est « foo » ou « 3000000000 », une erreur est générée.

Lorsque updateString est appelé sur un type de données **Binary**, **varbinary**, **varbinary (max)** ou **image** , il gère la valeur de chaîne en tant que valeur de chaîne hexadécimale.

Quand le type de données de colonne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] est **XML**, la valeur des données doit être du **XML**valide. Lors de l’appel de méthodes updateBytes, updateBinaryStream ou updateBlob, la valeur de données doit être la représentation sous forme de chaîne hexadécimale des caractères XML. Par exemple :

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Notez qu'une marque d'ordre d'octet (BOM, Byte-Order Mark) est obligatoire si les caractères XML correspondent à des encodages de caractères spécifiques.

## <a name="setter-method-conversions"></a>Conversions de méthodes Setter

Pour les données typées Java passées aux méthodes set\<Type>() de la classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) et de la classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), les conversions suivantes s’appliquent.

![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")

Le serveur tente toutes les conversions et retourne des erreurs en cas d'échec.

Dans le cas du type de données **String** , si la valeur dépasse la longueur de **varchar**, elle est mappée à **LONGVARCHAR**. De même, **nvarchar** est mappé à **LONGNVARCHAR** si la valeur dépasse la longueur prise en charge de **nvarchar**. Il en va de même pour **byte[]** . Les valeurs de plus de **varbinary** deviennent **LONGVARBINARY**.

Deux catégories de conversions sont prises en charge par les méthodes setter du pilote JDBC :

- **Sans perte (x)** : conversions pour le cas numériques où le type setter est inférieur ou égal au type serveur sous-jacent. Par exemple, lors de l’appel de setBigDecimal sur une colonne **decimal** de serveur sous-jacente, aucune conversion n’est nécessaire. Pour les conversions de numérique à caractère, le type de données **numeric** Java est converti en **String**. Par exemple, l’appel de setDouble avec une valeur « 53 » sur une colonne varchar(50) produit une valeur caractère « 53 » dans cette colonne de destination.

- **Convertie (y)** : conversions d’un type **numérique** Java en type **numérique** serveur sous-jacent plus petit. Ces conversions sont standard et suivent les conventions de conversion [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La précision est toujours tronquée (jamais arrondie) et tout dépassement de capacité génère une erreur de conversion non prise en charge. Par exemple, l’utilisation de updateDecimal avec la valeur « 1,9999 » sur une colonne d’entiers sous-jacente produit « 1 » dans la colonne de destination ; en revanche, si la valeur « 3000000000 » est passée, le pilote génère une erreur.

- **Dépendant des données (z)** : les conversions d’un type de **chaîne** Java [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en type de données sous-jacent dépendent des conditions suivantes: le pilote envoie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valeur de **chaîne** à et effectue des conversions, Si nécessaire. Si sendStringParametersAsUnicode est définie sur true et que le type de données [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sous-jacent est **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] n’autorise pas la conversion de **nvarchar** en **image** et lève une exception SQLServerException. Si sendStringParametersAsUnicode est défini sur false et que le type de données [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sous-jacent est **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permet la conversion de **varchar** en **image** et aucune exception n’est levée.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] effectue les conversions et retourne les erreurs au pilote JDBC en cas de problème.

Quand le type de données de colonne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] est **XML**, la valeur des données doit être du **XML**valide. Lors de l’appel de méthodes updateBytes, updateBinaryStream ou updateBlob, la valeur de données doit être la représentation sous forme de chaîne hexadécimale des caractères XML. Par exemple :

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Notez qu'une marque d'ordre d'octet (BOM, Byte-Order Mark) est obligatoire si les caractères XML correspondent à des encodages de caractères spécifiques.

## <a name="conversions-on-setobject"></a>Conversions sur setObject

> [!NOTE]  
> Les pilotes Microsoft JDBC 4,2 (et versions ultérieures) pour SQL Server prennent en charge JDBC 4,1 et 4,2. Pour plus d’informations sur les mappages et les conversions de type de données 4,1 et 4,2, consultez [compatibilité jdbc 4,1 pour le pilote JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) et [compatibilité JDBC 4,2 pour le pilote JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md), en plus des informations ci-dessous.

Pour les données typées Java passées aux méthodes setObject(\<Type>) de la classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), les conversions suivantes s’appliquent.

![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")

La méthode setObject sans type cible spécifié utilise le mappage par défaut. Dans le cas du type de données **String** , si la valeur dépasse la longueur de **varchar**, elle est mappée à **LONGVARCHAR**. De même, **nvarchar** est mappé à **LONGNVARCHAR** si la valeur dépasse la longueur prise en charge de **nvarchar**. Il en va de même pour **byte[]** . Les valeurs de plus de **varbinary** deviennent **LONGVARBINARY**.

Trois catégories de conversions sont prises en charge par les méthodes setObject du pilote JDBC :

- **Sans perte (x)** : conversions pour le cas numériques où le type setter est inférieur ou égal au type serveur sous-jacent. Par exemple, lors de l’appel de setBigDecimal sur une colonne **decimal** de serveur sous-jacente, aucune conversion n’est nécessaire. Pour les conversions de numérique à caractère, le type de données **numeric** Java est converti en **String**. Par exemple, l’appel de setDouble avec une valeur « 53 » sur une colonne varchar(50) produit une valeur caractère « 53 » dans cette colonne de destination.

- **Convertie (y)** : conversions d’un type **numérique** Java en type **numérique** serveur sous-jacent plus petit. Ces conversions sont standard et suivent les conventions de conversion [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La précision est toujours tronquée (jamais arrondie) et tout dépassement de capacité génère une erreur de conversion non prise en charge. Par exemple, l’utilisation de updateDecimal avec la valeur « 1,9999 » sur une colonne d’entiers sous-jacente produit « 1 » dans la colonne de destination ; en revanche, si la valeur « 3000000000 » est passée, le pilote génère une erreur.

- **Dépendant des données (z)** : les conversions d’un type de **chaîne** Java [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en type de données sous-jacent dépendent des conditions suivantes: le pilote envoie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valeur de **chaîne** à et effectue des conversions, Si nécessaire. Si la propriété de connexion sendStringParametersAsUnicode est définie sur true et que le type de données [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sous-jacent est **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] n’autorise pas la conversion de **nvarchar** en **image** et lève une exception SQLServerException. Si sendStringParametersAsUnicode est défini sur false et que le type de données [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sous-jacent est **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permet la conversion de **varchar** en **image** et aucune exception n’est levée.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] effectue les conversions de définitions en masse et retourne les erreurs au pilote JDBC en cas de problème. Les conversions côté client constituent l’exception et sont effectuées uniquement dans le cas de valeurs de **Date**, d' **heure**, d' **horodatage**, de **valeur booléenne**et de **chaîne** .

Quand le type de données de colonne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] est **XML**, la valeur des données doit être du **XML**valide. Lors de l'appel des méthodes setObject(byte[], SQLXML), setObject(inputStream, SQLXML) ou setObject(Blob, SQLXML), la valeur de données doit être la représentation sous forme de chaîne hexadécimale des caractères XML. Par exemple :

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Notez qu'une marque d'ordre d'octet (BOM, Byte-Order Mark) est obligatoire si les caractères XML correspondent à des encodages de caractères spécifiques.

## <a name="see-also"></a>Voir aussi

[Présentation des types de données du pilote JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
