---
title: ADO 事件處理常式摘要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93790b3df8cb1d78ab2e0988cdc43cbd9af0718c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540446"
---
# <a name="ado-connection-and-recordset-events"></a>ADO 連接和資料錄集的事件
兩個 ADO 物件可以引發事件：[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件並[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 **ConnectionEvent**系列上屬於作業**連線**物件，而**RecordsetEvent**系列上屬於作業**資料錄集**物件。

-   **連線事件**:當連接上的交易開始、 經過認可或回復; 時，系統所發出事件當[命令](../../../ado/reference/ado-api/command-object-ado.md); 時執行期間發生警告**連接事件**作業，或當**連接**開頭或結尾。

-   **資料錄集事件**:周圍非同步的擷取作業，以及當您瀏覽的資料列時，會發出事件**Recordset**物件，變更的資料列中的欄位**資料錄集**，變更中的資料列**資料錄集**，開啟**Recordset**使用伺服器端資料指標關閉**資料錄集**，或進行任何變更也**資料錄集**。

 下表摘要說明的事件，以及它們的描述。

|ConnectionEvent|描述|
|---------------------|-----------------|
|[BeginTransComplete，CommitTransComplete，RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**交易管理**-通知，在此連接上目前的交易啟動後，認可或回復。|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)， [ConnectComplete，中斷連線](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**連接管理**-目前的連接將會啟動的通知已啟動，或已結束。|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)， [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**命令執行管理**-通知的連接上目前的命令執行會啟動，或已結束。|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**參考**-目前作業的相關額外資訊的通知。|

|RecordsetEvent|描述|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)， [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**擷取狀態**-通知進度的資料擷取作業，或已完成擷取作業。 這些事件只可供如果**資料錄集**開啟使用用戶端資料指標。|
|[WillChangeField FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**欄位變更管理**-目前欄位的值將會變更，或已變更的通知。|
|[WillMove、 MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)， [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**瀏覽管理**-目前的資料列位置中的通知**Recordset**會變更、 已變更，或已達到結束**資料錄集**。|
|[WillChangeRecord RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**資料列變更管理**-在目前資料列中的項目通知**資料錄集**將會變更，或已變更。|
|[WillChangeRecordset RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**資料錄集變更管理**-在目前的項目通知**資料錄集**將會變更，或已變更。|

## <a name="see-also"></a>另請參閱
 [ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md) [ADO 事件](../../../ado/reference/ado-api/ado-events.md)[事件參數](../../../ado/guide/data/event-parameters.md)[事件處理常式如何一起運作](../../../ado/guide/data/how-event-handlers-work-together.md)[的事件類型](../../../ado/guide/data/types-of-events.md)
