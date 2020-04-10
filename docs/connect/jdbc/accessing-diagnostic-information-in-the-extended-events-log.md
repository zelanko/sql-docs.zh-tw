---
title: 存取擴充事件記錄檔中的診斷資訊 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5f8086c0ccb161bb94e1b878736b55ee306fe4b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920351"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>存取擴充事件記錄檔中的診斷資訊
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  在 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 中，已經更新追蹤 ([追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md))，讓您能夠更輕易地將用戶端事件與伺服器連線通道緩衝區中的診斷資訊 (例如連線失敗) 以及擴充事件記錄檔中的應用程式效能資訊相互關聯。 如需讀取擴充事件記錄檔的資訊，請參閱[檢視事件工作階段資料](https://msdn.microsoft.com/library/hh710068(SQL.110).aspx)。  
  
## <a name="details"></a>詳細資料  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會針對連線作業傳送用戶端連線識別碼。 如果連線失敗，您可以存取連線通道緩衝區 ([使用連線通道緩衝區在 SQL Server 2008 中進行連線的疑難排解](https://go.microsoft.com/fwlink/?LinkId=207752))、尋找 **ClientConnectionID** 欄位，並且取得有關連線失敗的診斷資訊。 僅在發生錯誤時，才會在信號緩衝區中記錄用戶端連接識別碼。 (如果在傳送登入前封包之前連線失敗，則不會產生用戶端連線識別碼。)用戶端連接識別碼是 16 位元組的 GUID。 如果在擴充事件工作階段中將 **client_connection_id** 動作新增至事件，您也可在擴充事件目標輸出中找到用戶端連線識別碼。 如果您需要進一步的用戶端驅動程式診斷協助，則可以啟用追蹤，並重新執行連線命令，以觀察追蹤中的 **ClientConnectionID** 欄位。  
  
 您可以使用 [ISQLServerConnection 介面](../../connect/jdbc/reference/isqlserverconnection-interface.md)，以程式設計方式取得用戶端連線識別碼。 連接識別碼也會出現在任何與連接有關的例外狀況中。  
  
 發生連線錯誤時，伺服器內建診斷 (BID) 追蹤資訊和連線通道緩衝區中的用戶端連線識別碼可協助您將用戶端連線與伺服器連線相互關聯。 如需伺服器 BID 追蹤的詳細資訊，請參閱[資料存取追蹤](https://go.microsoft.com/fwlink/?LinkId=125805)。 請注意，資料存取追蹤文章也包含資料存取追蹤的相關資訊，但是這些資訊不適用於 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]；如需使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 執行資料存取追蹤的資訊，請參閱[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)。  
  
 JDBC 驅動程式也會傳送執行緒特有的活動識別碼。 如果已啟動工作階段並啟用 TRACK_CAUSAILITY 選項，即可在擴充的事件工作階段中擷取活動識別碼。 如果使用中的連接發生效能問題，您可以從用戶端的追蹤中取得活動識別碼 (ActivityID 欄位)，然後在擴充事件輸出中找出活動識別碼。 擴充事件中的活動識別碼是附加 4 位元組序號的 16 位元組 GUID (與用戶端連線識別碼的 GUID 不同)。 此序號代表要求在執行緒中的順序。 系統會針對 SQL 批次陳述式和 RPC 要求傳送 ActivityId。 若要將 ActivityId 傳送至伺服器，您必須先在 Logging.Properties 檔案中指定下列機碼/值組：  
  
```
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 `on` (區分大小寫) 以外的任何值都會停用傳送 ActivityId。  
  
 如需詳細資訊，請參閱[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)。 這個追蹤旗標會搭配對應的 JDBC 物件記錄器使用，以便決定是否要在 JDBC 驅動程式中追蹤和傳送 ActivityId。 除了更新 Logging.Properties 檔案以外，您也必須將記錄器 com.microsoft.sqlserver.jdbc 啟用成 FINER 或更高設定。 如果您想要針對特定類別所提出的要求，將 ActivityId 傳送至伺服器，就必須將對應的類別記錄器啟用成 FINER 或 FINEST。 例如，如果類別是 SQLServerStatement，請啟用記錄器 com.microsoft.sqlserver.jdbc.SQLServerStatement。  
  
 下列範例會使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來啟動擴充事件工作階段，此工作階段將儲存在通道緩衝區中，並且針對 RPC 和批次作業記錄用戶端所傳送的活動識別碼：  
  
```sql
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
  
  
