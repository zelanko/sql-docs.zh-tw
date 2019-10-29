---
title: 使用 SqlDependency 偵測變更
description: 示範如何偵測查詢結果與原始接收的不同之處。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2d2c4c48a9085fa83d6104233be5f2e1c6b11318
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452242"
---
# <a name="detecting-changes-with-sqldependency"></a>使用 SqlDependency 偵測變更

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

<xref:Microsoft.Data.SqlClient.SqlDependency> 物件可以與 <xref:Microsoft.Data.SqlClient.SqlCommand> 相關聯，以偵測查詢結果與原先抓取的不同之處。 您也可以將委派指派給 `OnChange` 事件，這會在關聯的命令的結果變更時引發。 執行命令之前，您必須先將 <xref:Microsoft.Data.SqlClient.SqlDependency> 與命令建立關聯。 <xref:Microsoft.Data.SqlClient.SqlDependency> 的 `HasChanges` 屬性也可以用來判斷自從資料第一次抓取之後，查詢結果是否已經變更。

## <a name="security-considerations"></a>安全性考量

相依性基礎結構會依賴呼叫 <xref:Microsoft.Data.SqlClient.SqlDependency.Start%2A> 時開啟的 <xref:Microsoft.Data.SqlClient.SqlConnection>，以便接收基礎資料已針對指定命令變更的通知。 用戶端起始呼叫 `SqlDependency.Start` 的能力是透過使用 <xref:Microsoft.Data.SqlClient.SqlClientPermission> 和代碼啟用安全性屬性來控制。 如需詳細資訊，請參閱[啟用查詢通知](enable-query-notifications.md)。

### <a name="example"></a>範例

下列步驟說明如何宣告相依性、執行命令，並在結果集變更時收到通知：

1. 起始與伺服器的 `SqlDependency` 連線。

2. 建立 <xref:Microsoft.Data.SqlClient.SqlConnection> 和 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件，以連接到伺服器並定義 Transact-sql 語句。

3. 建立新的 `SqlDependency` 物件，或使用現有的物件，並將它系結至 `SqlCommand` 物件。 就內部而言，這會建立一個 <xref:Microsoft.Data.Sql.SqlNotificationRequest> 物件，並視需要將它系結至命令物件。 此通知要求包含可唯一識別此 `SqlDependency` 物件的內部識別碼。 如果用戶端接聽程式尚未啟用，它也會啟動。

4. 訂閱 `SqlDependency` 物件之 `OnChange` 事件的事件處理常式。

5. 使用 `SqlCommand` 物件的任何 `Execute` 方法來執行命令。 因為命令已繫結至通知物件，所以伺服器了解必須產生通知，而且佇列資訊將指向相依性佇列。

6. 停止伺服器的 `SqlDependency` 連接。

如果任何使用者後續變更基礎資料，Microsoft SQL Server 會偵測到有此類變更的暫止通知，並透過所建立的基礎 `SqlConnection`，張貼已處理並轉送至用戶端的通知。呼叫 `SqlDependency.Start`。 用戶端接聽程式會接收到失效訊息。 然後，用戶端接聽程式會找出相關聯的 `SqlDependency` 物件，並引發 `OnChange` 事件。

下列程式碼片段顯示您要用來建立範例應用程式的設計模式。

```csharp
void Initialization()
{
    // Create a dependency connection.
    SqlDependency.Start(connectionString, queueName);
}

void SomeMethod()
{
    // Assume connection is an open SqlConnection.

    // Create a new SqlCommand object.
    using (SqlCommand command=new SqlCommand(
        "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers",
        connection))
    {

        // Create a dependency and associate it with the SqlCommand.
        SqlDependency dependency=new SqlDependency(command);
        // Maintain the reference in a class member.

        // Subscribe to the SqlDependency event.
        dependency.OnChange+=new
           OnChangeEventHandler(OnDependencyChange);

        // Execute the command.
        using (SqlDataReader reader = command.ExecuteReader())
        {
            // Process the DataReader.
        }
    }
}

// Handler method
void OnDependencyChange(object sender,
   SqlNotificationEventArgs e )
{
  // Handle the event (for example, invalidate this cache entry).
}

void Termination()
{
    // Release the dependency.
    SqlDependency.Stop(connectionString, queueName);
}
```

## <a name="next-steps"></a>後續步驟
- [SQL Server 中的查詢通知](query-notifications-sql-server.md)
