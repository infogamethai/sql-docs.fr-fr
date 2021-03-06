---
title: Connexion avec l'authentification Azure Active Directory | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b596936010fcdce4eb5c0701c5f0c6631cd9687e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028122"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Connexion avec l'authentification Azure Active Directory

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Cet article fournit des informations sur le développement d’applications Java pour utiliser la fonctionnalité d’authentification Azure Active Directory avec le pilote Microsoft JDBC pour SQL Server.

Vous pouvez utiliser l’authentification Azure Active Directory (AAD), qui est un mécanisme de connexion à Azure SQL Database V12 à l’aide d’identités dans Azure Active Directory. Utilisez l’authentification Azure Active Directory pour gérer de manière centralisée les identités des utilisateurs de base de données et comme alternative à l’authentification SQL Server. Le pilote JDBC vous permet de spécifier vos informations d’identification de Azure Active Directory dans la chaîne de connexion JDBC pour vous connecter à la base de données SQL Azure. Pour plus d’informations sur la configuration de l’authentification Azure Active Directory [, consultez connexion à SQL Database à l’aide de l’authentification Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Les propriétés de connexion pour la prise en charge de l’authentification Azure Active Directory dans le pilote JDBC Microsoft pour SQL Server sont les suivantes:
*   **authentification**: utilisez cette propriété pour indiquer la méthode d’authentification SQL à utiliser pour la connexion. Les valeurs possibles sont : 
    * **ActiveDirectoryMSI**
        * Pris en charge depuis la version de `authentication=ActiveDirectoryMSI` pilote **v 7.2**, peut être utilisé pour se connecter à un Azure SQL Database/Data Warehouse à partir d’une ressource Azure avec la prise en charge de l’identité activée. Si vous le souhaitez, **msiClientId** peut également être spécifié dans les propriétés Connection/DataSource avec ce mode d’authentification, qui doit contenir l’ID client d’un Managed Service Identity à utiliser pour acquérir le **accessToken** pour l’établissement connexion.
    * **ActiveDirectoryIntegrated**
        * Pris en charge depuis la version Driver `authentication=ActiveDirectoryIntegrated` **v 6.0**, peut être utilisé pour se connecter à un Azure SQL Database/Data Warehouse à l’aide de l’authentification intégrée. Pour utiliser ce mode d’authentification, vous devez fédérer l’Services ADFS local (ADFS) avec Azure Active Directory dans le Cloud. Une fois la configuration terminée, vous pouvez vous connecter en ajoutant la bibliothèque Native’sqljdbc_auth. dll’au chemin d’accès de la classe d’application sur le système d’exploitation Windows, ou en configurant un ticket Kerberos pour la prise en charge de l’authentification multiplateforme. Vous serez en mesure d’accéder à Azure SQL DB/DW sans être invité à entrer vos informations d’identification lorsque vous êtes connecté à un ordinateur joint à un domaine.
    * **ActiveDirectoryPassword**
        * Pris en charge depuis la version Driver `authentication=ActiveDirectoryPassword` **v 6.0**, peut être utilisé pour se connecter à un Azure SQL Database/Data Warehouse à l’aide d’un nom et d’un mot de passe de principal Azure ad.
    * **SqlPassword**
        * Utilisez `authentication=SqlPassword` pour vous connecter à un SQL Server à l’aide des propriétés UserName/user et Password.
    * **NotSpecified**
        * Utilisez `authentication=NotSpecified` ou laissez la valeur par défaut quand aucune de ces méthodes d’authentification n’est nécessaire.

*   **accessToken**: utilisez cette propriété de connexion pour vous connecter à un SQL Database à l’aide d’un jeton d’accès. accessToken peut uniquement être défini à l’aide du paramètre Properties de la méthode getConnection () dans la classe par. Il ne peut pas être utilisé dans l’URL de connexion.  

Pour plus d’informations, consultez la propriété Authentication dans la page [définition des propriétés de connexion](../../connect/jdbc/setting-the-connection-properties.md) .  


## <a name="client-setup-requirements"></a>Configuration requise pour le client
Pour l’authentification **ActiveDirectoryMSI** , les composants ci-dessous doivent être installés sur l’ordinateur client:
* Java 8 ou version ultérieure
* Pilote JDBC Microsoft 7,2 (ou version ultérieure) pour SQL Server
* L’environnement client doit être une ressource Azure et la prise en charge de la fonctionnalité «identité» doit être activée.
* Un utilisateur de base de données à relation contenant-contenu représentant l’identité gérée affectée par le système de votre ressource Azure ou l’identité gérée affectée à l’utilisateur, ou l’un des groupes auxquels votre MSI appartient, doit exister dans la base de données cible et doit disposer de l’autorisation CONNECT.

Pour d’autres modes d’authentification, les composants ci-dessous doivent être installés sur l’ordinateur client:
* Java 7 ou version ultérieure
* Pilote JDBC Microsoft 6,0 (ou version ultérieure) pour SQL Server
* Si vous utilisez le mode d’authentification par jeton d’accès, vous avez besoin d' [Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) et de ses dépendances pour exécuter les exemples de cet article. Pour plus d’informations, consultez la section **connexion à l’aide** d’un jeton d’accès.
* Si vous utilisez le mode d’authentification **ActiveDirectoryPassword** , vous avez besoin [d’Azure-ActiveDirectory-Library-for-Java et de](https://github.com/AzureAD/azure-activedirectory-library-for-java) ses dépendances. Pour plus d’informations, consultez la section **connexion à l’aide du mode d’authentification ActiveDirectoryPassword** .
* Si vous utilisez le mode **ActiveDirectoryIntegrated** , vous avez besoin d’Azure-ActiveDirectory-Library-for-Java et de ses dépendances. Pour plus d’informations, consultez la section **connexion à l’aide du mode d’authentification ActiveDirectoryIntegrated** .

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>Connexion à l’aide du mode d’authentification ActiveDirectoryMSI
L’exemple suivant montre comment utiliser le mode `authentication=ActiveDirectoryMSI`. Exécutez cet exemple à partir d’une ressource Azure, e, g d’une machine virtuelle Azure, App Service ou d’un Function App fédéré avec Azure Active Directory.

Avant d’exécuter l’exemple, remplacez le nom du serveur/de la base de données par le nom de votre serveur ou de votre base de données dans les lignes suivantes:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

L’exemple utilise le mode d’authentification ActiveDirectoryMSI:

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AAD_MSI {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryMSI");
        // Optional
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

L’exécution de cet exemple sur une machine virtuelle Azure récupère un jeton d’accès à partir de l' _identité gérée affectée_ par le système ou de l' _identité gérée_ par l’utilisateur (si **msiClientId** est spécifié) et établit une connexion à l’aide de l’accès extrait. lexical. Si une connexion est établie, le message suivant doit s’afficher:

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Connexion à l’aide du mode d’authentification ActiveDirectoryIntegrated
Avec la version 6,4, le pilote JDBC Microsoft ajoute la prise en charge de l’authentification ActiveDirectoryIntegrated à l’aide d’un ticket Kerberos sur plusieurs plateformes (Windows, Linux et macOS).
Pour plus d’informations, consultez [définir le ticket Kerberos sur Windows, Linux et Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) pour plus d’informations. Sur Windows, sqljdbc_auth. dll peut également être utilisé pour l’authentification ActiveDirectoryIntegrated avec le pilote JDBC.

> [!NOTE]
>  Si vous utilisez une version antérieure du pilote, consultez ce [lien](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) pour les dépendances respectives requises pour utiliser ce mode d’authentification. 

L’exemple suivant montre comment utiliser le mode `authentication=ActiveDirectoryIntegrated`. Exécutez cet exemple sur un ordinateur appartenant à un domaine qui est fédéré avec Azure Active Directory. Un utilisateur de base de données à relation contenant-contenu représentant votre principal de Azure AD, ou l’un des groupes auxquels vous appartenez, doit exister dans la base de données et doit disposer de l’autorisation CONNECT. 

Avant de générer et d’exécuter l’exemple, sur l’ordinateur client (sur lequel vous souhaitez exécuter l’exemple), téléchargez la [bibliothèque Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) et ses dépendances, et incluez-les dans le chemin de build Java.

Avant d’exécuter l’exemple, remplacez le nom du serveur/de la base de données par le nom de votre serveur ou de votre base de données dans les lignes suivantes:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

L’exemple utilise le mode d’authentification ActiveDirectoryIntegrated:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADIntegrated {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

L’exécution de cet exemple sur un ordinateur client utilise automatiquement votre ticket Kerberos et aucun mot de passe n’est requis. Si une connexion est établie, le message suivant doit s’afficher:

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Définir le ticket Kerberos sur Windows, Linux et Mac

Vous devez configurer un ticket Kerberos qui lie votre utilisateur actuel à un compte de domaine Windows. Vous trouverez ci-dessous un résumé des étapes clés.

#### <a name="windows"></a>Windows
JDK est fourni `kinit`avec, que vous pouvez utiliser pour obtenir un ticket TGT d’Centre de distribution de clés (KDC) sur un ordinateur joint à un domaine fédéré avec Azure Active Directory.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Étape 1: récupération d’un ticket d’accord de ticket
- **Exécuter sur**: Windows
- **Action** :
  - Utilisez la commande `kinit username@DOMAIN.COMPANY.COM` pour obtenir un ticket TGT du KDC, puis vous serez invité à entrer votre mot de passe de domaine.
  - Utilisez `klist` pour afficher les tickets disponibles. Si kinit a réussi, vous devez voir un ticket de krbtgt/domaine. COMPANY. COM @ DOMAIN.COMPANY.COM.

> [!NOTE]
>  Vous devrez peut-être spécifier `.ini` un fichier `-Djava.security.krb5.conf` avec pour votre application afin de localiser KDC.

#### <a name="linux-and-mac"></a>Linux et Mac

##### <a name="requirements"></a>Spécifications
Accédez à un ordinateur Windows joint à un domaine pour interroger votre contrôleur de domaine Kerberos.

##### <a name="step-1-find-kerberos-kdc"></a>Étape 1: Rechercher Kerberos KDC
- **Exécuter sur**: ligne de commande Windows
- **Action**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (où «Domain.Company.com» correspond au nom de votre domaine)
- **Résultat de l'exemple**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Informations à extraire** Nom du contrôleur de périphérique, dans ce cas`co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Étape 2: configuration du KDC dans krb5. conf
- **Exécuter sur**: Linux/Mac
- **Action**: modifiez le/etc/krb5.conf dans l’éditeur de votre choix. Configurez les clés suivantes
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  Enregistrez ensuite le fichier krb5.conf et quittez

> [!NOTE]
>  Le domaine doit être en MAJUSCULES.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>Étape 3 : tester la récupération du ticket d'attribution de ticket
- **Exécuter sur**: Linux/Mac
- **Action** :
  - Utilisez la commande `kinit username@DOMAIN.COMPANY.COM` pour obtenir un ticket TGT du KDC, puis vous serez invité à entrer votre mot de passe de domaine.
  - Utilisez `klist` pour afficher les tickets disponibles. Si kinit a réussi, vous devez voir un ticket de krbtgt/domaine. COMPANY. COM @ DOMAIN.COMPANY.COM.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>Connexion à l’aide du mode d’authentification ActiveDirectoryPassword
L’exemple suivant montre comment utiliser le mode `authentication=ActiveDirectoryPassword`.

Avant de générer et d’exécuter l’exemple:
1.  Sur l’ordinateur client (sur lequel vous souhaitez exécuter l’exemple), téléchargez la [bibliothèque Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) et ses dépendances, et incluez-les dans le chemin de la build Java.
2.  Recherchez les lignes de code suivantes et remplacez le nom du serveur/de la base de données par le nom de votre serveur ou de votre base de données.
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  Recherchez les lignes de code suivantes et remplacez nom d’utilisateur par le nom de l’utilisateur AAD auquel vous souhaitez vous connecter.
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

L’exemple utilise le mode d’authentification ActiveDirectoryPassword:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADUserPassword {
    
    public static void main(String[] args) throws Exception{
        
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
Si la connexion est établie, le message suivant doit s’afficher comme sortie:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Une base de données utilisateur contenue doit exister et un utilisateur de base de données à relation contenant-contenu représentant le Azure AD utilisateur ou l’un des groupes spécifiés, le Azure AD utilisateur spécifié appartient à, doit exister dans la base de données et doit disposer de l’autorisation CONNECT (sauf pour Azure Active Directory administrateur ou groupe de serveurs)

## <a name="connecting-using-access-token"></a>Connexion à l’aide d’un jeton d’accès
Les applications/services peuvent récupérer un jeton d’accès à partir de la Azure Active Directory et l’utiliser pour se connecter à Azure SQL Database/Data Warehouse.

> [!NOTE] 
> **accessToken** peut uniquement être défini à l’aide du paramètre Properties de la méthode getConnection () dans la classe par. Elle ne peut pas être utilisée dans la chaîne de connexion.

L’exemple ci-dessous contient une application Java simple qui se connecte à Azure SQL Database/Data Warehouse à l’aide de l’authentification basée sur les jetons d’accès. Avant de générer et d’exécuter l’exemple, procédez comme suit:
1.  Créez un compte d’application dans Azure Active Directory pour votre service.
    1. Connectez-vous au portail Azure.
    2. Cliquez sur Azure Active Directory dans le volet de navigation de gauche.
    3. Cliquez sur l’onglet «inscriptions d’applications».
    4. Dans le tiroir, cliquez sur «nouvelle inscription d’application».
    5. Entrez mytokentest comme nom convivial pour l’application, sélectionnez «application Web/API».
    6. Nous n’avons pas besoin de l’URL de connexion. N’indiquez rien: « https://mytokentest ».
    7. Cliquez sur «créer» en bas.
    9. Toujours dans le Portail Azure, cliquez sur l’onglet «Paramètres» de votre application, puis ouvrez l’onglet «Propriétés».
    10. Recherchez la valeur «ID d’application» (alias client ID), puis copiez-la, vous en aurez besoin plus tard lors de la configuration de votre application (par exemple, 1846943b-AD04-4808-aa13-4702d908b5c1). Consultez la capture instantanée suivante.
    11. Sous la section «clés», créez une clé en renseignant le champ nom, en sélectionnant la durée de la clé et en enregistrant la configuration (laissez le champ valeur vide). Après l’enregistrement, le champ de valeur doit être renseigné automatiquement, copiez la valeur générée. Il s’agit du secret du client.
    12. Dans le volet gauche, cliquez sur Azure Active Directory. Sous «inscriptions des applications», recherchez l’onglet «points de terminaison». Copiez l’URL sous «point de terminaison de jeton serment 2,0», il s’agit de votre URL STS.
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Connectez-vous à la base de données utilisateur de votre SQL Server Azure en tant qu’administrateur Azure Active Directory et utilisez une commande T-SQL pour configurer un utilisateur de base de données à relation contenant-contenu pour votre principal d’application. Pour plus d’informations, consultez la page [connexion à SQL Database ou SQL Data Warehouse à l’aide de l’authentification Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) pour plus d’informations sur la création d’un administrateur de Azure Active Directory et d’un utilisateur de base de données à relation contenant-contenu.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  Sur l’ordinateur client (sur lequel vous souhaitez exécuter l’exemple), téléchargez la bibliothèque [Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) et ses dépendances, et incluez-les dans le chemin de la build Java. Notez que la bibliothèque Azure-ActiveDirectory-Library-for-Java n’est nécessaire que pour exécuter cet exemple spécifique. L’exemple utilise les API de cette bibliothèque pour récupérer le jeton d’accès à partir d’Azure AAD. Si vous disposez déjà d’un jeton d’accès, vous pouvez ignorer cette étape. Notez que vous devez également supprimer la section de l’exemple qui récupère le jeton d’accès.

Dans l’exemple suivant, remplacez l’URL STS, l’ID client, la clé secrète client, le nom du serveur et de la base de données par vos valeurs.

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD.
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;

public class AADTokenBased {

    public static void main(String[] args) throws Exception {

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);

        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

Si la connexion réussit, le message suivant doit s’afficher comme sortie:

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
