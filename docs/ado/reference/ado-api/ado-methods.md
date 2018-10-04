---
title: ADO 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb7cf0945eb15d0f741e5b5fcba6c6e28fbe4955
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47660586"
---
# <a name="ado-methods"></a>ADO 方法
|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|建立可更新的新記錄**資料錄集**物件。|  
|[附加](../../../ado/reference/ado-api/append-method-ado.md)|將物件附加至集合。 如果集合很**欄位**，新**欄位**在附加至集合之前，可能會建立物件。|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|將資料附加至大型文字或二進位資料**欄位**，或**參數**物件。|  
|[BeginTrans、 CommitTrans 和 RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|管理交易中處理**連線**物件，如下所示：<br /><br /> **BeginTrans** — 開始新交易。<br /><br /> **CommitTrans** — 儲存任何變更，並結束目前的交易。 它也可以啟動新的交易。<br /><br /> **RollbackTrans** — 取消任何變更並結束目前的交易。 它也可以啟動新的交易。|  
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|取消執行暫止狀態，非同步方法呼叫。|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|取消擱置中的批次更新。|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|取消的現有或新資料列所做的任何變更**Recordset**物件，或**欄位**集合**記錄**物件，然後再呼叫**更新**方法。|  
|[Clear](../../../ado/reference/ado-api/clear-method-ado.md)|移除所有**錯誤**物件從**錯誤**集合。|  
|[複製](../../../ado/reference/ado-api/clone-method-ado.md)|建立複本**Recordset**從現有的物件**資料錄集**物件。 選擇性地指定複製處於唯讀模式。|  
|[關閉](../../../ado/reference/ado-api/close-method-ado.md)|關閉開啟的物件和任何相依的物件。|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|比較兩個書籤，並傳回它們相對值的指示。|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|將檔案或目錄，以及其內容，複製到另一個位置。|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|複製指定的字元或位元組數 (取決於**型別**) 中**Stream**到另一個**Stream**物件。|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|建立新**參數**具有指定之屬性的物件。|  
|[刪除 （ADO Parameters 集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|刪除的物件**參數**集合。|  
|[刪除 （ADO Fields 集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|刪除的物件**欄位**集合。|  
|[刪除 (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|刪除目前的記錄或一組記錄。|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|刪除檔案或目錄，以及所有子目錄。|  
|[執行 (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)|執行查詢、 SQL 陳述式或預存程序中指定**CommandText**屬性。|  
|[執行 (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|執行指定的查詢，SQL 陳述式、 預存程序或提供者特定的文字。|  
|[尋找](../../../ado/reference/ado-api/find-method-ado.md)|搜尋**資料錄集**針對符合指定之準則的資料列。|  
|[排清](../../../ado/reference/ado-api/flush-method-ado.md)|強制的內容**Stream**的基礎物件的 ADO 緩衝區中剩餘**Stream**相關聯。|  
|[get_OLEDBCommand 方法](../../../ado/reference/ado-api/get-oledbcommand-method.md)|傳回基礎 OLEDB 命令，先傳播所有在 ADO 命令上設定 [OLEDB] 命令的參數資訊。|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|傳回**Recordset**其資料列代表的檔案和子目錄中所表示的目錄**記錄**。|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|傳回所有的或大型文字或二進位資料內容的一部分**欄位**物件。|  
|[GetDataProviderDSO 方法](../../../ado/reference/ado-api/getdataproviderdso-method.md)|從 Shape 提供者擷取基礎 OLEDB 資料來源物件。|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|擷取的多筆記錄**資料錄集**成陣列的物件。|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|傳回**資料錄集**做為字串。|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|將現有檔案的內容載入**Stream**。|  
|[[移動]](../../../ado/reference/ado-api/move-method-ado.md)|移動中的目前記錄的位置**資料錄集**物件。|  
|[MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|移至 [first、 last、 下一步]，或上一個記錄中指定**資料錄集**物件，會記錄目前的記錄。|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|將檔案或目錄和其內容中，移至另一個位置。|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|清除目前**Recordset**物件，並傳回下一步**資料錄集**前移透過一系列的命令。|  
|[開啟 (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)|開啟資料來源的連接。|  
|[開啟 （ADO 記錄）](../../../ado/reference/ado-api/open-method-ado-record.md)|開啟現有**記錄**物件，或建立新的檔案或目錄。|  
|[開啟 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|開啟資料指標。|  
|[開啟 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)|會開啟**Stream**來操作二進位或文字資料流的物件。|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|從提供者取得資料庫結構描述資訊。|  
|[put_OLEDBCommand 方法](../../../ado/reference/ado-api/put-oledbcommand-method.md)|這個方法會執行任何作業-它一律會傳回 S_OK。|  
|[讀取](../../../ado/reference/ado-api/read-method.md)|讀取指定的數量的位元組**Stream**物件。|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|從文字檔讀取指定的字元數**Stream**物件。|  
|[[重新整理]](../../../ado/reference/ado-api/refresh-method-ado.md)|更新物件來反映，從可用的物件的集合以及特定給提供者。|  
|[重新查詢](../../../ado/reference/ado-api/requery-method.md)|更新中的資料**資料錄集**重新執行查詢所依據之物件的物件。|  
|[重新同步處理](../../../ado/reference/ado-api/resync-method.md)|重新整理中目前的資料**Recordset**物件，或**欄位**的集合**記錄**物件，從基礎資料庫。|  
|[儲存](../../../ado/reference/ado-api/save-method.md)|節省**Recordset**檔案中或**Stream**物件。|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|將儲存的二進位內容**Stream**至檔案。|  
|[搜尋](../../../ado/reference/ado-api/seek-method.md)|搜尋的索引**資料錄集**來快速尋找符合指定的值，並變更該資料列目前的資料列位置的資料列。|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|設定為資料流結尾的位置。|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|讀取的文字資料流時，會略過一整行。|  
|[統計資料](../../../ado/reference/ado-api/stat-method.md)|取得開啟的資料流相關的統計資訊。|  
|[支援](../../../ado/reference/ado-api/supports-method.md)|判斷指定**資料錄集**物件支援特定類型的功能。|  
|[Update](../../../ado/reference/ado-api/update-method.md)|儲存您對目前資料列的任何變更**Recordset**物件，或有**欄位**的集合**記錄**物件。|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|寫入磁碟中的所有暫止的批次更新。|  
|[寫入](../../../ado/reference/ado-api/write-method.md)|將二進位資料寫入**Stream**物件。|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|將指定的文字字串來寫入**Stream**物件。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 B:ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件與介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
