---
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
ms.openlocfilehash: 00b33a9fa92dd6ec86cbac5a939fe593725bc091
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82749220"
---
# <a name="ado-enumerated-constants"></a>ADO 列舉常數
為了協助進行調試，ADO 列舉會列出每個常數的值。 不過，這個值純粹是諮詢，而且可能會從 ADO 的某個版本變更為另一個。 您的程式碼應該只取決於每個列舉常數的名稱，而不是實際的值。  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|對於 RDS**記錄集**物件，指定抓取資料之非同步執行緒的執行優先權。|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|指定**MSDataShape**提供者在階層式**記錄集中**重新計算匯總和計算結果欄的時機。|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|指定哪些欄位可以在使用**記錄集**物件的資料來源的開放式更新期間，用來偵測衝突。|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|指定**UpdateBatch**方法後面是否接著隱含的重新**同步**處理方法作業，如果是，則為該作業的範圍。|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|指定哪些記錄會受到作業影響。|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|指定表示作業應開始之位置的書簽。|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|指定應該如何解讀命令引數。|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|指定以書簽表示的兩筆記錄的相對位置。|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|指定在**連接**中修改資料、開啟**記錄**，或指定**記錄**和**資料流程**物件之**Mode**屬性值的可用許可權。|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|指定**連接**物件的**開啟**方法是否應在建立連接之後（同步）或之前傳回（以非同步方式傳回）。|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|指定在開啟 ODBC 資料來源的連接時，是否應該顯示對話方塊，以提示遺漏參數。|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|指定**CopyRecord**方法的行為。|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|指定資料指標引擎的位置。|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|指定**支援**方法應測試的功能。|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|指定**記錄集**物件中使用的資料指標類型。|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|指定**欄位**、**參數**或**屬性**的資料類型。|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|指定記錄的編輯狀態。|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|指定 ADO 執行階段錯誤的類型。|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|指定造成事件發生的原因。|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|指定事件執行的目前狀態。|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|指定提供者應該如何執行命令。|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|指定**記錄**物件的**fields**集合中所參考的特殊欄位。|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|指定**欄位**物件的一或多個屬性。|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|指定**欄位**物件的狀態。|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|指定要從**記錄集**篩選的記錄群組。|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|指定要從**記錄集**取出多少筆記錄。|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|指定**連接**物件的交易隔離層級。|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|指定用來做為文字**資料流程**物件中之行分隔符號的字元。|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|指定在編輯期間放置在記錄上的鎖定類型。|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|指定哪些記錄應該傳回至伺服器。|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|指定**Record**物件**MoveRecord**方法的行為。|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|指定物件為開啟或關閉、連接到資料來源、執行命令或提取資料。|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|指定**參數**物件的屬性。|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|指定**參數**是否代表輸入參數、輸出參數或兩者，或者，如果參數是預存程式的傳回值，則為。|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|指定用來儲存**記錄集**的格式。|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|指定記錄指標在**記錄集**內的目前位置。|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|指定**屬性**物件的屬性。|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|指定**記錄**物件**開啟**方法是否應開啟現有的**記錄**，或應建立新的**記錄**。|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|指定用於開啟**記錄**的選項。 這些值可以使用 OR 運算子結合。|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|指定有關批次更新和其他大量作業的記錄狀態。|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|指定**記錄**物件的類型。|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|指定重新**同步**的呼叫是否覆寫基礎值。|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|指定在從**資料流程**物件儲存時，是否要建立或覆寫檔案。 這些值可以與 AND 運算子結合。|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|指定**OpenSchema**方法所抓取之架構**記錄集**的類型。 在**記錄集中**指定記錄搜尋的方向。|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|在**記錄集中**指定記錄搜尋的方向。 指定要執行的**搜尋**類型。|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|指定要執行的**搜尋**類型。 指定用來開啟**資料流程**物件的選項。 這些值可以與 AND 運算子結合。|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|指定用來開啟**資料流程**物件的選項。 這些值可以與 AND 運算子結合。 指定是否應從**資料流程**物件讀取整個資料流程或下一行。|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|指定是否應從**資料流程**物件讀取整個資料流程或下一行。 指定**資料流程**物件中儲存的資料類型。|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|指定**資料流程**物件中儲存的資料類型。 指定是否要將行分隔符號附加至寫入**資料流程**物件的字串。|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|指定是否要將行分隔符號附加至寫入**資料流程**物件的字串。 指定以字串形式抓取**記錄集**時的格式。|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|指定以字串形式抓取**記錄集**時的格式。 指定**連接**物件的交易屬性。|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|指定**連接**物件的交易屬性。|  
  
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
