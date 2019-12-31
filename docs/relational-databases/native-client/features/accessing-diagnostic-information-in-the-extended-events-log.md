---
title: 擴充事件記錄檔中的診斷資訊
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: aaa180c2-5e1a-4534-a125-507c647186ab
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f8840d746dec7dbcc4fc87d827a85cbe9c3af65
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258732"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>存取擴展事件記錄檔中的診斷資訊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  從開始[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 和資料存取追蹤（[資料存取追蹤](https://go.microsoft.com/fwlink/?LinkId=125805)）已更新，可讓您更輕鬆地從連接信號緩衝區取得連接失敗的診斷資訊，以及擴充事件記錄檔中的應用程式效能資訊。  
  
 如需讀取擴充事件記錄檔的資訊，請參閱[檢視事件工作階段資料](https://msdn.microsoft.com/library/ac742a01-2a95-42c7-b65e-ad565020dc49)。  
  
> [!NOTE]  
>  此功能僅供疑難排解及診斷使用，可能不適用稽核或安全性。  
  
## <a name="remarks"></a>備註  
 針對連接作業，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會傳送用戶端連接識別碼。 如果連線失敗，您可以存取連線通道緩衝區 ([使用連線通道緩衝區在 SQL Server 2008 中進行連線的疑難排解](https://go.microsoft.com/fwlink/?LinkId=207752))、尋找 **ClientConnectionID** 欄位，並且取得有關連線失敗的診斷資訊。 僅在發生錯誤時，才會在信號緩衝區中記錄用戶端連接識別碼。 （如果連接在傳送預先登入封包之前失敗，將不會產生用戶端連線識別碼）。用戶端連接識別碼是16位元組的 GUID。 如果在擴充的事件工作階段中，將 **client_connection_id** 動作新增至事件，您也可以在擴充的事件輸出目標中找到用戶端連接識別碼。 如果您需要進一步的診斷協助，您可以啟用資料存取追蹤並重新執行連接命令，然後觀察資料存取追蹤的 **ClientConnectionID** 欄位中是否有失敗的作業。  
  
 如果您在 Native Client 中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 ODBC，而連接成功，您可以使用**SQL_COPT_SS_CLIENT_CONNECTION_ID**屬性搭配[SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)來取得用戶端連接識別碼。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 也會傳送執行緒專屬的活動識別碼。 如果已啟動工作階段並啟用 TRACK_CAUSAILITY 選項，即可在擴充的事件工作階段中擷取活動識別碼。 如果使用中的連接發生效能問題，您可以從用戶端的資料存取追蹤中取得活動識別碼 (**ActivityID** 欄位)，然後在擴充的事件輸出中找出活動識別碼。 擴充事件中的活動識別碼為 16 位元組的 GUID (與用戶端連接識別碼的 GUID 不同)，後面附加 4 位元組的序號。 此序號表示執行緒內要求的順序，並指出執行緒的批次和 RPC 陳述式的相對排序。 啟用資料存取追蹤，並開啟資料存取追蹤組態中的 18 位元時，會選擇性地針對 SQL 批次陳述式和 RPC 要求傳送 **ActivityID**。  
  
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
 在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中，SQL Server Native Client 控制檔案 (ctrl.guid.snac11) 的內容為：  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x00000000  0   MSDADIAG.ETW  
{2DA81B52-908E-7DB6-EF81-76856BB47C4F}  0xFFFFFFFF  0   SQLNCLI11.1  
```  
  
## <a name="mof-file"></a>MOF 檔案  
 在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中，SQL Server Native Client mof 檔的內容為：  
  
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
//  SQLNCLI11.1  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1"),  
 Guid("{2DA81B52-908E-7DB6-EF81-76856BB47C4F}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1 : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1"),  
 Guid("{2DA81B53-908E-7DB6-EF81-76856BB47C4F}"),  
 DisplayName("SQLNCLI11.1"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace : Bid2Etw_SQLNCLI11_1  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1 formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace_TextA : Bid2Etw_SQLNCLI11_1_Trace  
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
 Description("SQLNCLI11.1 formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace_TextW : Bid2Etw_SQLNCLI11_1_Trace  
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
 [處理錯誤和訊息](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
