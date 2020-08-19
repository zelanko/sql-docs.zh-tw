---
description: ADO 列舉常數
title: ADO 列舉常數 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADO]
ms.assetid: c97ed131-1a93-463c-9e61-22f029b0c474
author: rothja
ms.author: jroth
ms.openlocfilehash: 7d126d0783e448dab786a228b4e10a8ec7c0f840
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451440"
---
# <a name="ado-enumerated-constants"></a>ADO 列舉常數
為了協助進行偵錯工具，ADO 列舉會列出每個常數的值。 不過，此值純粹是諮詢，而且可能會從 ADO 的某個版本變更為另一個。 您的程式碼應該只取決於每個列舉常數的名稱，而不是實際值。  
  
|持續性|描述|  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|針對 RDS **記錄集** 物件，指定抓取資料之非同步執行緒的執行優先權。|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|指定當 **MSDataShape** 提供者在階層式 **記錄集中**重新計算匯總和計算資料行時。|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|指定哪些欄位可以用來偵測資料來源之資料列的開放式更新與 **記錄集** 物件之間的衝突。|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|指定 **UpdateBatch** 方法是否接著隱含的 **Resync** 方法作業，如果是，該作業的範圍。|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|指定作業會影響哪些記錄。|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|指定表示作業應開始之位置的書簽。|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|指定如何解讀命令引數。|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|指定兩筆記錄以其書簽表示的相對位置。|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|指定在**連接**中修改資料、開啟**記錄**，或針對**記錄**和**資料流程**物件的**Mode**屬性指定值的可用許可權。|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|指定**連接**物件的**開啟**方法應該在 (同步) 之後，或在建立連接 (非同步) 之前傳回。|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|指定是否應該在開啟 ODBC 資料來源的連接時，顯示對話方塊以提示遺漏參數。|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|指定 **CopyRecord** 方法的行為。|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|指定資料指標引擎的位置。|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|指定 **支援** 方法應該測試的功能。|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|指定 **記錄集** 物件中使用的資料指標類型。|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|指定 **欄位**、 **參數**或 **屬性**的資料類型。|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|指定記錄的編輯狀態。|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|指定 ADO 執行階段錯誤的類型。|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|指定造成事件發生的原因。|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|指定事件執行的目前狀態。|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|指定提供者應該如何執行命令。|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|指定**記錄**物件的**fields**集合中所參考的特殊欄位。|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|指定 **欄位** 物件的一或多個屬性。|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|指定 **欄位** 物件的狀態。|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|指定要從 **記錄集**篩選的記錄群組。|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|指定要從 **記錄集**取出多少筆記錄。|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|指定 **連接** 物件的交易隔離層級。|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|指定用來做為文字 **資料流程** 物件中之行分隔符號的字元。|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|指定在編輯期間放置於記錄的鎖定類型。|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|指定應傳回給伺服器的記錄。|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|指定 **Record** 物件 **MoveRecord** 方法的行為。|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|指定物件為開啟或關閉、連接至資料來源、執行命令或提取資料。|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|指定 **參數** 物件的屬性。|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|指定 **參數** 是否代表輸入參數、輸出參數或兩者，或如果參數是預存程式的傳回值。|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|指定儲存 **記錄集**的格式。|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|指定記錄指標在記錄 **集**內的目前位置。|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|指定 **屬性** 物件的屬性。|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|指定是否應該開啟現有的**記錄**，或應該建立新**記錄**的**記錄**物件**Open**方法。|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|指定用於開啟 **記錄**的選項。 您可以使用 OR 運算子來結合這些值。|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|指定與批次更新和其他大量作業有關的記錄狀態。|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|指定 **記錄** 物件的類型。|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|指定重新 **同步**的呼叫是否覆寫基礎值。|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|指定從 **資料流程** 物件儲存時是否應該建立或覆寫檔案。 這些值可以與 AND 運算子合併。|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|指定**OpenSchema**方法所抓取之架構**記錄集**的類型。 指定記錄 **集**內的記錄搜尋方向。|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|指定記錄 **集**內的記錄搜尋方向。 指定要執行的 **搜尋** 類型。|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|指定要執行的 **搜尋** 類型。 指定開啟 **資料流程** 物件的選項。 這些值可以與 AND 運算子合併。|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|指定開啟 **資料流程** 物件的選項。 這些值可以與 AND 運算子合併。 指定是否應該從 **資料流程** 物件讀取整個資料流程或下一行。|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|指定是否應該從 **資料流程** 物件讀取整個資料流程或下一行。 指定 **資料流程** 物件中儲存的資料類型。|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|指定 **資料流程** 物件中儲存的資料類型。 指定是否將行分隔符號附加至寫入 **資料流程** 物件的字串。|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|指定是否將行分隔符號附加至寫入 **資料流程** 物件的字串。 指定以字串形式抓取 **記錄集** 時的格式。|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|指定以字串形式抓取 **記錄集** 時的格式。 指定 **連接** 物件的交易屬性。|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|指定 **連接** 物件的交易屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [附錄 B： ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件和介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
