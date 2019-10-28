---
title: 啟用查詢通知
description: 討論如何使用查詢通知，包括啟用和使用它們的需求。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 94b472a1fe040aa3a684d9f7b523ba09c82a651e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452229"
---
# <a name="enabling-query-notifications"></a>啟用查詢通知

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

使用查詢通知的應用程式有一組常見的需求。 您必須正確設定資料來源才能支援 SQL 查詢通知，而且使用者必須具有正確的用戶端及伺服器端權限。  
  
若要使用查詢通知，您必須：  
  
- 啟用資料庫的查詢通知。  
  
- 確定用來連接到資料庫的使用者識別碼具有必要的許可權。  
  
- 使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件來執行具有相關聯通知物件的有效 SELECT 語句，<xref:Microsoft.Data.SqlClient.SqlDependency> 或 <xref:Microsoft.Data.Sql.SqlNotificationRequest>。  
  
- 如果受監視的資料變更，請提供程式碼來處理通知。  
  
## <a name="query-notifications-requirements"></a>查詢通知需求  
查詢通知僅支援符合特定需求清單的 SELECT 語句。 下表提供 SQL Server 線上叢書中 Service Broker 和查詢通知檔的連結。  
  
**SQL Server 文件**  
  
- [為通知建立查詢](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Service Broker 的安全性考量](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [安全性與保護 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Notification Services 的安全性考量](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [查詢通知權限](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Service Broker 的國際性考量](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [解決方案設計考量 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Service Broker 開發人員資訊中心](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [開發人員手冊 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>啟用查詢通知以執行範例程式碼  
若要透過使用 SQL Server Management Studio，在 **AdventureWorks** 資料庫上啟用 Service Broker，請執行下列 Transact-SQL 陳述式：  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
若要讓查詢通知範例正確執行，必須在資料庫伺服器上執行下列 Transact-sql 語句。  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>查詢通知許可權  
執行要求通知之命令的使用者，必須擁有伺服器的訂閱查詢通知資料庫許可權。  
  
在部分信任狀況下執行的用戶端程式代碼需要 <xref:Microsoft.Data.SqlClient.SqlClientPermission>。  
  
下列程式碼會建立 <xref:Microsoft.Data.SqlClient.SqlClientPermission> 物件，並將 <xref:System.Security.Permissions.PermissionState> 設定為 <xref:System.Security.Permissions.PermissionState.Unrestricted>。 如果在呼叫堆疊中較高的所有呼叫端都尚未被授與許可權，<xref:System.Security.CodeAccessPermission.Demand%2A> 將會在執行時間強制執行 <xref:System.Security.SecurityException>。  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>選擇通知物件  
查詢通知 API 提供兩個物件來處理通知：<xref:Microsoft.Data.SqlClient.SqlDependency> 和 <xref:Microsoft.Data.Sql.SqlNotificationRequest>。
  
### <a name="using-sqldependency"></a>使用 SqlDependency  
若要使用 <xref:Microsoft.Data.SqlClient.SqlDependency>，所使用的 SQL Server 資料庫必須啟用 Service Broker，且使用者必須具有接收通知的使用權限。 系統會預先定義 Service Broker 物件（例如通知佇列）。  
  
此外，<xref:Microsoft.Data.SqlClient.SqlDependency> 會自動啟動背景工作執行緒，以便在張貼到佇列時處理通知;它也會剖析 Service Broker 訊息，將資訊公開為事件引數資料。 <xref:Microsoft.Data.SqlClient.SqlDependency> 必須藉由呼叫 `Start` 方法來初始化，以便建立對資料庫的相依性。 這是一種靜態方法，只需要在應用程式初始化期間針對每個需要的資料庫連接呼叫一次。 對於每個進行的相依性連線，`Stop` 方法應該在應用程式終止時呼叫。  
  
### <a name="using-sqlnotificationrequest"></a>使用 SqlNotificationRequest  
相反地，<xref:Microsoft.Data.Sql.SqlNotificationRequest> 需要您自行執行整個接聽基礎結構。 此外，必須定義所有支援的 Service Broker 物件，例如佇列、服務和佇列所支援的訊息類型。 如果您的應用程式需要特殊的通知訊息或通知行為，或如果您的應用程式是較大 Service Broker 應用程式的一部分，則此手動方法很有用。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 中的查詢通知](query-notifications-sql-server.md)
