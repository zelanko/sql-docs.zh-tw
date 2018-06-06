---
title: 存取擴充的事件記錄檔中的診斷資訊 |Microsoft 文件
description: 追蹤適用於 SQL Server 的 OLE DB 驅動程式，以及存取擴充的事件記錄檔中的診斷資訊
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 255daa268cb3b8aeaee0e371052ae8af01241f72
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>存取擴展事件記錄檔中的診斷資訊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  從開始[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，OLE DB 驅動程式的 SQL Server 和資料存取追蹤 ([資料存取追蹤](http://go.microsoft.com/fwlink/?LinkId=125805)) 已更新為更輕鬆地從連接信號緩衝區取得有關連接失敗的診斷資訊並從擴充的事件記錄檔的應用程式效能資訊。  
  
 如需有關讀取擴充的事件記錄檔的詳細資訊，請參閱[檢視事件工作階段資料](../../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)。 

  
> [!NOTE]  
>  此功能僅供疑難排解及診斷使用，可能不適用稽核或安全性。  
  
## <a name="remarks"></a>備註  
 OLE DB 驅動程式的 SQL Server 會針對連接作業傳送用戶端連接識別碼。 如果連接失敗，您可以存取連接信號緩衝區 ([連接 SQL Server 2008 中與連接信號緩衝區疑難排解](http://go.microsoft.com/fwlink/?LinkId=207752))，並尋找**ClientConnectionID**欄位和取得有關連接失敗的診斷資訊。 僅在發生錯誤時，才會在信號緩衝區中記錄用戶端連接識別碼。 (如果在傳送登入前封包之前連接失敗，則不會產生用戶端連接識別碼。)用戶端連接識別碼是 16 位元組的 GUID。 您也可以找到用戶端連接識別碼，在擴充的事件輸出目標，，如果**client_connection_id**動作已加入至事件中的擴充的事件工作階段。 您可以啟用資料存取追蹤並重新執行連接命令，並觀察**ClientConnectionID**欄位在資料存取追蹤失敗的作業中，如果您需要進一步診斷協助。  
   
  
 OLE DB 驅動程式的 SQL Server 也會傳送執行緒專屬的活動識別碼。 如果已啟動工作階段並啟用 TRACK_CAUSAILITY 選項，即可在擴充的事件工作階段中擷取活動識別碼。 如需使用中連線的效能問題，您可以從用戶端的資料存取追蹤取得活動識別碼 (**ActivityID**欄位)，然後在擴充的事件 」 輸出中尋找活動識別碼。 擴充事件中的活動識別碼為 16 位元組的 GUID (與用戶端連接識別碼的 GUID 不同)，後面附加 4 位元組的序號。 此序號表示執行緒內要求的順序，並指出執行緒的批次和 RPC 陳述式的相對排序。 **ActivityID**會在上啟用資料存取追蹤和資料存取追蹤組態字詞中的 18 位元開啟時選擇性地針對 SQL 批次陳述式和 RPC 要求傳送。  
  
 以下是使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 啟動擴充事件工作階段的範例，該工作階段會儲存在信號緩衝區中，並且會記錄從 RPC 和批次作業上之用戶端傳送的活動識別碼。  
  
```  
create event session MySession on server   
add event connectivity_ring_buffer_recorded,   
add event sql_statement_starting (action (client_connection_id)),   
add event sql_statement_completed (action (client_connection_id)),   
add event rpc_starting (action (client_connection_id)),   
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
  
```  
  
## <a name="control-file"></a>控制檔案  
 SQL Server 控制檔案 (ctrl.guid) OLE DB 驅動程式的內容是：  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x630ff  0   MSDADIAG.ETW
{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}  0x630ff  0   MSOLEDBSQL.1  
```  
  
## <a name="mof-file"></a>MOF 檔案  
 SQL Server mof 檔案，OLE DB 驅動程式的內容是：  
  
```  
#pragma classflags("forceupdate")  
#pragma namespace ("\\\\.\\Root\\WMI")  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  MSDADIAG.ETW  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F3-3CC6-0B9C-6651-9649CCE5C752}"),  
 DisplayName("msdadiag"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace : Bid2Etw_MSDADIAG_ETW  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextA : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextW : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  MSOLEDBSQL.1  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1 : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59D-D3E8-9684-AEAC-B214EFD91B31}"),  
 DisplayName("MSOLEDBSQL.1"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace : Bid2Etw_MSOLEDBSQL_1  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1 formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextA : Bid2Etw_MSOLEDBSQL_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1 formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextW : Bid2Etw_MSOLEDBSQL_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
```  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤](../../oledb/ole-db-errors/errors.md)  
  
  
