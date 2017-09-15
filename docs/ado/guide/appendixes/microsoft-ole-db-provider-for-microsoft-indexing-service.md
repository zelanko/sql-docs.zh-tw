---
title: "Microsoft OLE DB Provider for Microsoft 索引服務 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2303810eb0856db07b096927559f2db18ce29838
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Microsoft OLE DB Provider for Microsoft 索引服務概觀
Microsoft OLE DB Provider for Microsoft 索引服務提供以程式設計方式唯讀存取檔案系統和 Web 資料由 Microsoft 索引服務編製索引。 ADO 應用程式可以發出 SQL 查詢來擷取內容和檔案屬性資訊。

 提供者是無限制執行緒，啟用 UNICODE。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到此提供者，設定**提供者 =**引數[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性：

```
MSIDXS
```

 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性會傳回這個字串以及。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串是：

```
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 字串，包含這些關鍵字：

|關鍵字|Description|
|-------------|-----------------|
|**提供者**|指定 OLE DB Provider for Microsoft 索引服務。 一般而言，這是唯一的連接字串中指定的關鍵字。|
|**資料來源**|指定的索引服務類別目錄名稱。 如果未指定此關鍵字，系統會使用預設目錄。|
|**地區設定識別碼**|指定唯一 32 位元數字 （例如，1033年），指定與使用者的語言喜好設定。 如果未指定此關鍵字，則會使用預設系統地區設定識別碼。|

## <a name="command-text"></a>命令文字
 索引服務 SQL 查詢語法組成 SQL 92 延伸**選取**陳述式和其**FROM**和**其中**子句。 查詢的結果會傳回透過 OLE DB 資料列集，可供 ADO 和管理[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。

 您可以搜尋精確的單字或片語，或使用萬用字元來搜尋的單字或模式。 搜尋邏輯可以根據布林值決策、 加權的詞彙或接近其他字詞。 您也可以搜尋 「 任意文字 」，找到相符項目意義，而不是完全相同的文字為基礎。

 特定命令用語是完整記錄在索引服務文件集的查詢語言。

 提供者不接受預存程序呼叫或簡單的資料表名稱 (例如， [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性一定會是**adCmdText**)。

## <a name="recordset-behavior"></a>資料錄集行為
 下表列出可用的功能**資料錄集**開啟與此提供者的物件。 靜態資料指標類型 (**adOpenStatic**) 使用。

 如需詳細資訊，關於**資料錄集**您的提供者組態，執行行為[支援](../../../ado/reference/ado-api/supports-method.md)方法，並列舉[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合**資料錄集**來判斷是否存在特定提供者的動態屬性。

 **標準的 ADO 資料錄集屬性的可用性：**

|屬性|可用性|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|讀取/寫入|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|讀取/寫入|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|唯讀|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|唯讀|
|[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)*|讀取/寫入|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|讀取/寫入|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|一律**adUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|一律**adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|一律**adEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|唯讀|
|[篩選](../../../ado/reference/ado-api/filter-property.md)|讀取/寫入|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|讀取/寫入|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|無法使用|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|讀取/寫入|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|唯讀|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|讀取/寫入|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|唯讀|
|[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)|讀取/寫入|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|唯讀|
|[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)|唯讀|

 \*為了讓這項功能提供者，存在於上必須啟用書籤**資料錄集**。

 **標準的 ADO 資料錄集方法的可用性：**

|方法|可用？|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|否|
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|是|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|否|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|否|
|[複製](../../../ado/reference/ado-api/clone-method-ado.md)|是|
|[關閉](../../../ado/reference/ado-api/close-method-ado.md)|是|
|[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|否|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|是|
|[[移動]](../../../ado/reference/ado-api/move-method-ado.md)|是|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|是|
|[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)|是|
|[重新查詢](../../../ado/reference/ado-api/requery-method.md)|是|
|[重新同步處理](../../../ado/reference/ado-api/resync-method.md)|是|
|[支援](../../../ado/reference/ado-api/supports-method.md)|是|
|[Update](../../../ado/reference/ado-api/update-method.md)|否|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|否|

 對於特定的實作詳細資料和 Microsoft 索引服務的 Microsoft OLE DB 提供者的功能資訊，請參閱[OLE DB 程式設計人員指南](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx)，或請造訪 Windows NT Server Web 的 Web 服務頁面站台。

## <a name="see-also"></a>另請參閱
 [CommandType 屬性 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [ConnectionString 屬性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [支援方法](../../../ado/reference/ado-api/supports-method.md)

