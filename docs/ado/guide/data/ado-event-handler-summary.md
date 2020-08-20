---
description: ADO 連接和記錄集事件
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 92d1dcd202c4e115cda4198f90e3410c2cb44319
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453840"
---
# <a name="ado-connection-and-recordset-events"></a>ADO 連接和記錄集事件
有兩個 ADO 物件可以引發事件： [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 物件和 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) 物件。 **ConnectionEvent**系列適用于**連接**物件上的作業，而**RecordsetEvent**系列則與**記錄集**物件上的作業有關。

-   **連接事件**：當連接上的交易開始、認可或回復時，就會發出事件。當 [命令](../../../ado/reference/ado-api/command-object-ado.md) 執行時，在 **連接事件** 作業期間發生警告時，或 **連接** 開始或結束。

-   **記錄集事件**：當您流覽 **記錄集** 物件的資料列、變更記錄 **集**資料列中的欄位、 **變更記錄集**內的資料列、使用伺服器端資料指標來開啟 **記錄** 集、關閉 **記錄**集，或在 **記錄集中**進行任何變更時，就會發出事件。

 下表摘要說明這些事件及其描述。

|ConnectionEvent|描述|
|---------------------|-----------------|
|[BeginTransComplete, CommitTransComplete, RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**交易管理** -通知：連接上目前的交易已啟動、認可或回復。|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)、 [ConnectComplete、Disconnect](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**連接管理** -目前連接即將啟動、已啟動或已結束的通知。|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)、 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**命令執行管理** -在連接上執行目前命令的通知將會啟動或結束。|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**告知性** 通知：有關于目前作業的其他資訊。|

|RecordsetEvent|描述|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)、 [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|抓取**狀態**-資料抓取作業進度的通知，或已完成的提取作業。 只有在使用用戶端資料指標開啟 **記錄集** 時，才可以使用這些事件。|
|[WillChangeField、FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**欄位變更管理** -目前欄位的值將會變更或已變更的通知。|
|[WillMove、MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)、 [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**流覽管理** -通知： **記錄集中** 目前的資料列位置將會變更、已變更或已到達 **記錄集**的結尾。|
|[WillChangeRecord、RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|資料**列變更管理**-**記錄集**目前資料列中的某些內容將會變更或已變更的通知。|
|[WillChangeRecordset、RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**記錄集變更管理** -目前 **記錄集** 內的某個內容將會變更或已變更的通知。|

## <a name="see-also"></a>另請參閱
 [Ado 事件具現化（依語言](../../../ado/guide/data/ado-event-instantiation-by-language.md) [ado 事件](../../../ado/reference/ado-api/ado-events.md)） [事件參數](../../../ado/guide/data/event-parameters.md)事件 [處理常式如何一起運作](../../../ado/guide/data/how-event-handlers-work-together.md)事件 [類型](../../../ado/guide/data/types-of-events.md)
