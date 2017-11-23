---
title: "ADO 列舉常數 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: enumerated constants [ADO]
ms.assetid: c97ed131-1a93-463c-9e61-22f029b0c474
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb606a366746b09d7ba6303b0cb11bb1b96f6164
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="ado-enumerated-constants"></a>ADO 列舉常數
若要協助偵錯，ADO 列舉會列出每個常數的值。 不過，這個值只是單純地建議，並從 ADO 發行版本可能會變更為另。 您的程式碼應該僅相依於名稱，而不是實際值，每個列舉常數。  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|針對 RDS**資料錄集**物件，指定非同步擷取資料的執行緒的執行優先順序。|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|指定何時**MSDataShape**提供者會重新計算彙總和導出資料行，以階層**資料錄集**。|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|指定哪些欄位可以用來偵測衝突，開放式與資料來源的資料列的更新期間**資料錄集**物件。|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|指定是否**UpdateBatch**方法後面的隱含**重新同步處理**方法作業而且如果是，該作業的範圍。|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|指定的記錄作業所影響。|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|指定指出此作業的開始位置的書籤。|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|指定應如何解譯為命令引數。|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|指定兩筆記錄，其書籤所代表的相對位置。|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|指定在修改資料的可用權限**連接**、 開啟**記錄**，或指定的值**模式**屬性**記錄**和**資料流**物件。|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|指定是否**開啟**方法**連接**物件後，應傳回 （同步） 或之前 （非同步） 建立連線。|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|指定是否應該顯示的對話方塊開啟 ODBC 資料來源的連接時提示遺漏的參數。|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|指定的行為**CopyRecord**方法。|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|指定資料指標引擎的位置。|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|指定哪些功能**支援**應該先測試方法。|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|指定使用中的資料指標類型**資料錄集**物件。|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|指定的資料型別**欄位**，**參數**，或**屬性**。|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|指定記錄的編輯狀態。|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|指定 ADO 執行階段錯誤的類型。|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|指定造成事件發生的原因。|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|指定的事件執行的目前狀態。|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|指定提供者如何執行命令。|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|指定特殊欄位中參考**欄位**集合**記錄**物件。|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|指定一或多個屬性**欄位**物件。|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|指定的狀態**欄位**物件。|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|指定要從篩選的記錄群組**資料錄集**。|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|指定要從擷取記錄數**資料錄集**。|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|指定的交易隔離層級**連接**物件。|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|指定做為文字中的分行符號字元**資料流**物件。|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|指定在編輯期間鎖定記錄類型。|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|指定應傳回哪一筆記錄，到伺服器。|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|指定的行為**記錄**物件**MoveRecord**方法。|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|指定物件是否為開啟或關閉、 連接到執行命令，或擷取資料的資料來源。|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|指定的屬性**參數**物件。|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|指定是否**參數**代表輸入的參數、 輸出參數，或兩者，或如果參數是預存程序的傳回值。|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|指定用來儲存格式**資料錄集**。|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|指定目前位置中的記錄指標**資料錄集**。|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|指定的屬性**屬性**物件。|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|指定**記錄**物件**開啟**方法是否現有**記錄**應已開啟，或新**記錄**應該建立。|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|指定選項，開啟**記錄**。 這些值可能會使用 OR 運算子合併。|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|指定批次更新和其他的大量作業記錄的狀態。|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|指定的型別**記錄**物件。|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|指定基礎值會覆寫呼叫**重新同步處理**。|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|指定檔案是否要建立或覆寫時從儲存**資料流**物件。 值可以與 AND 運算子結合。|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|指定的結構描述類型**資料錄集**， **OpenSchema**方法擷取。 指定的記錄搜尋方向**資料錄集**。|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|指定的記錄搜尋方向**資料錄集**。 指定的型別**搜尋**來執行。|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|指定的型別**搜尋**來執行。 指定選項，開啟**資料流**物件。 值可以與 AND 運算子結合。|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|指定選項，開啟**資料流**物件。 值可以與 AND 運算子結合。 指定整個資料流或下一行是否應該從讀取**資料流**物件。|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|指定整個資料流或下一行是否應該從讀取**資料流**物件。 指定類型的資料儲存在**資料流**物件。|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|指定類型的資料儲存在**資料流**物件。 指定是否要將分行符號附加至字串寫入**資料流**物件。|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|指定是否要將分行符號附加至字串寫入**資料流**物件。 指定的格式，擷取時**資料錄集**做為字串。|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|指定的格式，擷取時**資料錄集**做為字串。 指定的交易屬性**連接**物件。|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|指定的交易屬性**連接**物件。|  
  
## <a name="see-also"></a>請參閱＜  
 [ADO 應用程式開發介面參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [附錄 b: ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件與介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
