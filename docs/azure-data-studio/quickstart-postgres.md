---
title: 'Démarrage rapide : Se connecter à et interroger PostgreSQL'
titleSuffix: Azure Data Studio
description: Ce guide de démarrage rapide montre comment utiliser Azure Data Studio pour se connecter à PostgreSQL et exécuter une requête
ms.custom: seodec18
ms.date: 09/18/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
ms.openlocfilehash: ac4d1a3ae93310475c284661e1b8dff1d9a9f523
ms.sourcegitcommit: 183d622fff36a22b882309378892010be3bdcd52
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71127249"
---
# <a name="quickstart-connect-and-query-postgresql-using-includename-sosincludesname-sos-shortmd"></a>Démarrage rapide : Se connecter à et interroger PostgreSQL à l’aide de [!INCLUDE[name-sos](../includes/name-sos-short.md)]
Ce guide de démarrage rapide montre comment utiliser [!INCLUDE[name-sos](../includes/name-sos-short.md)] pour se connecter à Postgres, puis utiliser des instructions SQL pour créer la base de données *tutorialdb* et l’interroger.

## <a name="prerequisites"></a>Conditions préalables requises

Pour effectuer ce guide de démarrage rapide, vous avez besoin de [!INCLUDE[name-sos](../includes/name-sos-short.md)], de l’extension PostgreSQL pour [!INCLUDE[name-sos](../includes/name-sos-short.md)] et de l’accès à un serveur PostgreSQL.

- [Installez [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md).
- [Installez l’extension PostgreSQL pour Azure Data Studio](postgres-extension.md).
- [Installez PostgreSQL](https://www.postgresql.org/download/). (Vous pouvez également créer une base de données Postgres dans le cloud avec la commande [az postgres up](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli)). 

## <a name="connect-to-postgresql"></a>Se connecter à PostgreSQL

1. Démarrez **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** .

2. La première fois que vous démarrez [!INCLUDE[name-sos](../includes/name-sos-short.md)], la boîte de dialogue **Connexion** s’ouvre. Si la boîte de dialogue **Connexion** ne s’ouvre pas, cliquez sur l'icône **Nouvelle connexion** sur la page **SERVEUR** :

   ![Icône de nouvelle connexion](media/quickstart-postgresql/new-connection-icon.png)

3. Dans le formulaire qui s’affiche, accédez à **Type de connexion**, puis sélectionnez **PostgreSQL** dans la liste déroulante.


4. Renseignez les champs restants en utilisant le nom du serveur, le nom d’utilisateur et le mot de passe de votre serveur PostgreSQL. 

   ![Écran de nouvelle connexion](media/quickstart-postgresql/new-connection-screen.png)  

   | Paramètre       | Valeur d'exemple | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nom du serveur** | localhost | Nom complet du serveur |
   | **User name** | postgres | Nom d’utilisateur avec lequel vous souhaitez vous connecter. |
   | **Mot de passe (connexion SQL)** | *password* | Mot de passe du compte avec lequel vous vous connectez. |
   | **Mot de passe** | *Vérifier* | Cochez cette case si vous ne souhaitez pas entrer le mot de passe chaque fois que vous vous connectez. |
   | **Nom de la base de données** | \<Default\> | Renseignez ce champ si vous souhaitez que la connexion spécifie une base de données. |
   | **Groupe de serveurs** | \<Default\> | Cette option vous permet d’attribuer cette connexion à un groupe de serveurs spécifique que vous créez. | 
   | **Nom (facultatif)** | *laisser vide* | Cette option vous permet de spécifier un nom convivial pour votre serveur. | 

5. Sélectionnez **Se connecter**. 

Une fois la connexion établie, votre serveur s'ouvre dans la barre latérale **SERVEURS**.


## <a name="create-a-database"></a>création d'une base de données ;

La procédure suivante crée une base de données nommée **tutorialdb** :

1. Cliquez avec le bouton droit sur votre serveur PostgreSQL dans la barre latérale **SERVEURS**, puis sélectionnez **Nouvelle requête**.

2. Collez cette instruction SQL dans l’éditeur de requête qui s’ouvre.

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. Dans la barre d'outils, sélectionnez **Exécuter** pour exécuter la requête. Les notifications s'affichent dans le volet **MESSAGES** pour afficher la progression de la requête.

>[!TIP]
> Vous pouvez utiliser la touche **F5** de votre clavier pour exécuter l’instruction au lieu d'**Exécuter**.

Une fois la requête terminée, cliquez avec le bouton droit sur **Bases de données** et sélectionnez **Actualiser** pour afficher **tutorialdb** dans la liste sous le nœud **Bases de données**.


## <a name="create-a-table"></a>Créer une table

 Les étapes suivantes créent une table dans **tutorialdb** :

1. Modifiez le contexte de connexion à **tutorialdb** à l’aide de la liste déroulante dans l’éditeur de requête. 

   ![Modifier le contexte](media/quickstart-postgresql/change-context.png)

2. Collez l’instruction SQL suivante dans l’éditeur de requête et cliquez sur **Exécuter**. 

   > [!NOTE]
   > Vous pouvez ajouter cela ou remplacer la requête existante dans l’éditeur. Cliquer sur **Exécuter** exécute uniquement la requête qui est mise en surbrillance. Si rien n’est mis en surbrillance, cliquez sur **Exécuter** pour exécuter toutes les requêtes dans l’éditeur.

   ```sql
   -- Drop the table if it already exists
   DROP TABLE IF EXISTS customers;
   -- Create a new table called 'customers'
   CREATE TABLE customers(
       customer_id SERIAL PRIMARY KEY,
       name VARCHAR (50) NOT NULL,
       location VARCHAR (50) NOT NULL,
       email VARCHAR (50) NOT NULL
   );
   ```

## <a name="insert-rows"></a>Insérer des lignes

Collez l’extrait suivant dans la fenêtre de requête, puis cliquez sur **Exécuter** :

   ```sql
   -- Insert rows into table 'customers'
   INSERT INTO customers
       (customer_id, name, location, email)
    VALUES
      ( 1, 'Orlando', 'Australia', ''),
      ( 2, 'Keith', 'India', 'keith0@adventure-works.com'),
      ( 3, 'Donna', 'Germany', 'donna0@adventure-works.com'),
      ( 4, 'Janet', 'United States','janet1@adventure-works.com');
   ```

## <a name="query-the-data"></a>Interroger les données

1. Collez l’extrait suivant dans l’éditeur de requête, puis cliquez sur **Exécuter** :
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. Les résultats de la requête sont affichés :

   ![Afficher les résultats](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>Next Steps

En savoir plus sur les [scénarios disponibles pour Postgres dans Azure Data Studio.](postgres-extension.md) 