---
title: Microsoft OLE DB Provider for Microsoft 索引服務 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: dea7ec95efc1f560a2279868b2116d02d7ad6fef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701202"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Microsoft OLE DB Provider for Microsoft 索引服務概觀
Microsoft OLE DB Provider for Microsoft 索引服務提供程式設計的唯讀存取檔案系統和 Web 資料由 Microsoft 索引服務編製索引。 ADO 應用程式可以發出 SQL 查詢來擷取內容和檔案屬性資訊。

 提供者是無限制執行緒，並啟用 UNICODE。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到此提供者，將**提供者 =** 引數[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性：

```vb
MSIDXS
```

 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性會傳回此字串以及。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串是：

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 字串是由這些關鍵字所組成：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 OLE DB Provider for Microsoft 索引服務。 一般而言，這是唯一的連接字串中指定的關鍵字。|
|**資料來源**|指定的索引服務類別目錄名稱。 如果未指定此關鍵字，則會使用預設系統類別目錄。|
|**地區設定識別碼**|指定唯一 32 位元指定的數字 （例如，1033年） 的相關使用者的語言喜好設定。 如果未指定此關鍵字，則會使用預設系統地區設定識別項。|

## <a name="command-text"></a>命令文字
 編製索引服務 SQL 查詢語法包含延伸模組，SQL-92**選取**陳述式並將其**FROM**並**其中**子句。 查詢的結果會傳回透過 OLE DB 資料列，其中可以使用 ADO 與管理[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。

 您可以搜尋精確的單字或片語，或使用萬用字元來搜尋的文字或模式。 搜尋邏輯可以根據布林值決策、 加權的詞彙或接近其他字詞。 您也可以搜尋 「 任意文字 」，找到相符項目表示，而不是完全相同的文字為基礎。

 特定命令用語有 Indexing Service 文件的查詢語言的完整說明。

 提供者不接受預存程序呼叫或簡單的資料表名稱 (例如[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性一律會是**adCmdText**)。

## <a name="recordset-behavior"></a>資料錄集行為
 下表列出可用的功能**資料錄集**開啟與此提供者的物件。 只有靜態資料指標類型 (**adOpenStatic**) 使用。

 如需詳細資訊的相關**資料錄集**您的提供者組態，執行行為[支援](../../../ado/reference/ado-api/supports-method.md)方法，並列舉[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合**資料錄集**來判斷提供者特有的動態屬性是否存在。

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
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|always **adOpenStatic**|
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
|[狀態](../../../ado/reference/ado-api/state-property-ado.md)|唯讀|
|[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)|唯讀|

 \*為了讓這項功能提供者存在於上必須啟用書籤**資料錄集**。

 **標準的 ADO 資料錄集方法的可用性：**

|方法|可用？|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|否|
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|是|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|否|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|否|
|[複製](../../../ado/reference/ado-api/clone-method-ado.md)|是|
|[關閉](../../../ado/reference/ado-api/close-method-ado.md)|是|
|[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|否|
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

 如需特定的實作詳細資料和 Microsoft 索引服務的 Microsoft OLE DB 提供者的功能資訊，請參閱[OLE DB 程式設計人員指南](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx)，或瀏覽 Windows NT Server Web 的 Web 服務頁面站台。

## <a name="see-also"></a>另請參閱
 [CommandType 屬性 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [ConnectionString 屬性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [支援方法](../../../ado/reference/ado-api/supports-method.md)
