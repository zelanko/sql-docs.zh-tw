---
description: ADO 方法
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
ms.openlocfilehash: 7702a90afe7ef4c96b1cc4bd01bd45e774a0bacc
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771797"
---
# <a name="ado-methods"></a>ADO 方法

|方法|描述|  
|-|-|  
|[AddNew](./addnew-method-ado.md)|針對可更新的 **記錄集** 物件建立新的記錄。|  
|[Append](./append-method-ado.md)|將物件附加至集合。 如果集合是 **欄位**，可能會先建立新的 **欄位** 物件，再將它附加至集合。|  
|[AppendChunk](./appendchunk-method-ado.md)|將資料附加至大型文字或二進位資料 **欄位**，或附加至 **參數** 物件。|  
|[BeginTrans、CommitTrans 和 RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)|管理 **連接** 物件內的交易處理，如下所示：<br /><br /> **BeginTrans** -開始新的交易。<br /><br /> **CommitTrans** ：儲存任何變更並結束目前的交易。 它也可以啟動新的交易。<br /><br /> **RollbackTrans** -取消任何變更，並結束目前的交易。 它也可以啟動新的交易。|  
|[取消](./cancel-method-ado.md)|取消執行暫止的非同步方法呼叫。|  
|[CancelBatch](./cancelbatch-method-ado.md)|取消暫止的批次更新。|  
|[CancelUpdate](./cancelupdate-method-ado.md)|在呼叫**Update**方法之前，取消對**記錄集**物件的目前或新資料列所做的任何變更，或**記錄**物件的**Fields**集合的任何變更。|  
|[Clear](./clear-method-ado.md)|從**錯誤**集合中移除所有**錯誤**物件。|  
|[複製](./clone-method-ado.md)|從現有的**記錄集**物件建立重複的**記錄集**物件。 （選擇性）指定複製是唯讀的。|  
|[關閉](./close-method-ado.md)|關閉開啟的物件和任何相依的物件。|  
|[CompareBookmarks](./comparebookmarks-method-ado.md)|比較兩個書簽，並傳回其相對值的指示。|  
|[CopyRecord](./copyrecord-method-ado.md)|將檔案或目錄及其內容複寫到另一個位置。|  
|[CopyTo](./copyto-method-ado.md)|根據**資料流程**中的**類型**) ，將指定的字元數或位元組數 (複製到另一個**資料流程**物件。|  
|[CreateParameter](./createparameter-method-ado.md)|建立具有指定屬性的新 **參數** 物件。|  
|[刪除 (ADO 參數集合) ](./delete-method-ado-parameters-collection.md)|從 **Parameters** 集合中刪除物件。|  
|[刪除 (ADO Fields 集合) ](./delete-method-ado-fields-collection.md)|從 **Fields** 集合中刪除物件。|  
|[刪除 (ADO 記錄集) ](./delete-method-ado-recordset.md)|刪除目前的記錄或一組記錄。|  
|[DeleteRecord](./deleterecord-method-ado.md)|刪除檔案或目錄及其所有子目錄。|  
|[執行 (ADO 命令) ](./execute-method-ado-command.md)|執行 **CommandText** 屬性中指定的查詢、SQL 語句或預存程式。|  
|[執行 (ADO 連接) ](./execute-method-ado-connection.md)|執行指定的查詢、SQL 語句、預存程式或提供者特定的文字。|  
|[Find](./find-method-ado.md)|搜尋 **記錄集** ，以尋找符合指定準則的資料列。|  
|[清除](./flush-method-ado.md)|將 ADO 緩衝區中剩餘的 **資料流程** 內容強制至與 **資料流程** 相關聯的基礎物件。|  
|[get_OLEDBCommand 方法](./get-oledbcommand-method.md)|傳回基礎 OLEDB 命令，先將 ADO 命令上設定的任何參數資訊傳播至 OLEDB 命令。|  
|[GetChildren](./getchildren-method-ado.md)|傳回 **記錄集** ，其資料列代表此 **記錄**所代表之目錄中的檔案和子目錄。|  
|[GetChunk](./getchunk-method-ado.md)|傳回大型文字或二進位資料 **欄位** 物件的所有或部分內容。|  
|[GetDataProviderDSO 方法](./getdataproviderdso-method.md)|從圖形提供者抓取基礎 OLEDB 資料來源物件。|  
|[GetRows](./getrows-method-ado.md)|將 **記錄集** 物件的多筆記錄抓取到陣列中。|  
|[GetString](./getstring-method-ado.md)|以字串形式傳回 **記錄集** 。|  
|[LoadFromFile](./loadfromfile-method-ado.md)|將現有檔案的內容載入至 **資料流程**。|  
|[移動](./move-method-ado.md)|移動 **記錄集** 物件中目前記錄的位置。|  
|[MoveFirst、MoveLast、MoveNext 和 MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|移至指定 **記錄集** 物件中的第一個、最後一個、下一個或上一個記錄，並使其記錄目前的記錄。|  
|[MoveRecord](./moverecord-method-ado.md)|將檔案或目錄和其內容移至另一個位置。|  
|[NextRecordset](./nextrecordset-method-ado.md)|清除目前的 **記錄集** 物件，並藉由前進一系列的命令，傳回下一個 **記錄集** 。|  
|[開啟 (ADO 連接) ](./open-method-ado-connection.md)|開啟與資料來源的連接。|  
|[開啟 (ADO 記錄) ](./open-method-ado-record.md)|開啟現有的 **記錄** 物件，或建立新的檔案或目錄。|  
|[開啟 (ADO 記錄集) ](./open-method-ado-recordset.md)|開啟資料指標。|  
|[開啟 (ADO Stream) ](./open-method-ado-stream.md)|開啟 **資料流程** 物件，以操作二進位或文字資料的資料流程。|  
|[OpenSchema](./openschema-method.md)|從提供者取得資料庫架構資訊。|  
|[put_OLEDBCommand 方法](./put-oledbcommand-method.md)|這個方法不會執行任何作業，它一律會傳回 S_OK。|  
|[讀取](./read-method.md)|從 **資料流程** 物件讀取指定的位元組數目。|  
|[ReadText](./readtext-method.md)|從文字 **資料流程** 物件讀取指定的字元數。|  
|[[重新整理]](./refresh-method-ado.md)|更新集合中的物件，以反映可供提供者使用的物件，以及特定的物件。|  
|[重新](./requery-method.md)|藉由重新執行物件所依據的查詢來更新 **記錄集** 物件中的資料。|  
|[重新同步處理](./resync-method.md)|從基礎資料庫重新整理目前**記錄集**物件中的資料，或**記錄**物件的**欄位**集合中的資料。|  
|[儲存](./save-method.md)|將 **記錄集** 儲存在檔案或 **資料流程** 物件中。|  
|[SaveToFile](./savetofile-method.md)|將 **資料流程** 的二進位內容儲存至檔案。|  
|[Seek](./seek-method.md)|搜尋 **記錄集** 的索引，以快速找出符合指定值的資料列，並將目前的資料列位置變更為該資料列。|  
|[SetEOS](./seteos-method.md)|設定資料流程結尾的位置。|  
|[SkipLine](./skipline-method.md)|讀取文字資料流程時，略過一行。|  
|[統計](./stat-method.md)|取得有關開啟之資料流程的統計資訊。|  
|[支援](./supports-method.md)|判斷指定的 **記錄集** 物件是否支援特定的功能類型。|  
|[更新](./update-method.md)|儲存您對**記錄集**物件的目前資料列所做的任何變更，或**記錄**物件的**Fields**集合。|  
|[UpdateBatch](./updatebatch-method.md)|將所有暫止的批次更新寫入磁片。|  
|[寫入](./write-method.md)|將二進位資料寫入 **資料流程** 物件。|  
|[WriteText](./writetext-method.md)|將指定的文字字串寫入 **資料流程** 物件。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](./ado-api-reference.md)   
 [ADO 集合](./ado-collections.md)   
 [ADO 動態屬性](./ado-dynamic-properties.md)   
 [ADO 列舉常數](./ado-enumerated-constants.md)   
 [附錄 B： ADO 錯誤](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](./ado-events.md)   
 [ADO 物件模型](./ado-object-model.md)   
 [ADO 物件和介面](./ado-objects-and-interfaces.md)   
 [ADO 屬性](./ado-properties.md)