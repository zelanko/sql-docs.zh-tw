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
author: rothja
ms.author: jroth
ms.openlocfilehash: 65145ce8f77c352fb24a2a206d99828298b6a60c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747261"
---
# <a name="ado-methods"></a>ADO 方法

|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|建立可更新之**記錄集**物件的新記錄。|  
|[追加](../../../ado/reference/ado-api/append-method-ado.md)|將物件附加至集合。 如果集合是**欄位**，則可以在附加至集合之前，建立新的**Field**物件。|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|將資料附加至大型文字或二進位資料**欄位**或**參數**物件。|  
|[BeginTrans、CommitTrans 和 RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|管理**連接**物件內的交易處理，如下所示：<br /><br /> **BeginTrans** -開始新的交易。<br /><br /> **CommitTrans** -儲存任何變更，並結束目前的交易。 它也可能會開始新的交易。<br /><br /> **RollbackTrans** -取消任何變更，並結束目前的交易。 它也可能會開始新的交易。|  
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|取消執行暫止的非同步方法呼叫。|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|取消暫止的批次更新。|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|在呼叫**Update**方法之前，取消對**記錄集**物件的目前或新資料列或**記錄**物件的**Fields**集合所做的任何變更。|  
|[清除](../../../ado/reference/ado-api/clear-method-ado.md)|從**Errors**集合中移除所有**錯誤**物件。|  
|[複製](../../../ado/reference/ado-api/clone-method-ado.md)|從現有的**記錄集**物件建立重複的**記錄集**物件。 （選擇性）指定複製為唯讀。|  
|[關閉](../../../ado/reference/ado-api/close-method-ado.md)|關閉開啟的物件和任何相依物件。|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|比較兩個書簽，並傳回其相對值的指示。|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|將檔案或目錄及其內容複寫到另一個位置。|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|將**資料流程**中指定的字元或位元組數（視**類型**而定）複製到另一個**資料流程**物件。|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|建立具有指定之屬性的新**參數**物件。|  
|[Delete （ADO Parameters 集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|從**Parameters**集合中刪除物件。|  
|[Delete （ADO Fields 集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|從**Fields**集合中刪除物件。|  
|[Delete （ADO 記錄集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|刪除目前的記錄或一組記錄。|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|刪除檔案或目錄及其所有子目錄。|  
|[執行（ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)|執行**CommandText**屬性中所指定的查詢、SQL 語句或預存程式。|  
|[執行（ADO 連接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)|執行指定的查詢、SQL 語句、預存程式或提供者特定的文字。|  
|[尋找](../../../ado/reference/ado-api/find-method-ado.md)|搜尋**記錄集**，尋找符合指定準則的資料列。|  
|[刷](../../../ado/reference/ado-api/flush-method-ado.md)|將 ADO 緩衝區中剩餘的**資料流程**內容強制寫入與**資料流程**相關聯的基礎物件。|  
|[get_OLEDBCommand 方法](../../../ado/reference/ado-api/get-oledbcommand-method.md)|傳回基礎 OLEDB 命令，第一次將 ADO 命令上設定的任何參數資訊傳播至 OLEDB 命令。|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|傳回**記錄集**，其資料列代表此**記錄**所表示之目錄中的檔案和子目錄。|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|傳回大型文字或二進位資料**欄位**物件內容的全部或一部分。|  
|[GetDataProviderDSO 方法](../../../ado/reference/ado-api/getdataproviderdso-method.md)|從圖形提供者抓取基礎 OLEDB 資料來源物件。|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|將**記錄集**物件的多個記錄捕獲到陣列中。|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|以字串形式傳回**記錄集**。|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|將現有檔案的內容載入**資料流程**。|  
|[移動](../../../ado/reference/ado-api/move-method-ado.md)|移動**記錄集**物件中目前記錄的位置。|  
|[MoveFirst、MoveLast、MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|移至指定之**記錄集**物件中的第一個、最後一個、下一個或上一個記錄，並將該記錄設為目前的記錄。|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|將檔案或目錄及其內容移至另一個位置。|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|藉由推進一系列命令，清除目前的**記錄集**物件，並傳回下一個**記錄集**。|  
|[開啟（ADO 連接）](../../../ado/reference/ado-api/open-method-ado-connection.md)|開啟與資料來源的連接。|  
|[開啟（ADO 記錄）](../../../ado/reference/ado-api/open-method-ado-record.md)|開啟現有的**記錄**物件，或建立新的檔案或目錄。|  
|[開啟（ADO 記錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|開啟資料指標。|  
|[開啟（ADO Stream）](../../../ado/reference/ado-api/open-method-ado-stream.md)|開啟**資料流程**物件來操作二進位或文字資料的資料流程。|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|從提供者取得資料庫架構資訊。|  
|[put_OLEDBCommand 方法](../../../ado/reference/ado-api/put-oledbcommand-method.md)|這個方法不會執行任何作業，它一律會傳回 S_OK。|  
|[讀取](../../../ado/reference/ado-api/read-method.md)|從**資料流程**物件讀取指定的位元組數目。|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|從文字**資料流程**物件讀取指定的字元數。|  
|[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)|更新集合中的物件，以反映提供者所提供的物件。|  
|[再次](../../../ado/reference/ado-api/requery-method.md)|藉由重新執行物件所依據的查詢，更新**記錄集**物件中的資料。|  
|[重新同步處理](../../../ado/reference/ado-api/resync-method.md)|從基礎資料庫重新整理目前**記錄集**物件中的資料，或**記錄**物件的**Fields**集合。|  
|[儲存](../../../ado/reference/ado-api/save-method.md)|將**記錄集**儲存在檔案或**資料流程**物件中。|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|將**資料流程**的二進位內容儲存至檔案。|  
|[Seek](../../../ado/reference/ado-api/seek-method.md)|搜尋**記錄集**的索引，以快速找出符合指定值的資料列，並將目前的資料列位置變更為該資料列。|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|設定為數據流結尾的位置。|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|讀取文字資料流程時，略過一行整行。|  
|[Stat](../../../ado/reference/ado-api/stat-method.md)|取得有關開啟資料流程的統計資訊。|  
|[支援](../../../ado/reference/ado-api/supports-method.md)|判斷指定的**記錄集**物件是否支援特定類型的功能。|  
|[更新](../../../ado/reference/ado-api/update-method.md)|儲存您對**記錄集**物件的目前資料列或**記錄**物件的**Fields**集合所做的任何變更。|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|將所有暫止的批次更新寫入磁片。|  
|[寫入](../../../ado/reference/ado-api/write-method.md)|將二進位資料寫入**資料流程**物件。|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|將指定的文字字串寫入**資料流程**物件。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 B： ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件和介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
