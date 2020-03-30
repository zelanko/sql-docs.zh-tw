---
title: 使用 SqlNotificationRequest 執行 SqlCommand
description: 示範如何設定 SqlCommand 物件來處理查詢通知。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: b4ec71c2bd693599106692a45f9e9aa10a63babd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896229"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>使用 SqlNotificationRequest 執行 SqlCommand

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

<xref:Microsoft.Data.SqlClient.SqlCommand> 可以設定為當資料從伺服器中擷取之後發生變更時產生通知，而且如果再次執行查詢，則結果集會不同。 這適用於您想要在伺服器上使用自訂通知佇列，或當您不想維護即時物件時的案例。

## <a name="creating-the-notification-request"></a>建立通知要求

您可以使用 <xref:Microsoft.Data.Sql.SqlNotificationRequest> 物件，藉由將其繫結至 `SqlCommand` 物件來建立通知要求。 建立要求之後，您就不再需要 `SqlNotificationRequest` 物件。 您可以查詢佇列中的任何通知，並適當地回應。 即使關閉了應用程式且隨後重新啟動，也可能會發生通知。

在具有相關聯通知的命令執行時，對原始結果集所做的任何變更，都會傳送訊息至在通知要求中設定的 SQL Server 佇列。

輪詢 SQL Server 佇列及轉譯訊息的方式，視應用程式而定。 應用程式會負責輪詢佇列並根據訊息的內容進行回應。

> [!NOTE]
> 搭配 <xref:Microsoft.Data.SqlClient.SqlDependency> 使用 SQL Server 通知要求時，請建立您自己的佇列名稱，而不是使用預設的服務名稱。

<xref:Microsoft.Data.Sql.SqlNotificationRequest> 沒有新的用戶端安全性元素。 這主要是伺服器功能，而且伺服器已建立特殊權限，使用者必須擁有該權限，才能要求通知。

### <a name="example"></a>範例

下列程式碼片段示範如何建立 <xref:Microsoft.Data.Sql.SqlNotificationRequest>，並將其與 <xref:Microsoft.Data.SqlClient.SqlCommand> 產生關聯。

```csharp
// Assume connection is an open SqlConnection.
// Create a new SqlCommand object.
SqlCommand command=new SqlCommand(
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);

// Create a SqlNotificationRequest object.
SqlNotificationRequest notificationRequest=new SqlNotificationRequest();
notificationRequest.id="NotificationID";
notificationRequest.Service="mySSBQueue";

// Associate the notification request with the command.
command.Notification=notificationRequest;
// Execute the command.
command.ExecuteReader();
// Process the DataReader.
// You can use Transact-SQL syntax to periodically poll the
// SQL Server queue to see if you have a new message.
```

## <a name="next-steps"></a>後續步驟
- [SQL Server 中的查詢通知](query-notifications-sql-server.md)
