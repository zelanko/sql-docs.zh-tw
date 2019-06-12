---
title: 快速入門：連線和查詢 PostgreSQL
titleSuffix: Azure Data Studio
description: 本快速入門示範如何使用 Azure Data Studio 來連線至 PostgreSQL，然後執行查詢
ms.custom: seodec18
ms.date: 03/19/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
manager: jroth
ms.openlocfilehash: be8683ae563e4e0676f53203cb40386cf8aa4840
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778328"
---
# <a name="quickstart-connect-and-query-postgresql-using-includename-sosincludesname-sos-shortmd"></a>快速入門：使用 PostgreSQL 連線及查詢 [!INCLUDE[name-sos](../includes/name-sos-short.md)]
本快速入門示範如何使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]連接到 Postgres，並再使用 SQL 陳述式來建立資料庫*tutorialdb*並查詢它。

## <a name="prerequisites"></a>先決條件

若要完成本快速入門中，您需要[!INCLUDE[name-sos](../includes/name-sos-short.md)]，適用於 PostgreSQL 擴充功能 [！包含[名稱 sos](../includes/name-sos-short.md)，和 PostgreSQL 伺服器的存取權。

- [安裝[!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)。
- [安裝 PostgreSQL 擴充功能適用於 Azure 資料 Studio](postgres-extension.md)。
- [安裝 PostgreSQL](https://www.postgresql.org/download/)。 (或者，您可以建立 Postgres 資料庫，在雲端中使用[az postgres 向上](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli))。 

## <a name="connect-to-postgresql"></a>連線至 PostgreSQL

1. 啟動 **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** 。

2. 首次啟動[!INCLUDE[name-sos](../includes/name-sos-short.md)]**連線** 對話方塊隨即開啟。 如果**連接**對話方塊未開啟，按一下**伺服器**頁面中的**新增連線**圖示：

   ![新的 [連線] 圖示](media/quickstart-postgresql/new-connection-icon.png)

3. 在出現的表單，移至**連線類型**，然後選取**PostgreSQL**從下拉式清單。


4. 填入其餘的欄位，使用適用於 PostgreSQL 伺服器的伺服器名稱、 使用者名稱和密碼。 

   ![新的 [連線] 畫面](media/quickstart-postgresql/new-connection-screen.png)  

   | 設定       | 範例值 | 描述 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱** | localhost | 完整伺服器名稱 |
   | **使用者名稱** | postgres | 您想要登入的使用者名稱。 |
   | **密碼 (SQL 登入)** | *password* | 您正登入帳戶的密碼。 |
   | **密碼** | *檢查* | 如果您不想每次連接輸入密碼，請核取此方塊。 |
   | **資料庫名稱** | \<預設值\> | 如果您想要指定資料庫連線，請填寫這。 |
   | **伺服器群組** | \<預設值\> | 此選項可讓您將此連線指派給您所建立的特定伺服器群組。 | 
   | **名稱 （選擇性）** | *保留空白* | 此選項可讓您指定您的伺服器的易記名稱。 | 

5. 選取 [連接]  。 

成功連線之後，您的伺服器會在中開啟**伺服器**資訊看板。


## <a name="create-a-database"></a>建立資料庫

下列步驟會建立名為的資料庫**tutorialdb**:

1. 以滑鼠右鍵按一下您的 PostgreSQL 伺服器**伺服器**資訊看板，然後選取**新的查詢**。

2. 開啟查詢編輯器中，貼上這個 SQL 陳述式。

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. 從工具列中選取**執行**來執行查詢。 通知會出現在**訊息**窗格，即可顯示查詢的進度。

>[!TIP]
> 您可以使用**F5**上執行的陳述式，而不是使用鍵盤**執行**。

查詢完成後，以滑鼠右鍵按一下**資料庫**，然後選取**重新整理**若要查看**tutorialdb**下方的清單中**資料庫**節點.


## <a name="create-a-table"></a>建立資料表

 下列步驟中建立資料表**tutorialdb**:

1. 變更的連接內容**tutorialdb**使用查詢編輯器中的下拉箭號。 

   ![變更內容](media/quickstart-postgresql/change-context.png)

2. 將下列 SQL 陳述式貼到查詢編輯器，然後按一下**執行**。 

   > [!NOTE]
   > 您可以將此附加或覆寫現有的查詢編輯器 中。 按一下 **執行**執行只會反白顯示的查詢。 如果不反白顯示，按一下**執行**在編輯器中執行所有的查詢。

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

## <a name="insert-rows"></a>插入資料列

將下列程式碼片段貼到 [查詢] 視窗，然後按一下**執行**:

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

## <a name="query-the-data"></a>查詢資料

1. 將下列程式碼片段貼到查詢編輯器，然後按一下**執行**:
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. 查詢的結果會顯示：

   ![檢視結果](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>後續步驟

深入了解[案例適用於在 Azure Data Studio Postgres](postgres-extension.md)。 