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
ms.openlocfilehash: c2b7890cc9926025e7662e8571fb79309590f9de
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776677"
---
# <a name="ado-enumerated-constants"></a>ADO 列舉常數
為了協助進行偵錯工具，ADO 列舉會列出每個常數的值。 不過，此值純粹是諮詢，而且可能會從 ADO 的某個版本變更為另一個。 您的程式碼應該只取決於每個列舉常數的名稱，而不是實際值。  
  
|持續性|描述|  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](./adcprop-asyncthreadpriority-enum.md)|針對 RDS **記錄集** 物件，指定抓取資料之非同步執行緒的執行優先權。|  
|[ADCPROP_AUTORECALC_ENUM](./adcprop-autorecalc-enum.md)|指定當 **MSDataShape** 提供者在階層式 **記錄集中**重新計算匯總和計算資料行時。|  
|[ADCPROP_UPDATECRITERIA_ENUM](./adcprop-updatecriteria-enum.md)|指定哪些欄位可以用來偵測資料來源之資料列的開放式更新與 **記錄集** 物件之間的衝突。|  
|[ADCPROP_UPDATERESYNC_ENUM](./adcprop-updateresync-enum.md)|指定 **UpdateBatch** 方法是否接著隱含的 **Resync** 方法作業，如果是，該作業的範圍。|  
|[AffectEnum](./affectenum.md)|指定作業會影響哪些記錄。|  
|[BookmarkEnum](./bookmarkenum.md)|指定表示作業應開始之位置的書簽。|  
|[CommandTypeEnum](./commandtypeenum.md)|指定如何解讀命令引數。|  
|[CompareEnum](./compareenum.md)|指定兩筆記錄以其書簽表示的相對位置。|  
|[ConnectModeEnum](./connectmodeenum.md)|指定在**連接**中修改資料、開啟**記錄**，或針對**記錄**和**資料流程**物件的**Mode**屬性指定值的可用許可權。|  
|[ConnectOptionEnum](./connectoptionenum.md)|指定**連接**物件的**開啟**方法應該在 (同步) 之後，或在建立連接 (非同步) 之前傳回。|  
|[ConnectPromptEnum](./connectpromptenum.md)|指定是否應該在開啟 ODBC 資料來源的連接時，顯示對話方塊以提示遺漏參數。|  
|[CopyRecordOptionsEnum](./copyrecordoptionsenum.md)|指定 **CopyRecord** 方法的行為。|  
|[CursorLocationEnum](./cursorlocationenum.md)|指定資料指標引擎的位置。|  
|[CursorOptionEnum](./cursoroptionenum.md)|指定 **支援** 方法應該測試的功能。|  
|[CursorTypeEnum](./cursortypeenum.md)|指定 **記錄集** 物件中使用的資料指標類型。|  
|[DataTypeEnum](./datatypeenum.md)|指定 **欄位**、 **參數**或 **屬性**的資料類型。|  
|[EditModeEnum](./editmodeenum.md)|指定記錄的編輯狀態。|  
|[ErrorValueEnum](./errorvalueenum.md)|指定 ADO 執行階段錯誤的類型。|  
|[EventReasonEnum](./eventreasonenum.md)|指定造成事件發生的原因。|  
|[EventStatusEnum](./eventstatusenum.md)|指定事件執行的目前狀態。|  
|[ExecuteOptionEnum](./executeoptionenum.md)|指定提供者應該如何執行命令。|  
|[FieldEnum](./fieldenum.md)|指定**記錄**物件的**fields**集合中所參考的特殊欄位。|  
|[FieldAttributeEnum](./fieldattributeenum.md)|指定 **欄位** 物件的一或多個屬性。|  
|[FieldStatusEnum](./fieldstatusenum.md)|指定 **欄位** 物件的狀態。|  
|[FilterGroupEnum](./filtergroupenum.md)|指定要從 **記錄集**篩選的記錄群組。|  
|[GetRowsOptionEnum](./getrowsoptionenum.md)|指定要從 **記錄集**取出多少筆記錄。|  
|[IsolationLevelEnum](./isolationlevelenum.md)|指定 **連接** 物件的交易隔離層級。|  
|[LineSeparatorsEnum](./lineseparatorsenum.md)|指定用來做為文字 **資料流程** 物件中之行分隔符號的字元。|  
|[LockTypeEnum](./locktypeenum.md)|指定在編輯期間放置於記錄的鎖定類型。|  
|[MarshalOptionsEnum](./marshaloptionsenum.md)|指定應傳回給伺服器的記錄。|  
|[MoveRecordOptionsEnum](./moverecordoptionsenum.md)|指定 **Record** 物件 **MoveRecord** 方法的行為。|  
|[ObjectStateEnum](./objectstateenum.md)|指定物件為開啟或關閉、連接至資料來源、執行命令或提取資料。|  
|[ParameterAttributesEnum](./parameterattributesenum.md)|指定 **參數** 物件的屬性。|  
|[ParameterDirectionEnum](./parameterdirectionenum.md)|指定 **參數** 是否代表輸入參數、輸出參數或兩者，或如果參數是預存程式的傳回值。|  
|[PersistFormatEnum](./persistformatenum.md)|指定儲存 **記錄集**的格式。|  
|[PositionEnum](./positionenum.md)|指定記錄指標在記錄 **集**內的目前位置。|  
|[PropertyAttributesEnum](./propertyattributesenum.md)|指定 **屬性** 物件的屬性。|  
|[RecordCreateOptionsEnum](./recordcreateoptionsenum.md)|指定是否應該開啟現有的**記錄**，或應該建立新**記錄**的**記錄**物件**Open**方法。|  
|[RecordOpenOptionsEnum](./recordopenoptionsenum.md)|指定用於開啟 **記錄**的選項。 您可以使用 OR 運算子來結合這些值。|  
|[RecordStatusEnum](./recordstatusenum.md)|指定與批次更新和其他大量作業有關的記錄狀態。|  
|[RecordTypeEnum](./recordtypeenum.md)|指定 **記錄** 物件的類型。|  
|[ResyncEnum](./resyncenum.md)|指定重新 **同步**的呼叫是否覆寫基礎值。|  
|[SaveOptionsEnum](./saveoptionsenum.md)|指定從 **資料流程** 物件儲存時是否應該建立或覆寫檔案。 這些值可以與 AND 運算子合併。|  
|[SchemaEnum](./schemaenum.md)|指定**OpenSchema**方法所抓取之架構**記錄集**的類型。 指定記錄 **集**內的記錄搜尋方向。|  
|[SearchDirectionEnum](./searchdirectionenum.md)|指定記錄 **集**內的記錄搜尋方向。 指定要執行的 **搜尋** 類型。|  
|[SeekEnum](./seekenum.md)|指定要執行的 **搜尋** 類型。 指定開啟 **資料流程** 物件的選項。 這些值可以與 AND 運算子合併。|  
|[StreamOpenOptionsEnum](./streamopenoptionsenum.md)|指定開啟 **資料流程** 物件的選項。 這些值可以與 AND 運算子合併。 指定是否應該從 **資料流程** 物件讀取整個資料流程或下一行。|  
|[StreamReadEnum](./streamreadenum.md)|指定是否應該從 **資料流程** 物件讀取整個資料流程或下一行。 指定 **資料流程** 物件中儲存的資料類型。|  
|[StreamTypeEnum](./streamtypeenum.md)|指定 **資料流程** 物件中儲存的資料類型。 指定是否將行分隔符號附加至寫入 **資料流程** 物件的字串。|  
|[StreamWriteEnum](./streamwriteenum.md)|指定是否將行分隔符號附加至寫入 **資料流程** 物件的字串。 指定以字串形式抓取 **記錄集** 時的格式。|  
|[StringFormatEnum](./stringformatenum.md)|指定以字串形式抓取 **記錄集** 時的格式。 指定 **連接** 物件的交易屬性。|  
|[XactAttributeEnum](./xactattributeenum.md)|指定 **連接** 物件的交易屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](./ado-api-reference.md)   
 [ADO 集合](./ado-collections.md)   
 [ADO 動態屬性](./ado-dynamic-properties.md)   
 [附錄 B： ADO 錯誤](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](./ado-events.md)   
 [ADO 方法](./ado-methods.md)   
 [ADO 物件模型](./ado-object-model.md)   
 [ADO 物件和介面](./ado-objects-and-interfaces.md)   
 [ADO 屬性](./ado-properties.md)