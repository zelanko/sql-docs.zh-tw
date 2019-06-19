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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4d9b2e581bfbce225bd34e78761b9e8ade621172
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696730"
---
# <a name="ado-enumerated-constants"></a>ADO 列舉常數
若要協助偵錯，ADO 列舉會列出每個常數的值。 不過，這個值會是純粹諮詢，，而且可能會從一個版本的 ADO 變更到另一個。 名稱，而非實際的值，每個列舉常數時，應該僅相依於您的程式碼。  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|對於使用 RDS**資料錄集**物件時，指定擷取資料的非同步執行緒的執行優先權。|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|指定何時**MSDataShape**提供者重新計算彙總與導出資料行，以階層**資料錄集**。|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|指定哪些欄位可用來偵測衝突，開放式資料來源之資料列更新期間**資料錄集**物件。|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|指定是否**UpdateBatch**方法後面隱含**重新同步處理**方法作業，如果是的話，該作業的範圍。|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|指定的記錄會受到影響的作業。|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|指定書籤，表示作業應該開始的位置。|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|指定應該如何解譯為命令引數。|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|指定兩筆記錄由其書籤的相對位置。|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|指定在修改資料的可用權限**連接**，開啟**記錄**，或指定值**模式**屬性**資料錄**並**Stream**物件。|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|指定是否**開放**方法**連線**物件後，應該傳回 （同步） 或之前 （非同步） 建立連線。|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|指定是否應該顯示對話方塊中開啟 ODBC 資料來源的連接時，遺漏的參數提示。|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|指定的行為**CopyRecord**方法。|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|指定資料指標引擎的位置。|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|指定哪些功能**支援**方法應該先進行測試。|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|指定資料指標中所使用的型別**資料錄集**物件。|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|指定的資料型別**欄位**，**參數**，或**屬性**。|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|指定編輯一筆記錄的狀態。|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|指定 ADO 執行階段錯誤的類型。|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|指定造成事件發生的原因。|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|指定的事件執行的目前狀態。|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|指定提供者執行命令的方式。|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|指定中參考的特殊欄位**欄位**的集合**記錄**物件。|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|指定一或多個屬性**欄位**物件。|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|指定的狀態**欄位**物件。|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|指定要從篩選的記錄群組**資料錄集**。|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|指定要擷取記錄數**資料錄集**。|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|指定的交易隔離層級**連線**物件。|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|指定做為文字行分隔符號的字元**Stream**物件。|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|指定在編輯期間鎖定記錄的型別。|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|指定哪些記錄應該傳回至伺服器。|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|指定的行為**記錄**物件**MoveRecord**方法。|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|指定物件是否為開啟或關閉、 連接到資料來源，執行命令，或擷取資料。|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|指定的屬性**參數**物件。|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|指定是否**參數**代表輸入的參數、 輸出參數，或兩者，或如果參數是預存程序的傳回值。|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|指定要儲存的格式**資料錄集**。|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|指定目前的位置內的記錄指標**資料錄集**。|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|指定的屬性**屬性**物件。|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|指定**記錄**物件**開放**方法是否現有**記錄**應該開啟，或新**記錄**應該建立。|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|指定選項，開啟**記錄**。 使用 OR 運算子，可以結合這些值。|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|指定批次更新和其他的大量作業記錄的狀態。|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|指定的型別**記錄**物件。|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|指定基礎值會覆寫呼叫**Resync**。|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|指定檔案是否要建立或覆寫時從儲存**Stream**物件。 值可以與 AND 運算子結合。|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|指定的結構描述型別**Recordset**可**OpenSchema**方法擷取。 指定的記錄搜尋中的方向**資料錄集**。|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|指定的記錄搜尋中的方向**資料錄集**。 指定的型別**搜尋**來執行。|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|指定的型別**搜尋**來執行。 指定選項，開啟**Stream**物件。 值可以與 AND 運算子結合。|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|指定選項，開啟**Stream**物件。 值可以與 AND 運算子結合。 指定的整個資料流] 或 [下一列是否應該從讀取**Stream**物件。|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|指定的整個資料流] 或 [下一列是否應該從讀取**Stream**物件。 指定類型的資料儲存在**Stream**物件。|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|指定類型的資料儲存在**Stream**物件。 指定寫入的字串是否有附加行分隔符號**Stream**物件。|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|指定寫入的字串是否有附加行分隔符號**Stream**物件。 擷取時指定的格式**資料錄集**做為字串。|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|擷取時指定的格式**資料錄集**做為字串。 指定的交易屬性**連線**物件。|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|指定的交易屬性**連線**物件。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [附錄 B：ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件與介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
