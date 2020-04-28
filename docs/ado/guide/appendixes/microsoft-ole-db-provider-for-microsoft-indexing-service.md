---
title: Microsoft OLE DB 的 microsoft 索引服務提供者 |Microsoft Docs
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
ms.openlocfilehash: a5a81514fd12117a9f43e2c33bf0cda579fb363d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926669"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Microsoft OLE DB Provider for Microsoft 索引服務總覽
Microsoft OLE DB Provider for Microsoft 索引服務提供以程式設計的唯讀方式存取檔案系統，以及由 Microsoft 索引服務編制索引的 Web 資料。 ADO 應用程式可以發出 SQL 查詢來取得內容和檔案屬性資訊。

 提供者是無限制執行緒且已啟用 UNICODE。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到這個提供者，請將**提供者 =** 引數設定為[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性，以執行下列動作：

```vb
MSIDXS
```

 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性也會傳回這個字串。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串為：

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 此字串包含下列關鍵字：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 Microsoft 索引服務的 OLE DB 提供者。 這通常是在連接字串中指定的唯一關鍵字。|
|**資料來源**|指定索引服務類別目錄名稱。 如果未指定此關鍵字，則會使用預設的系統目錄。|
|**地區設定識別碼**|指定唯一32位數位（例如1033），指定與使用者語言相關的喜好設定。 如果未指定此關鍵字，則會使用預設的系統地區設定識別碼。|

## <a name="command-text"></a>命令文字
 索引服務 SQL 查詢語法包含 SQL-92 **SELECT**語句及其**FROM**和**WHERE**子句的延伸模組。 查詢的結果會透過 OLE DB 的資料列集傳回，這可由 ADO 取用並做為[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件來操作。

 您可以搜尋確切的單字或片語，或使用萬用字元搜尋單字的模式或詞幹。 搜尋邏輯可以根據布林值決策、加權詞彙或與其他單字的鄰近性。 您也可以依「任意文字」搜尋，這會根據意義尋找相符專案，而不是確切的文字。

 特定的命令用語已完整記載于索引服務檔的查詢語言中。

 提供者不接受預存程序呼叫或簡單的資料表名稱（例如， [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性一律會是**adCmdText**）。

## <a name="recordset-behavior"></a>記錄集行為
 下表列出使用此提供者開啟的**記錄集**物件可用的功能。 只有靜態資料指標類型（**adOpenStatic**）可供使用。

 如需提供者設定之**記錄集**行為的詳細資訊，請執行[支援](../../../ado/reference/ado-api/supports-method.md)方法，並列舉**記錄集**的[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合，以判斷提供者特定的動態屬性是否存在。

 **標準 ADO 記錄集屬性的可用性：**

|屬性|可用性|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|讀取/寫入|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|讀取/寫入|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|唯讀|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|唯讀|
|[書簽](../../../ado/reference/ado-api/bookmark-property-ado.md)*|讀取/寫入|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|讀取/寫入|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|一律**adUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|一律**adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|一律**adEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|唯讀|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|讀取/寫入|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|讀取/寫入|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|無法使用|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|讀取/寫入|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|唯讀|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|讀取/寫入|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|唯讀|
|[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)|讀取/寫入|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|唯讀|
|[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)|唯讀|

 \*必須在提供者上啟用書簽，這項功能才會存在於**記錄集**上。

 **標準 ADO 記錄集方法的可用性：**

|方法|是否可用？|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|否|
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|是|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|否|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|否|
|[複製](../../../ado/reference/ado-api/clone-method-ado.md)|是|
|[關閉](../../../ado/reference/ado-api/close-method-ado.md)|是|
|[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|否|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|是|
|[移動](../../../ado/reference/ado-api/move-method-ado.md)|是|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|是|
|[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)|是|
|[再次](../../../ado/reference/ado-api/requery-method.md)|是|
|[重新同步處理](../../../ado/reference/ado-api/resync-method.md)|是|
|[支援](../../../ado/reference/ado-api/supports-method.md)|是|
|[更新](../../../ado/reference/ado-api/update-method.md)|否|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|否|

 如需 microsoft OLE DB 提供者有關 Microsoft 索引服務的特定執行詳細資料和功能資訊，請參閱 OLE DB 程式設計[人員指南](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx)，或造訪 Windows NT Server 網站的 Web 服務頁面。

## <a name="see-also"></a>另請參閱
 [CommandType 屬性（ado）](../../../ado/reference/ado-api/commandtype-property-ado.md) [CONNECTIONSTRING 屬性（Ado）](../../../ado/reference/ado-api/connectionstring-property-ado.md) [屬性集合（ado）](../../../ado/reference/ado-api/properties-collection-ado.md) [提供者屬性（ado）](../../../ado/reference/ado-api/provider-property-ado.md) [Recordset 物件（ado）](../../../ado/reference/ado-api/recordset-object-ado.md) [支援方法](../../../ado/reference/ado-api/supports-method.md)
