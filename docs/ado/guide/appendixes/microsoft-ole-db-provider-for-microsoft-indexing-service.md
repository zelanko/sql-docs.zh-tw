---
description: Microsoft OLE DB Provider for Microsoft 索引編制服務總覽
title: Microsoft OLE DB 的 Microsoft 索引服務提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
author: rothja
ms.author: jroth
ms.openlocfilehash: b3e479ca023efb704bf496c9ffaeaca2f1b6ba15
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991039"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Microsoft OLE DB Provider for Microsoft 索引編制服務總覽
Microsoft OLE DB Provider for Microsoft 索引服務提供以程式設計方式唯讀存取由 Microsoft 索引服務編制索引的檔案系統和 Web 資料。 ADO 應用程式可以發出 SQL 查詢來取出內容和檔案屬性資訊。

 提供者是無限制執行緒和 UNICODE 啟用。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到這個提供者，請將[ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)屬性的**provider =** 引數設定為：

```vb
MSIDXS
```

 讀取 [Provider](../../reference/ado-api/provider-property-ado.md) 屬性也會傳回這個字串。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串為：

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 此字串包含下列關鍵字：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 Microsoft 索引服務的 OLE DB 提供者。 這通常是在連接字串中指定的唯一關鍵字。|
|**資料來源**|指定索引服務類別目錄名稱。 如果未指定此關鍵字，則會使用預設系統目錄。|
|**地區設定識別碼**|指定唯一的32位數位 (例如 1033) ，指定與使用者語言相關的喜好設定。 如果未指定此關鍵字，則會使用預設的系統地區設定識別碼。|

## <a name="command-text"></a>命令文字
 索引服務 SQL 查詢語法包含 SQL-92 **SELECT** 語句的延伸模組及其 **FROM** 和 **WHERE** 子句。 查詢的結果會透過 OLE DB 的資料列集來傳回，而 ADO 可以取用這些資料列集，並將其視為 [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件來使用。

 您可以搜尋確切的單字或片語，或使用萬用字元來搜尋單字的模式或詞幹。 搜尋邏輯可以根據布林值決策、加權詞彙或其他單字的相近。 您也可以搜尋「自由文字」，這會根據意義尋找相符專案，而不是確切的字組。

 特定的命令方言完整記載于索引服務檔的查詢語言。

 提供者不接受預存程序呼叫或簡單的資料表名稱 (例如， [CommandType](../../reference/ado-api/commandtype-property-ado.md) 屬性一律會 **adCmdText**) 。

## <a name="recordset-behavior"></a>記錄集行為
 下表列出使用此提供者開啟的 **記錄集** 物件所提供的功能。 只有靜態資料指標類型 (**adOpenStatic**) 可用。

 如需提供者設定的**記錄集**行為詳細資訊，請執行[支援](../../reference/ado-api/supports-method.md)的方法，並列舉**記錄集**的[屬性](../../reference/ado-api/properties-collection-ado.md)集合，以判斷是否存在提供者特定的動態屬性。

 **標準 ADO 記錄集屬性的可用性：**

|屬性|可用性|
|--------------|------------------|
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|讀取/寫入|
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|讀取/寫入|
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|唯讀|
|[轉爐](../../reference/ado-api/bof-eof-properties-ado.md)|唯讀|
|[書簽](../../reference/ado-api/bookmark-property-ado.md)*|讀取/寫入|
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|讀取/寫入|
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|一律 **adUseServer**|
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|一律 **adOpenStatic**|
|[EditMode](../../reference/ado-api/editmode-property.md)|一律 **adEditNone**|
|[Eof](../../reference/ado-api/bof-eof-properties-ado.md)|唯讀|
|[Filter](../../reference/ado-api/filter-property.md)|讀取/寫入|
|[LockType](../../reference/ado-api/locktype-property-ado.md)|讀取/寫入|
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|無法使用|
|[MaxRecords](../../reference/ado-api/maxrecords-property-ado.md)|讀取/寫入|
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|唯讀|
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|讀取/寫入|
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|唯讀|
|[Source](../../reference/ado-api/source-property-ado-recordset.md)|讀取/寫入|
|[State](../../reference/ado-api/state-property-ado.md)|唯讀|
|[狀態](../../reference/ado-api/status-property-ado-recordset.md)|唯讀|

 \*必須在提供者上啟用書簽，這項功能才會存在於 **記錄集**上。

 **標準 ADO 記錄集方法的可用性：**

|方法|是否可用？|
|------------|----------------|
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|否|
|[取消](../../reference/ado-api/cancel-method-ado.md)|是|
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|否|
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|否|
|[複製](../../reference/ado-api/clone-method-ado.md)|是|
|[關閉](../../reference/ado-api/close-method-ado.md)|是|
|[刪除](../../reference/ado-api/delete-method-ado-recordset.md)|否|
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|是|
|[移動](../../reference/ado-api/move-method-ado.md)|是|
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)|是|
|[開啟](../../reference/ado-api/open-method-ado-recordset.md)|是|
|[重新](../../reference/ado-api/requery-method.md)|是|
|[重新同步處理](../../reference/ado-api/resync-method.md)|是|
|[支援](../../reference/ado-api/supports-method.md)|是|
|[更新](../../reference/ado-api/update-method.md)|否|
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|否|

 如需 microsoft OLE DB Provider for Microsoft 索引服務的特定執行詳細資料與功能資訊，請參閱 OLE DB 程式設計 [人員指南](/previous-versions/windows/desktop/ms713643(v=vs.85))，或造訪 Windows NT Server 網站的 Web 服務頁面。

## <a name="see-also"></a>另請參閱
 [CommandType 屬性 (ado) ](../../reference/ado-api/commandtype-property-ado.md) [CONNECTIONSTRING 屬性 (Ado) ](../../reference/ado-api/connectionstring-property-ado.md) [屬性集合 (](../../reference/ado-api/properties-collection-ado.md) ado) [提供者屬性 ](../../reference/ado-api/provider-property-ado.md) (ado) [記錄集物件 ](../../reference/ado-api/recordset-object-ado.md) (ado) [支援方法](../../reference/ado-api/supports-method.md)