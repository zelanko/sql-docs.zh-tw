---
title: ADO 屬性 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- properties [ADO]
- ADO properties
ms.assetid: 0ac0d1a7-6c7a-4f4c-b115-428935e0f98b
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: faf6f2c0bee80ae3f8b59a9b8241226facc89edb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="ado-properties"></a>ADO 屬性
|||  
|-|-|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|指出目前記錄位於哪一頁。|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|指出目前記錄的序數位置**資料錄集**物件。|  
|[ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md)|指出**命令**建立相關聯的物件**資料錄集**物件。|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|表示要**連接**物件指定**命令**，**資料錄集**，或**記錄**目前所屬的物件。|  
|[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)|表示欄位值的實際長度。|  
|[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)|表示物件的一或多個特性。|  
|[BOF 和 EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|**BOF**指出目前的記錄位置是在資料錄集物件中的第一個資料錄之前。<br /><br /> **EOF**表示目前的記錄位置之後的資料錄集物件最後一筆記錄。|  
|[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)|指出目前的記錄中的唯一識別書籤**資料錄集**物件或設定目前資料錄**資料錄集**有效書籤所識別的記錄中的物件。|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|表示記錄數目**資料錄集**本機快取在記憶體中的物件。|  
|[本文章節](../../../ado/reference/ado-api/chapter-property-ado.md)|取得或設定 OLE DB**章**物件上從 / **ADORecordsetConstruction**物件。|  
|[CharSet](../../../ado/reference/ado-api/charset-property-ado.md)|指出字元集所在的文字內容**資料流**應轉譯。|  
|[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)|表示做為輸入資料流**命令**物件。|  
|[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)|表示要對提供者發出命令的文字。|  
|[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)|表示在終止嘗試並產生錯誤之前，執行命令時要等待的時間。|  
|[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)|表示的類型**命令**物件。|  
|[ConnectionString 屬性](../../../ado/reference/ado-api/connectionstring-property-ado.md)|表示用來連接到資料來源的資訊。|  
|[ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)|表示在終止嘗試並產生錯誤之前，建立連接時要等待的時間。|  
|[Count](../../../ado/reference/ado-api/count-property-ado.md)|指出集合中的物件數目。|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|指出資料指標服務的位置。|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|表示使用中的資料指標類型**資料錄集**物件。|  
|[DataMember](../../../ado/reference/ado-api/datamember-property.md)|表示將會從所參考的物件擷取的資料成員名稱**DataSource**屬性。|  
|[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)|表示物件，包含表示為資料**資料錄集**物件。|  
|[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)|表示的預設資料庫**連接**物件。|  
|[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)|表示的資料容量**欄位**物件。|  
|[說明](../../../ado/reference/ado-api/description-property.md)|描述**錯誤**物件。|  
|[方言](../../../ado/reference/ado-api/dialect-property.md)|表示語法和一般的規則，提供者將用來剖析**CommandText**或**CommandStream**屬性。|  
|[方向](../../../ado/reference/ado-api/direction-property.md)|指出是否**參數**代表輸入的參數、 輸出參數，或兩者，或如果參數是預存程序的傳回值。|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|指出目前記錄的編輯狀態。|  
|[EOS](../../../ado/reference/ado-api/eos-property.md)|指出目前的位置是否位於資料流結尾。|  
|[篩選](../../../ado/reference/ado-api/filter-property.md)|指出資料中的篩選**資料錄集**。|  
|[HelpContext 和說明檔](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)|表示說明檔和相關聯的主題**錯誤**物件。<br /><br /> **文字串**傳回的內容識別碼，做為**長**的說明檔主題的值。<br /><br /> **HelpFile**傳回**字串**評估為完全解決的說明檔路徑的值。|  
|[Index](../../../ado/reference/ado-api/index-property.md)|表示索引的目前作用中的名稱**資料錄集**物件。|  
|[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)|表示層級的隔離**連接**物件。|  
|[項目](../../../ado/reference/ado-api/item-property-ado.md)|依名稱或序數數字，指出特定集合的成員。|  
|[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)|表示為文字行分隔符號使用的二進位字元**資料流**物件。|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|表示在編輯期間鎖定記錄類型。|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|表示要封送處理至伺服器的記錄。|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|表示要傳回的記錄數目上限**資料錄集**從查詢。|  
|[模式](../../../ado/reference/ado-api/mode-property-ado.md)|表示可用的權限中修改資料**連接**，**記錄**，或**資料流**物件。|  
|[名稱](../../../ado/reference/ado-api/name-property-ado.md)|表示物件的名稱。|  
|[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)|表示為特定的提供者特有的錯誤程式碼**錯誤**物件。|  
|[數字](../../../ado/reference/ado-api/number-property-ado.md)|表示唯一識別數字**錯誤**物件。|  
|[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)|表示中的數值小數位數**參數**或**欄位**物件。|  
|[originalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)|值會指出**欄位**，存在於記錄中進行任何變更之前。|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|表示網頁的資料數量**資料錄集**包含物件。|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|表示記錄數目代表中的每一頁**資料錄集**。|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|設定 OLE DB 的容器**列**物件上**ADORecordConstruction**物件，使資料列的父代會轉換成 ADO**記錄**物件。|  
|[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)|指出父系所指向的絕對 URL 字串**記錄**的目前**記錄**物件。|  
|[位置](../../../ado/reference/ado-api/position-property-ado.md)|指出目前的位置內**資料流**物件。|  
|[有效位數](../../../ado/reference/ado-api/precision-property-ado.md)|表示數值有效位數的程度**參數**物件或數值**欄位**物件。|  
|[備妥的](../../../ado/reference/ado-api/prepared-property-ado.md)|指出是否要儲存編譯的命令執行之前的版本。|  
|[提供者](../../../ado/reference/ado-api/provider-property-ado.md)|指出提供者的名稱**連接**物件。|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|表示中的記錄數目**資料錄集**物件。|  
|[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)|表示的類型**記錄**物件。|  
|[資料列](../../../ado/reference/ado-api/row-property-ado.md)|取得或設定 OLE DB**列**物件上從 / **ADORecordConstruction**物件。|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|取得或設定 OLE DB **RowPosition**物件上從 / **ADORecordsetConstruction**物件。|  
|[Rowset](../../../ado/reference/ado-api/rowset-property-ado.md)|取得或設定 OLE DB**資料列集**物件上從 / **ADORecordsetConstruction**物件。|  
|[來源 （ADO 錯誤）](../../../ado/reference/ado-api/source-property-ado-error.md)|表示原始產生錯誤的應用程式之物件的名稱。|  
|[來源 （ADO 資料錄）](../../../ado/reference/ado-api/source-property-ado-record.md)|指出所代表的實體**記錄**物件。|  
|[來源 （ADO 資料錄集）](../../../ado/reference/ado-api/source-property-ado-recordset.md)|表示中的資料來源**資料錄集**物件|  
|[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)|指出特定的 SQL 狀態**錯誤**物件。|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|物件的狀態是否已開啟或關閉表示所有適用的物件。 表示所有適用的物件是否連接、 執行，或擷取物件的目前狀態執行的非同步方法，|  
|[狀態 （ADO 欄位）](../../../ado/reference/ado-api/status-property-ado-field.md)|表示狀態**欄位**物件。|  
|[狀態 （ADO 資料錄集）](../../../ado/reference/ado-api/status-property-ado-recordset.md)|指出目前記錄關於批次更新或其他的大量作業的狀態。|  
|[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)|表示以階層式**資料錄集**物件是否基礎的子記錄的參考 (也就是*章*) 變更，當父資料列變更時。|  
|[Stream 屬性](../../../ado/reference/ado-api/stream-property.md)|取得或設定 OLE DB**資料流**物件上從 / **ADOStreamConstruction**物件。|  
|[型別](../../../ado/reference/ado-api/type-property-ado.md)|表示作業的類型或資料類型的**參數**，**欄位**，或**屬性**物件。|  
|[型別 （ADO 資料流）](../../../ado/reference/ado-api/type-property-ado-stream.md)|指示中所包含的資料類型**資料流**（二進位或文字）。|  
|[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)|指出目前的資料庫中的值**欄位**物件。|  
|[值](../../../ado/reference/ado-api/value-property-ado.md)|指派給的值會指出**欄位**，**參數**，或**屬性**物件。|  
|[版本](../../../ado/reference/ado-api/version-property-ado.md)|指示 ADO 版本號碼。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO 應用程式開發介面參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 b: ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件和介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)
