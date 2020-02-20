---
title: ASP.NET 應用程式中的 SqlDependency
description: 示範如何使用 ASP.NET 應用程式的查詢通知。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 4c2c2d0dcc12c38cd462f0bcfe86db7bbe829dce
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75243994"
---
# <a name="sqldependency-in-an-aspnet-application"></a>ASP.NET 應用程式中的 SqlDependency

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

此節的範例示範如何利用 ASP.NET <xref:System.Web.Caching.SqlCacheDependency> 物件，間接使用 <xref:Microsoft.Data.SqlClient.SqlDependency>。 <xref:System.Web.Caching.SqlCacheDependency> 物件會使用 <xref:Microsoft.Data.SqlClient.SqlDependency> 來接聽通知，並正確更新快取。  
  
> [!NOTE]
>  此範例程式碼假設您已藉由執行[啟用查詢通知](enable-query-notifications.md)中的指令碼來啟用查詢通知。  
  
## <a name="about-the-sample-application"></a>關於範例應用程式  
此範例應用程式會使用單一 ASP.NET 網頁，在 <xref:System.Web.UI.WebControls.GridView> 控制項中顯示 **AdventureWorks** SQL Server 資料庫的產品資訊。 當頁面載入時，程式碼會將目前的時間寫入至 <xref:System.Web.UI.WebControls.Label> 控制項。 然後會定義 <xref:System.Web.Caching.SqlCacheDependency> 物件，並在 <xref:System.Web.Caching.Cache> 物件上設定屬性，以儲存快取資料長達三分鐘。 然後，程式碼會連線到資料庫並擷取資料。 當頁面載入且應用程式正在執行時，ASP.NET 將從快取中擷取資料，您可以透過注意頁面上的時間不會變更來驗證這一點。 如果監視的資料變更，ASP.NET 就會讓快取失效，並以全新的資料重新填入 `GridView` 控制項，進而更新 `Label` 控制項中顯示的時間。  
  
## <a name="creating-the-sample-application"></a>建立範例應用程式  
遵循下列步驟，以建立並執行範例應用程式：  
  
1. 建立新的 ASP.NET 網站。  
  
2. 將 <xref:System.Web.UI.WebControls.Label> 和 <xref:System.Web.UI.WebControls.GridView> 控制項新增至 Default.aspx 頁面。  
  
3. 開啟頁面的類別模組並新增下列指示詞：  
  
    ```csharp  
    using Microsoft.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. 在頁面的 `Page_Load` 事件中新增下列程式碼：  
  
    [!code-csharp[DataWorks SqlDependency_Start#1](~/../sqlclient/doc/samples/SqlDependency_Start.cs#1)]
  
5. 新增兩個協助程式方法：`GetConnectionString` 和 `GetSQL`。 定義的連接字串會使用整合式安全性。 您需要驗證所使用的帳戶具有必要的資料庫使用權限，且範例資料庫 **AdventureWorks** 已啟用通知。
  
    [!code-csharp[DataWorks SqlDependency_Start#2](~/../sqlclient/doc/samples/SqlDependency_Start.cs#2)]
  
### <a name="testing-the-application"></a>測試應用程式  
應用程式會快取 Web 表單上顯示的資料，如果沒有任何活動，則每隔三分鐘就會重新整理一次。 如果資料庫發生變更，就會立即重新整理快取。 從 Visual Studio 執行應用程式，以將頁面載入瀏覽器。 顯示的快取重新整理時間表示上次重新整理快取的時間。 等候三分鐘，然後重新整理頁面，即會導致回傳事件發生。 請注意，頁面上顯示的時間已經變更。 如果您在三分鐘內重新整理頁面，則頁面上顯示的時間將維持不變。  
  
現在，使用 Transact-SQL UPDATE 命令來更新資料庫中的資料，並重新整理頁面。 顯示的時間現在表示已使用資料庫的新資料來重新整理快取。 請注意，雖然快取已更新，但在發生回傳事件之前，頁面上顯示的時間不會變更。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 中的查詢通知](query-notifications-sql-server.md)
