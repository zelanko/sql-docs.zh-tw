---
title: SQL Server Service Broker | Microsoft Docs
description: 了解 Service Broker。 查看其如何提供在 SQL Server 資料庫引擎與 Azure SQL 受控執行個體中進行傳訊的原生支援。
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.SSBMSGTYPEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBCONTRACTPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBQUEUEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBREMSVCBINDPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBROUTEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBPRIORITYPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBSERVICEPROPERTIES.GENERAL.F1
helpviewer_keywords:
- Broker See Service Broker
- SQL Server Service Broker
- Service Broker
ms.assetid: 8b8b3b57-fd46-44de-9a4e-e3a8e3999c1e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017
ms.openlocfilehash: cf37305f773f4b417ed3cac1bc5a31ad8d910505
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465699"
---
# <a name="service-broker"></a>Service Broker
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSB](../../includes/sssb-md.md)] 提供在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 與 [Azure SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance-index)中進行傳訊及佇列處理的原生支援。 開發人員能夠輕易地建立使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 元件的複雜應用程式，以便在不同資料庫間進行通訊，並建置可靠的分散式應用程式。  
  
## <a name="when-to-use-service-broker"></a>使用 Service Broker 的時機

 使用 Service Broker 元件來實作資料庫內原生的非同步訊息處理功能。 使用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的應用程式開發人員不需要撰寫複雜的通訊和傳訊間隔程式，即可將資料工作負載分散在多個資料庫。 Service Broker 可減少開發和測試工作，因為 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會處理對話內容中的通訊路徑。 此外，還可提升效能。 例如，支援網站的前端資料庫可記錄資訊，並將具有大量處理序的工作傳送到後端資料庫的佇列中。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 可確保所有工作都在交易內容中管理，以確保可靠性和技術一致性。  
  
## <a name="overview"></a>概觀

  Service Broker 是一種訊息傳遞架構，可讓您建立資料庫內原生的服務導向應用程式。 不同於傳統查詢處理功能 (其會在查詢生命週期過程中，從資料表持續讀取資料並加以處理)，在服務導向的應用程式中，您的資料庫服務會交換訊息。 每個服務都有一個佇列，訊息在處理之前均放置於其中。
  
![Service Broker](media/service-broker.png)
  
  佇列中的訊息可以使用 Transact-SQL `RECEIVE` 命令，或透過每當訊息抵達佇列時將呼叫的啟用程序來擷取。
  
### <a name="creating-services"></a>建立服務
 
  資料庫服務會使用 [CREATE SERVICE](../../t-sql/statements/create-service-transact-sql.md) Transact SQL 陳述式來建立。 服務可以使用 [CREATE QUEUE](../../t-sql/statements/create-queue-transact-sql.md) 陳述式來與訊息佇列建立產生關聯：
  
```sql
CREATE QUEUE dbo.ExpenseQueue;
GO
CREATE SERVICE ExpensesService
    ON QUEUE dbo.ExpenseQueue; 
```

### <a name="sending-messages"></a>傳送訊息
  
  訊息會使用 [SEND](../../t-sql/statements/send-transact-sql.md) Transact-SQL 陳述式，在服務之間的對話上進行傳送。 對話是使用 `BEGIN DIALOG` Transact-SQL 陳述式，在服務之間建立的通訊通道。 
  
```sql
DECLARE @dialog_handle UNIQUEIDENTIFIER;

BEGIN DIALOG @dialog_handle  
FROM SERVICE ExpensesClient  
TO SERVICE 'ExpensesService';  
  
SEND ON CONVERSATION @dialog_handle (@Message) ;  
```
   訊息將傳送至 `ExpenssesService` 並放置於 `dbo.ExpenseQueue`。 因為沒有任何與此佇列相關聯的啟用程序，所以，訊息將保留於佇列中，直到有人讀取它為止。

