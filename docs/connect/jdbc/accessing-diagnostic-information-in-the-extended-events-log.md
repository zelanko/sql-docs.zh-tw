---
title: "存取擴充的事件記錄檔中的診斷資訊 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e6dfbd857905f0c0f444c44a9c9eb9813cc32ab2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>存取擴展事件記錄檔中的診斷資訊
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  在[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]，追蹤 ([追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)) 已經更新，以方便您更輕鬆地將用戶端事件與診斷資訊，例如連接失敗，伺服器的連接性信號相互關聯緩衝區與應用程式中的效能資訊的擴充的事件記錄檔。 如需有關讀取擴充的事件記錄檔的詳細資訊，請參閱[檢視事件工作階段資料](http://msdn.microsoft.com/library/hh710068(SQL.110).aspx)。  
  
## <a name="details"></a>詳細資料  
 針對連接作業[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]會傳送用戶端連接識別碼。 如果連接失敗，您可以存取連接信號緩衝區 ([連接 SQL Server 2008 中與連接信號緩衝區疑難排解](http://go.microsoft.com/fwlink/?LinkId=207752))，並尋找**ClientConnectionID**欄位和取得有關連接失敗的診斷資訊。 僅在發生錯誤時，才會在信號緩衝區中記錄用戶端連接識別碼。 (如果在傳送登入前封包之前連接失敗，則不會產生用戶端連接識別碼。)用戶端連接識別碼是 16 位元組的 GUID。 您也可以找到用戶端連接識別碼在擴充的事件目標輸出中，如果**client_connection_id**動作已加入至事件中的擴充的事件工作階段。 您可以啟用追蹤和重新執行連接命令，並觀察**ClientConnectionID**欄位在追蹤中，如果您需要進一步的用戶端驅動程式診斷協助。  
  
 您可以取得用戶端連接識別碼，以程式設計方式利用[ISQLServerConnection 介面](../../connect/jdbc/reference/isqlserverconnection-interface.md)。 連接識別碼也會出現在任何與連接有關的例外狀況中。  
  
 發生連接錯誤時，伺服器 BID 追蹤資訊和連接性信號緩衝區中的用戶端連接識別碼可協助您將用戶端連接與伺服器連接相互關聯。 如需有關 BID 追蹤在伺服器上，請參閱 <<c0> [ 資料存取追蹤](http://go.microsoft.com/fwlink/?LinkId=125805)。 請注意，資料存取追蹤文章也包含有關執行資料存取追蹤，而不會套用至[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]; 請參閱[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)進行資料存取追蹤使用的資訊[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 JDBC 驅動程式也會傳送執行緒特有的活動識別碼。 如果已啟動工作階段並啟用 TRACK_CAUSAILITY 選項，即可在擴充的事件工作階段中擷取活動識別碼。 如果使用中的連接發生效能問題，您可以從用戶端的追蹤中取得活動識別碼 (ActivityID 欄位)，然後在擴充事件輸出中找出活動識別碼。 擴充事件中的活動識別碼是附加了四位元組序號的 16 位元組 GUID (與用戶端連接識別碼的 GUID 不同)。 此序號代表要求在執行緒中的順序。 系統會針對 SQL 批次陳述式和 RPC 要求傳送 ActivityId。 若要將 ActivityId 傳送至伺服器，您必須先在 Logging.Properties 檔案中指定下列機碼/值組：  
  
```  
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 以外的任何值`on`（區分大小寫） 將會停用傳送 ActivityId。  
  
 如需詳細資訊，請參閱[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)。 這個追蹤旗標會搭配對應的 JDBC 物件記錄器使用，以便決定是否要在 JDBC 驅動程式中追蹤和傳送 ActivityId。 除了更新 Logging.Properties 檔案以外，您也必須將記錄器 com.microsoft.sqlserver.jdbc 啟用成 FINER 或更高設定。 如果您想要針對特定類別所提出的要求，將 ActivityId 傳送至伺服器，就必須將對應的類別記錄器啟用成 FINER 或 FINEST。 例如，如果類別是 SQLServerStatement，請啟用記錄器 com.microsoft.sqlserver.jdbc.SQLServerStatement。  
  
 以下是範例會使用[!INCLUDE[tsql](../../includes/tsql_md.md)]從 RPC 和批次作業上的用戶端傳送到啟動擴充的事件工作階段，將儲存在信號緩衝區，並將記錄的活動識別碼：  
  
```  
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>另請參閱  
 [診斷 JDBC 驅動程式的問題](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  

