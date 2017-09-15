---
title: "ADO 事件處理常式摘要 |Microsoft 文件"
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
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0cd8bf7593fb1e8c770edde83e697f5b5be1d1d3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="ado-connection-and-recordset-events"></a>ADO 連接和資料錄集的事件
兩個 ADO 物件可以引發事件：[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件和[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 **ConnectionEvent**系列相關作業上**連接**物件，而**RecordsetEvent**系列相關作業上**資料錄集**物件。

-   **連接事件**： 當交易在連接上的開始、 認可或復原回; 當時，所發出的事件[命令](../../../ado/reference/ado-api/command-object-ado.md); 時執行期間發生警告**連接事件**作業。或當**連接**開頭或結尾。

-   **資料錄集事件**： 周圍非同步的擷取作業，以及當您瀏覽的資料列時，會發出事件**資料錄集**物件，變更的資料列中的欄位**資料錄集**，變更中的資料列**資料錄集**，開啟**資料錄集**與伺服器端資料指標關閉**資料錄集**，或進行任何變更也不會收到在**資料錄集**。

 下表摘要說明的事件，以及其描述。

|ConnectionEvent|Description|
|---------------------|-----------------|
|[BeginTransComplete，CommitTransComplete，RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**交易管理**— 通知會在連接上目前的交易啟動後，認可或回復。|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)， [ConnectComplete，中斷連線](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**連接管理**— 通知，將會啟動目前的連線，已啟動，或已結束。|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)， [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**命令執行管理**— 將啟動目前的命令在連接上執行，或已結束的通知。|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**告知性**— 有通知目前作業的其他資訊。|

|RecordsetEvent|Description|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)， [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**擷取狀態**— 或擷取作業已完成的資料擷取作業的進度通知。 這些事件，才可以使用如果**資料錄集**使用用戶端資料指標為開啟。|
|[WillChangeField FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**欄位變更管理**— 目前欄位的值將會變更，或已變更的通知。|
|[WillMove、 MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)， [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**瀏覽管理**— 目前的資料列位置中的通知**資料錄集**會變更、 已變更，或已到達結尾**資料錄集**。|
|[WillChangeRecord RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**資料列變更管理**— 這項目中目前資料列的通知**資料錄集**將會變更，或已變更。|
|[WillChangeRecordset RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**資料錄集變更管理**— 也就是在目前的通知**資料錄集**將會變更，或已變更。|

## <a name="see-also"></a>另請參閱
 [ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md) [ADO 事件](../../../ado/reference/ado-api/ado-events.md)[事件參數](../../../ado/guide/data/event-parameters.md)[事件處理常式如何一起運作](../../../ado/guide/data/how-event-handlers-work-together.md)[的事件類型](../../../ado/guide/data/types-of-events.md)