### <a name="processing-messages"></a>處理訊息

   放置於佇列的訊息均可使用標準的 `SELECT` 查詢來選取。 `SELECT` 陳述式將不會修改佇列和移除訊息。 若要從佇列中讀取及提取訊息，您可以使用 [RECEIVE](../../t-sql/statements/receive-transact-sql.md) Transact-SQL 陳述式。

```sql
RECEIVE conversation_handle, message_type_name, message_body  
FROM ExpenseQueue; 
```

  一旦您處理來自佇列的所有訊息之後，您應該使用 [END CONVERSATION](../../t-sql/statements/end-conversation-transact-sql.md) Transact-SQL 陳述式來關閉對話。

## <a name="where-is-the-documentation-for-service-broker"></a>Service Broker 的文件集在哪裡？  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的參考文件集包含在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 文件集內。 此參考文件集包含下列章節：  
  
-   [資料定義語言 &#40;DDL&#41; 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/statements.md)，適用 CREATE、ALTER 和 DROP 陳述式  
  
-   [Service Broker 陳述式](../../t-sql/statements/statements.md)  
  
-   [Service Broker 目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)  
  
-   [Service Broker 相關的動態管理檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
-   [ssbdiagnose 公用程式 &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
 請參閱＜ [舊版文件集](/previous-versions/sql/sql-server-2008-r2/bb522893(v=sql.105)) ＞，了解 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 概念及開發和管理工作。 此文件集未在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 文件集中重製，因為 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 中只有少數 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的變更。  
  
## <a name="whats-new-in-service-broker"></a>Service Broker 的新功能  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]並無導入重大變更。  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中導入了下列變更。  

### <a name="service-broker-and-azure-sql-managed-instance"></a>Service Broker 與 Azure SQL 受控執行個體

- 不支援跨執行個體服務代理程式 
 - `sys.routes` - 必要條件：從 sys.routes 選取位址。 位址在每個路由上都必須是 LOCAL。 請參閱 [sys.routes](../../relational-databases/system-catalog-views/sys-routes-transact-sql.md)。
 - `CREATE ROUTE` - 您只能使用 `LOCAL` 的 `ADDRESS` 來執行 `CREATE ROUTE`。 請參閱 [CREATE ROUTE](../../t-sql/statements/create-route-transact-sql.md)。
 - `ALTER ROUTE` 無法使用 `ALTER ROUTE` 來搭配 `LOCAL` 以外的 `ADDRESS`。 請參閱 [ALTER ROUTE](../../t-sql/statements/alter-route-transact-sql.md)。  
  
### <a name="messages-can-be-sent-to-multiple-target-services-multicast"></a>訊息可以傳送至多個目標服務 (多點傳送)  
 [SEND &#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md) 陳述式的語法已延伸，可透過支援多個交談控制代碼進行多點傳送。  
  
### <a name="queues-expose-the-message-enqueued-time"></a>佇列會公開訊息加入佇列的時間  
 佇列包含一個新的資料行 **message_enqueue_time**，其中顯示訊息已在佇列中的時間。  
  
### <a name="poison-message-handling-can-be-disabled"></a>有害訊息處理可以停用  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md) 和 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md) 陳述式現在能夠藉由加入子句 `POISON_MESSAGE_HANDLING (STATUS = ON | OFF)` 的方式啟用或停用有害訊息處理。 目錄檢視 **sys.service_queues** 現在包含 **is_poison_message_handling_enabled** 資料行，用來指出有害訊息為啟用或停用狀態。  
  
### <a name="always-on-support-in-service-broker"></a>Service Broker 中的 AlwaysOn 支援  
 如需詳細資訊，請參閱 [Service Broker 與 AlwaysOn 可用性群組 (SQL Server)](../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)。  
  
  
## <a name="next-steps"></a>後續步驟

Service Broker 最常見的用法是[事件通知](../../relational-databases/service-broker/event-notifications.md)。 了解如何[實作事件通知](../../relational-databases/service-broker/implement-event-notifications.md)、[設定安全性對話方塊](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)，或[取得更多資訊](../../relational-databases/service-broker/get-information-about-event-notifications.md)。