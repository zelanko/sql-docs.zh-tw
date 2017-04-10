---
title: "事件通知 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "事件通知, 關於"
  - "事件 [SQL Server], 通知"
ms.assetid: 4da73ca1-6c06-4e96-8ab8-2ecba30b6c86
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# 事件通知
  事件通知會傳送事件的詳細資訊給 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服務。 事件通知會將這些事件的資訊傳送給 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服務，以回應各種 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 資料定義語言 (DDL) 陳述式和 SQL 追蹤事件。  
  
 事件通知可用來執行下列工作：  
  
-   記錄和檢閱發生在資料庫的變更或活動。  
  
-   執行動作以非同步而不是同步的方式來回應事件。  
  
 事件通知可提供程式設計替代方案給 DDL 觸發程序和 SQL 追蹤。  
  
## 事件通知優點  
 事件通知會以非同步方式在交易範圍以外執行。 因此，與 DDL 觸發程序不同的是，事件通知可在資料庫應用程式中使用，以便回應未使用立即交易所定義之資源的事件。  
  
 與 SQL 追蹤不同的是，事件通知可用來在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體內執行動作，以回應 SQL 追蹤事件。  
  
 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起執行的應用程式可使用事件資料來追蹤進度和下決定。 例如，下列事件通知會在每次於 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中發出 `ALTER TABLE` 陳述式時，將通知傳送給特定服務。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE '//Adventure-Works.com/ArchiveService' ,  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
## 事件通知概念  
 建立事件通知時，會在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 執行個體與您所指定的目標服務之間開啟一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交談。 交談通常會維持開啟狀態，只要事件通知是以伺服器執行個體上的物件存在即可。 在某些錯誤的例子中，可以在卸除事件通知之間先關閉交談。 這些交談永遠不會在事件通知之間共用。 每個事件通知都有自己獨佔的交談。 明確地結束交談可防止目標服務再收到訊息，而且在下次事件通知引發之前都不會再重新開啟交談。  
  
 事件資訊是以 **xml** 類型的變數傳遞至 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服務，它提供事件發生時的詳細資訊、受影響之資料庫物件的詳細資訊、相關的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次陳述式以及其他資訊。 如需事件通知所產生之 XML 結構描述的詳細資訊，請參閱 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)。  
  
### 事件通知與 觸發程序  
 下表比較觸發程序和事件通知的異同。  
  
|觸發程序|事件通知|  
|--------------|-------------------------|  
|DML 觸發程序回應資料管理語言 (DML) 事件。 DDL 觸發程序回應資料定義語言 (DDL) 事件。|事件通知可回應 DDL 事件和 SQL 追蹤事件的子集。|  
|觸發程序可以執行 Transact-SQL 或 Common Language Runtime (CLR) Managed 程式碼。|事件通知不會執行程式碼。 相反的，它們可以傳送 **xml** 訊息給 Service Broker 服務。|  
|觸發程序會在引發它們的交易範圍內同步處理觸發程序。|事件通知可以非同步處理，而且不會在引發它們的交易範圍中執行。|  
|觸發程序的取用者與引發它的事件緊密繫結在一起。|事件通知的取用者與引發它的事件分離。|  
|觸發程序必須在本機伺服器上處理。|事件通知可以在遠端伺服器上處理。|  
|觸發程序是可以回復的。|事件通知是無法回復的。|  
|DML 觸發程序名稱是由結構描述限定範圍。 DML 觸發程序名稱是以資料庫或伺服器限定範圍。|事件通知名稱是以伺服器或資料庫限定範圍。 在 QUEUE_ACTIVATION 事件上的事件通知是限定成特定的佇列。|  
|DML 觸發程序是由套用觸發程序的資料表之相同擁有者所擁有。|佇列上的事件通知擁有者，有可能與套用事件通知的物件具有不同的擁有者。|  
|觸發程序支援 EXECUTE AS 子句。|事件通知不支援 EXECUTE AS 子句。|  
|DDL 觸發程序的事件資訊可以使用 EVENTDATA 函數來擷取，該函數會傳回 **xml** 資料類型。|事件通知會傳送 **xml** 事件資訊給 Service Broker 服務。 資訊將格式化成與 EVENTDATA 函數相同的結構描述。|  
|與觸發程序相關的中繼資料可在 **sys.triggers** 與 **sys.server_triggers** 目錄檢視中找到。|與事件通知相關的中繼資料可在 **sys.event_notifications** 與 **sys.server_event_notifications** 目錄檢視中找到。|  
  
### 事件通知與 SQL 追蹤  
 下表比較使用事件通知和 SQL 追蹤來監督伺服器事件的異同。  
  
|SQL 追蹤|事件通知|  
|---------------|-------------------------|  
|SQL 追蹤不會產生與交易關聯的效能負擔。 資料的封裝很有效率。|建立 XML 格式事件資料與傳送事件通知有相關聯的效能負擔。|  
|SQL 追蹤可以監督任何追蹤事件類別。|事件通知可以監督追蹤事件類別的子集，以及所有資料定義語言 (DDL) 事件。|  
|您可以自訂在追蹤事件中要產生哪些資料行。|會修復事件通知所傳回的 XML 格式事件資料之結構描述。|  
|不論 DDL 陳述式是否已回復，永遠都會產生 DDL 所產生的追蹤事件。|如果在對應 DDL 陳述式中的事件已回復，就不會引發事件通知。|  
|管理追蹤事件資料的中繼流程，將需要擴展和管理追蹤檔案或追蹤資料表。|事件通知資料的中繼管理是透過 Service Broker 佇列自動完成。|  
|每次重新啟動伺服器時都必須重新啟動追蹤。|在註冊後，事件通知會持續存在於伺服器週期中並已交易。|  
|在初始化後，就無法控制追蹤的引發。 停止時間和篩選時間可用來指定初始化它們的時間。 是透過輪詢對應追蹤檔案來存取追蹤。|可以針對收到事件通知所產生的訊息之佇列，使用 WAITFOR 陳述式來控制事件通知。 可以透過輪詢佇列來存取它們。|  
|ALTER TRACE 是建立追蹤所需的基本權限。 在對應電腦上建立追蹤檔案的權限也是必要的。|基本權限是視建立事件通知的類型而定。 在對應佇列上也需要 RECEIVE 權限。|  
|可以遠端接收追蹤。|可以遠端接收事件通知。|  
|追蹤事件是使用系統預存程序來實作。|事件通知是使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssSB](../../includes/sssb-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的組合來實作。|  
|透過查詢對應追蹤資料表、剖析追蹤檔案或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件 (SMO) 的 TraceReader Class，就可使用程式設計的方式來存取追蹤事件的資料。|透過針對 XML 格式的事件資料發出 XQuery，或使用 SMO Event 類別，以程式設計方式來存取事件資料。|  
  
## 事件通知工作  
  
|工作|主題|  
|----------|-----------|  
|描述如何建立及實作事件通知。|[實作事件通知](../../relational-databases/service-broker/implement-event-notifications.md)|  
|描述如何針對傳送訊息到遠端伺服器上 Service Broker 的事件通知，設定 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對話安全性。|[設定事件通知的對話安全性](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)|  
|描述如何傳回有關事件通知的詳細資訊。|[取得事件通知詳細資訊](../../relational-databases/service-broker/get-information-about-event-notifications.md)|  
  
## 另請參閱  
 [DDL 觸發程序](../../relational-databases/triggers/ddl-triggers.md)   
 [DML 觸發程序](../../relational-databases/triggers/dml-triggers.md)   
 [SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)  
  
  