---
title: SQL Server 中的查詢通知
description: 描述當資料變更時，.NET 應用程式可以如何要求 SQL Server 的通知。
ms.date: 08/15/2019
ms.assetid: 0f0ba1a1-3180-4af8-87f7-c795dc8f8f55
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d47241e3656e3ca7b4f5ea0eebe9f2cc8b571bf6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452077"
---
# <a name="query-notifications-in-sql-server"></a>SQL Server 中的查詢通知

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

查詢通知是根據 Service Broker 基礎結構而建置，可讓應用程式在資料變更時收到通知。 此功能對於從資料庫中提供資訊快取的應用程式 (如 Web 應用程式)，及需要在來源資料變更時收到通知的應用程式來說非常有用。  
  
有三種方式可使用 ADO.NET 來執行查詢通知：  
  
- 低層級的執行是由公開伺服器端功能的 `SqlNotificationRequest` 類別所提供，可讓您以通知要求執行命令。  
  
- 高階執行是由 `SqlDependency` 類別所提供，這是一個類別，可在來源應用程式與 SQL Server 之間提供高階的通知功能抽象概念，讓您可以使用相依性來偵測伺服器中的變更。 在多數情況下，對於使用 Microsoft SqlClient Data Provider for SQL Server 的受控用戶端應用程式，這是利用 SQL Server 通知功能最簡單、有效的方式。  
  
- 此外，使用 ASP.NET 2.0 或更新版本建置的 Web 應用程式可以使用 `SqlCacheDependency` Helper 類別。  
  
查詢通知會用於需要重新整理顯示或快取以回應基礎資料變更的應用程式。 Microsoft SQL Server 可讓 .NET 應用程式傳送命令至 SQL Server，並要求當執行相同命令而產生與最初擷取的不同結果集時，就產生通知。 在伺服器所產生的通知會透過佇列傳送，以供稍後處理。  
  
您可以設定 SELECT 和 EXECUTE 語句的通知。 使用 EXECUTE 語句時，SQL Server 會為執行的命令註冊通知，而不是執行語句本身。 此命令必須符合 SELECT 陳述式的需求和限制。 當註冊通知的命令包含多個陳述式時，資料庫引擎會為批次中的每個陳述式建立一個通知。  
  
如果您所開發的應用程式在資料變更時需擁有可靠的次秒通知，請查看**高效的查詢通知策略規劃**和**查詢通知的替代方案**這兩節，其屬於《SQL Server 線上叢書》的[通知規劃](https://go.microsoft.com/fwlink/?LinkId=211984)主題。 如需有關查詢通知和 SQL Server Service Broker 的詳細資訊，請參閱下列連結，以取得 SQL Server 線上叢書中的主題。  
  
**SQL Server 文件**  
  
- [使用查詢通知](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms175110(v=sql.105))  
  
- [為通知建立查詢](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [開發 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522889(v=sql.105))  
  
- [Service Broker 開發人員資訊中心](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [開發人員手冊 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="in-this-section"></a>本節內容  
[啟用查詢通知](enable-query-notifications.md)  
討論如何使用查詢通知，包括啟用和使用它們的需求。  
  
[ASP.NET 應用程式中的 SqlDependency](sqldependency-aspnet-app.md)  
示範如何使用 ASP.NET 應用程式中的查詢通知。  
  
[使用 SqlDependency 偵測變更](detect-changes-sqldependency.md)  
示範如何偵測查詢結果與原始接收的不同之處。  
  
[使用 SqlNotificationRequest 執行 SqlCommand](sqlcommand-execution-sqlnotificationrequest.md)  
示範如何設定 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件來處理查詢通知。  
  
## <a name="reference"></a>參考  
<xref:Microsoft.Data.Sql.SqlNotificationRequest>  
描述 <xref:Microsoft.Data.Sql.SqlNotificationRequest> 類別及其所有成員。  
  
<xref:Microsoft.Data.SqlClient.SqlDependency>  
描述 <xref:Microsoft.Data.SqlClient.SqlDependency> 類別及其所有成員。  
  
<xref:System.Web.Caching.SqlCacheDependency>  
描述 <xref:System.Web.Caching.SqlCacheDependency> 類別及其所有成員。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
