---
description: ADO 屬性
title: ADO 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- properties [ADO]
- ADO properties
ms.assetid: 0ac0d1a7-6c7a-4f4c-b115-428935e0f98b
author: rothja
ms.author: jroth
ms.openlocfilehash: 72a14ac3114a3b27a7570bc5961b9bd6ffff51cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451360"
---
# <a name="ado-properties"></a>ADO 屬性

|屬性|描述|  
|-|-|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|指出目前記錄所在的頁面。|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|表示 **記錄集** 物件目前記錄的序數位置。|  
|[ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md)|指出建立相關聯**記錄集**物件的**命令**物件。|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|指出指定的**命令**、**記錄集**或**記錄**物件目前所屬的**連接**物件。|  
|[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)|表示欄位值的實際長度。|  
|[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)|表示物件的一或多個特性。|  
|[BOF 和 EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|**BOF** 表示目前的記錄位置是在記錄集物件中的第一筆記錄之前。<br /><br /> **EOF** 表示目前的記錄位置是在記錄集物件中的最後一筆記錄之後。|  
|[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)|指出可唯一識別 **記錄集** 物件中目前記錄的書簽，或將 **記錄集** 物件中的目前記錄設定為有效書簽所識別的記錄。|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|指出記錄 **集** 物件中從本機快取到記憶體中的記錄數目。|  
|[章節](../../../ado/reference/ado-api/chapter-property-ado.md)|取得或設定**ADORecordsetConstruction**物件上/的 OLE DB**章節**物件。|  
|[字元集](../../../ado/reference/ado-api/charset-property-ado.md)|指出文字 **資料流程** 內容應轉譯成的字元集。|  
|[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)|表示當做 **命令** 物件輸入使用的資料流程。|  
|[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)|表示要對提供者發出的命令文字。|  
|[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)|表示在終止嘗試並產生錯誤之前，執行命令所要等候的時間長度。|  
|[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)|表示 **Command** 物件的型別。|  
|[ConnectionString 屬性](../../../ado/reference/ado-api/connectionstring-property-ado.md)|表示用來建立資料來源連接的資訊。|  
|[ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)|指出在結束嘗試並產生錯誤之前，建立連接所需等待的時間。|  
|[Count](../../../ado/reference/ado-api/count-property-ado.md)|表示集合中的物件數目。|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|表示資料指標服務的位置。|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|指出 **記錄集** 物件中使用的資料指標類型。|  
|[DataMember](../../../ado/reference/ado-api/datamember-property.md)|指出將從 **DataSource** 屬性所參考的物件中取出的資料成員名稱。|  
|[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)|表示物件，該物件包含要表示為 **記錄集** 物件的資料。|  
|[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)|表示 **連接** 物件的預設資料庫。|  
|[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)|表示 **Field** 物件的資料容量。|  
|[說明](../../../ado/reference/ado-api/description-property.md)|描述 **Error** 物件。|  
|[方言](../../../ado/reference/ado-api/dialect-property.md)|指出提供者將用來剖析 **CommandText** 或 **CommandStream** 屬性的語法和一般規則。|  
|[方向](../../../ado/reference/ado-api/direction-property.md)|指出 **參數** 是否代表輸入參數、輸出參數或兩者，或如果參數是預存程式的傳回值。|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|指出目前記錄的編輯狀態。|  
|[Eos](../../../ado/reference/ado-api/eos-property.md)|指出目前的位置是否在資料流程的結尾。|  
|[Filter](../../../ado/reference/ado-api/filter-property.md)|表示 **記錄集中**資料的篩選。|  
|[HelpCoNtext 和説明](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)|指出與 **錯誤** 物件相關聯的說明檔和主題。<br /><br /> **HelpContextID**協助工具會傳回說明檔中主題的內容識別碼，做為**完整**的值。<br /><br /> **HelpFile**協助檔會傳回評估為說明檔完整解析路徑的**字串**值。|  
|[Index](../../../ado/reference/ado-api/index-property.md)|表示 **記錄集** 物件目前作用中的索引名稱。|  
|[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)|表示 **連接** 物件的隔離層級。|  
|[Item](../../../ado/reference/ado-api/item-property-ado.md)|以名稱或序數表示集合的特定成員。|  
|[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)|表示要在文字 **資料流程** 物件中當做行分隔符號使用的二進位字元。|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|表示在編輯期間放置於記錄上的鎖定類型。|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|指出哪些記錄要封送處理回伺服器。|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|指出從查詢傳回 **記錄集** 的記錄數目上限。|  
|[Mode](../../../ado/reference/ado-api/mode-property-ado.md)|指出可用來修改 **連接**、 **記錄**或 **資料流程** 物件中資料的許可權。|  
|[名稱](../../../ado/reference/ado-api/name-property-ado.md)|指出物件的名稱。|  
|[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)|指出特定 **錯誤** 物件的提供者特定錯誤碼。|  
|[Number](../../../ado/reference/ado-api/number-property-ado.md)|指出可唯一識別 **錯誤** 物件的數位。|  
|[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)|指出 **參數** 或 **欄位** 物件中數值的小數位數。|  
|[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)|表示在進行任何變更之前，存在於記錄中的 **域** 值。|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|指出 **記錄集** 物件包含多少頁面的資料。|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|表示記錄 **集**內有多少筆記錄代表一個頁面。|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|在**ADORecordConstruction**物件上設定 OLE DB 資料**列**物件的容器，以便將資料列的父系轉換成 ADO**記錄**物件。|  
|[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)|指出指向目前**記錄**物件之父**記錄**的絕對 URL 字串。|  
|[位置](../../../ado/reference/ado-api/position-property-ado.md)|表示 **資料流程** 物件內的目前位置。|  
|[有效位數](../../../ado/reference/ado-api/precision-property-ado.md)|指出 **參數** 物件或數值 **欄位** 物件中數值的精確度程度。|  
|[Prepared](../../../ado/reference/ado-api/prepared-property-ado.md)|指出是否要在執行之前儲存命令的編譯版本。|  
|[提供者](../../../ado/reference/ado-api/provider-property-ado.md)|表示 **連接** 物件的提供者名稱。|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|指出記錄 **集** 物件中的記錄數目。|  
|[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)|表示 **記錄** 物件的類型。|  
|[資料列](../../../ado/reference/ado-api/row-property-ado.md)|取得或設定**ADORecordConstruction**物件上/的 OLE DB 資料**列**物件。|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|取得或設定來自**ADORecordsetConstruction**物件的 OLE DB **RowPosition**物件。|  
|[資料列集](../../../ado/reference/ado-api/rowset-property-ado.md)|取得或設定**ADORecordsetConstruction**物件上/的 OLE DB 資料列**集**物件。|  
|[ (ADO 錯誤) 的來源 ](../../../ado/reference/ado-api/source-property-ado-error.md)|指出原本產生錯誤的物件或應用程式的名稱。|  
|[ (ADO 記錄) 的來源 ](../../../ado/reference/ado-api/source-property-ado-record.md)|表示 **記錄** 物件所代表的實體。|  
|[ (ADO 記錄集) 的來源 ](../../../ado/reference/ado-api/source-property-ado-recordset.md)|指出 **記錄集** 物件中資料的來源|  
|[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)|指出特定 **錯誤** 物件的 SQL 狀態。|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|指出物件的狀態為開啟或關閉時，所有適用的物件。 指出執行非同步方法的所有適用物件，不論物件的目前狀態是連接、執行或正在抓取|  
|[狀態 (ADO 欄位) ](../../../ado/reference/ado-api/status-property-ado-field.md)|表示 **欄位** 物件的狀態。|  
|[ (ADO 記錄集的狀態) ](../../../ado/reference/ado-api/status-property-ado-recordset.md)|指出有關批次更新或其他大量作業之目前記錄的狀態。|  
|[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)|指出階層式 **記錄集** 物件中的基礎子記錄參考是否 (也就是，在父資料列位置變更時 *，) 變更* 。|  
|[Stream 屬性](../../../ado/reference/ado-api/stream-property.md)|從**ADOStreamConstruction**物件取得或設定 OLE DB**資料流程**物件。|  
|[型別](../../../ado/reference/ado-api/type-property-ado.md)|指出 **參數**、 **欄位**或 **屬性** 物件的操作類型或資料類型。|  
|[輸入 (ADO Stream) ](../../../ado/reference/ado-api/type-property-ado-stream.md)|表示 **資料流程** 中包含的資料類型 (二進位或文字) 。|  
|[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)|指出資料庫中 **Field** 物件的目前值。|  
|[值](../../../ado/reference/ado-api/value-property-ado.md)|表示指派給 **欄位**、 **參數**或 **屬性** 物件的值。|  
|[版本](../../../ado/reference/ado-api/version-property-ado.md)|表示 ADO 版本號碼。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 B： ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件和介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)
