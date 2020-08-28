---
description: ADO 屬性
title: ADO 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: a8a53f4b901209a1ef59be6ca2eb8b531bc52d7c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976279"
---
# <a name="ado-properties"></a>ADO 屬性

|屬性|描述|  
|-|-|  
|[AbsolutePage](./absolutepage-property-ado.md)|指出目前記錄所在的頁面。|  
|[AbsolutePosition](./absoluteposition-property-ado.md)|表示 **記錄集** 物件目前記錄的序數位置。|  
|[ActiveCommand](./activecommand-property-ado.md)|指出建立相關聯**記錄集**物件的**命令**物件。|  
|[ActiveConnection](./activeconnection-property-ado.md)|指出指定的**命令**、**記錄集**或**記錄**物件目前所屬的**連接**物件。|  
|[ActualSize](./actualsize-property-ado.md)|表示欄位值的實際長度。|  
|[屬性](./attributes-property-ado.md)|表示物件的一或多個特性。|  
|[BOF 和 EOF](./bof-eof-properties-ado.md)|**BOF** 表示目前的記錄位置是在記錄集物件中的第一筆記錄之前。<br /><br /> **EOF** 表示目前的記錄位置是在記錄集物件中的最後一筆記錄之後。|  
|[書籤](./bookmark-property-ado.md)|指出可唯一識別 **記錄集** 物件中目前記錄的書簽，或將 **記錄集** 物件中的目前記錄設定為有效書簽所識別的記錄。|  
|[CacheSize](./cachesize-property-ado.md)|指出記錄 **集** 物件中從本機快取到記憶體中的記錄數目。|  
|[章節](./chapter-property-ado.md)|取得或設定**ADORecordsetConstruction**物件上/的 OLE DB**章節**物件。|  
|[字元集](./charset-property-ado.md)|指出文字 **資料流程** 內容應轉譯成的字元集。|  
|[CommandStream](./commandstream-property-ado.md)|表示當做 **命令** 物件輸入使用的資料流程。|  
|[CommandText](./commandtext-property-ado.md)|表示要對提供者發出的命令文字。|  
|[CommandTimeout](./commandtimeout-property-ado.md)|表示在終止嘗試並產生錯誤之前，執行命令所要等候的時間長度。|  
|[CommandType](./commandtype-property-ado.md)|表示 **Command** 物件的型別。|  
|[ConnectionString 屬性](./connectionstring-property-ado.md)|表示用來建立資料來源連接的資訊。|  
|[ConnectionTimeout](./connectiontimeout-property-ado.md)|指出在結束嘗試並產生錯誤之前，建立連接所需等待的時間。|  
|[Count](./count-property-ado.md)|表示集合中的物件數目。|  
|[CursorLocation](./cursorlocation-property-ado.md)|表示資料指標服務的位置。|  
|[CursorType](./cursortype-property-ado.md)|指出 **記錄集** 物件中使用的資料指標類型。|  
|[DataMember](./datamember-property.md)|指出將從 **DataSource** 屬性所參考的物件中取出的資料成員名稱。|  
|[資料來源](./datasource-property-ado.md)|表示物件，該物件包含要表示為 **記錄集** 物件的資料。|  
|[DefaultDatabase](./defaultdatabase-property.md)|表示 **連接** 物件的預設資料庫。|  
|[DefinedSize](./definedsize-property.md)|表示 **Field** 物件的資料容量。|  
|[說明](./description-property.md)|描述 **Error** 物件。|  
|[方言](./dialect-property.md)|指出提供者將用來剖析 **CommandText** 或 **CommandStream** 屬性的語法和一般規則。|  
|[方向](./direction-property.md)|指出 **參數** 是否代表輸入參數、輸出參數或兩者，或如果參數是預存程式的傳回值。|  
|[EditMode](./editmode-property.md)|指出目前記錄的編輯狀態。|  
|[Eos](./eos-property.md)|指出目前的位置是否在資料流程的結尾。|  
|[Filter](./filter-property.md)|表示 **記錄集中**資料的篩選。|  
|[HelpCoNtext 和説明](./helpcontext-helpfile-properties.md)|指出與 **錯誤** 物件相關聯的說明檔和主題。<br /><br /> **HelpContextID**協助工具會傳回說明檔中主題的內容識別碼，做為**完整**的值。<br /><br /> **HelpFile**協助檔會傳回評估為說明檔完整解析路徑的**字串**值。|  
|[Index](./index-property.md)|表示 **記錄集** 物件目前作用中的索引名稱。|  
|[IsolationLevel](./isolationlevel-property.md)|表示 **連接** 物件的隔離層級。|  
|[Item](./item-property-ado.md)|以名稱或序數表示集合的特定成員。|  
|[LineSeparator](./lineseparator-property-ado.md)|表示要在文字 **資料流程** 物件中當做行分隔符號使用的二進位字元。|  
|[LockType](./locktype-property-ado.md)|表示在編輯期間放置於記錄上的鎖定類型。|  
|[MarshalOptions](./marshaloptions-property-ado.md)|指出哪些記錄要封送處理回伺服器。|  
|[MaxRecords](./maxrecords-property-ado.md)|指出從查詢傳回 **記錄集** 的記錄數目上限。|  
|[模式](./mode-property-ado.md)|指出可用來修改 **連接**、 **記錄**或 **資料流程** 物件中資料的許可權。|  
|[名稱](./name-property-ado.md)|指出物件的名稱。|  
|[NativeError](./nativeerror-property-ado.md)|指出特定 **錯誤** 物件的提供者特定錯誤碼。|  
|[Number](./number-property-ado.md)|指出可唯一識別 **錯誤** 物件的數位。|  
|[NumericScale](./numericscale-property-ado.md)|指出 **參數** 或 **欄位** 物件中數值的小數位數。|  
|[OriginalValue](./originalvalue-property-ado.md)|表示在進行任何變更之前，存在於記錄中的 **域** 值。|  
|[PageCount](./pagecount-property-ado.md)|指出 **記錄集** 物件包含多少頁面的資料。|  
|[PageSize](./pagesize-property-ado.md)|表示記錄 **集**內有多少筆記錄代表一個頁面。|  
|[ParentRow](./parentrow-property-ado.md)|在**ADORecordConstruction**物件上設定 OLE DB 資料**列**物件的容器，以便將資料列的父系轉換成 ADO**記錄**物件。|  
|[ParentURL](./parenturl-property-ado.md)|指出指向目前**記錄**物件之父**記錄**的絕對 URL 字串。|  
|[位置](./position-property-ado.md)|表示 **資料流程** 物件內的目前位置。|  
|[有效位數](./precision-property-ado.md)|指出 **參數** 物件或數值 **欄位** 物件中數值的精確度程度。|  
|[Prepared](./prepared-property-ado.md)|指出是否要在執行之前儲存命令的編譯版本。|  
|[提供者](./provider-property-ado.md)|表示 **連接** 物件的提供者名稱。|  
|[RecordCount](./recordcount-property-ado.md)|指出記錄 **集** 物件中的記錄數目。|  
|[RecordType](./recordtype-property-ado.md)|表示 **記錄** 物件的類型。|  
|[行](./row-property-ado.md)|取得或設定**ADORecordConstruction**物件上/的 OLE DB 資料**列**物件。|  
|[RowPosition](./rowposition-property-ado.md)|取得或設定來自**ADORecordsetConstruction**物件的 OLE DB **RowPosition**物件。|  
|[資料列集](./rowset-property-ado.md)|取得或設定**ADORecordsetConstruction**物件上/的 OLE DB 資料列**集**物件。|  
|[ (ADO 錯誤) 的來源 ](./source-property-ado-error.md)|指出原本產生錯誤的物件或應用程式的名稱。|  
|[ (ADO 記錄) 的來源 ](./source-property-ado-record.md)|表示 **記錄** 物件所代表的實體。|  
|[ (ADO 記錄集) 的來源 ](./source-property-ado-recordset.md)|指出 **記錄集** 物件中資料的來源|  
|[SQLState](./sqlstate-property.md)|指出特定 **錯誤** 物件的 SQL 狀態。|  
|[State](./state-property-ado.md)|指出物件的狀態為開啟或關閉時，所有適用的物件。 指出執行非同步方法的所有適用物件，不論物件的目前狀態是連接、執行或正在抓取|  
|[狀態 (ADO 欄位) ](./status-property-ado-field.md)|表示 **欄位** 物件的狀態。|  
|[ (ADO 記錄集的狀態) ](./status-property-ado-recordset.md)|指出有關批次更新或其他大量作業之目前記錄的狀態。|  
|[StayInSync](./stayinsync-property.md)|指出階層式 **記錄集** 物件中的基礎子記錄參考是否 (也就是，在父資料列位置變更時 *，) 變更* 。|  
|[Stream 屬性](./stream-property.md)|從**ADOStreamConstruction**物件取得或設定 OLE DB**資料流程**物件。|  
|[類型](./type-property-ado.md)|指出 **參數**、 **欄位**或 **屬性** 物件的操作類型或資料類型。|  
|[輸入 (ADO Stream) ](./type-property-ado-stream.md)|表示 **資料流程** 中包含的資料類型 (二進位或文字) 。|  
|[UnderlyingValue](./underlyingvalue-property.md)|指出資料庫中 **Field** 物件的目前值。|  
|[值](./value-property-ado.md)|表示指派給 **欄位**、 **參數**或 **屬性** 物件的值。|  
|[版本](./version-property-ado.md)|表示 ADO 版本號碼。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](./ado-api-reference.md)   
 [ADO 集合](./ado-collections.md)   
 [ADO 動態屬性](./ado-dynamic-properties.md)   
 [ADO 列舉常數](./ado-enumerated-constants.md)   
 [附錄 B： ADO 錯誤](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](./ado-events.md)   
 [ADO 方法](./ado-methods.md)   
 [ADO 物件模型](./ado-object-model.md)   
 [ADO 物件和介面](./ado-objects-and-interfaces.md)