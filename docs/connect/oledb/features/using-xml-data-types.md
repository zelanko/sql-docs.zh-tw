---
title: 使用 XML 資料類型 |Microsoft Docs
description: 使用 OLE DB 驅動程式中的 XML 資料類型，適用於 SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRowsetChange interface
- IRowsetUpdate interface
- data access [OLE DB Driver for SQL Server], xml data type
- OLE DB Driver for SQL Server schema rowsets
- PROVIDER_TYPES rowset
- IColumnsInfo interface
- IRowsetFind interface
- IColumnsRowset interface
- PROCEDURE_PARAMETERS rowset
- MSOLEDBSQL, XML
- xml data type [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, XML
- IRowset interface
- ISequentialStream interface
- ISSCommandWithParameters interface
- SS_XMLSCHEMA rowset
- OLE DB Driver for SQL Server OLE DB interfaces
- XML [SQL Server], OLE DB Driver for SQL Server
- COLUMNS rowset
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: fa67c09d301c5932ccd128129b3beccf57c1a1e3
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025227"
---
# <a name="using-xml-data-types"></a>使用 XML 資料類型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 推出的 **xml** 資料類型可讓您將 XML 文件和片段儲存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中。 **xml** 資料類型是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的內建資料類型，而且在某些狀況下類似於其他內建類型，例如 **int** 和 **varchar**。 如果是其他內建類型，當您建立資料表作為變數類型、參數類型、函式傳回型別，或是在 CAST 和 CONVERT 函式中時，可以使用 **xml** 資料類型作為資料行類型。  
  
## <a name="programming-considerations"></a>程式設計考量  
 XML 可以是自我描述的，因為它可以選擇性地包含指定文件編碼的 XML 標頭，例如：  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 XML 標準描述 XML 處理器如何透過檢查文件的前幾個位元組來偵測用於文件的編碼。 應用程式所指定的編碼有時候會與文件所指定的編碼產生衝突。 對於當做繫結參數傳遞的文件，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會將 XML 視為二進位資料，因此不需要進行轉換，而且 XML 剖析器可以毫無問題地使用在文件中指定的編碼。 不過，對於繫結為 WSTR 的 XML 資料，則應用程式必須確認文件的編碼為 Unicode。 這種情況下可能需要將文件載入到 DOM、將編碼變更為 Unicode，然後將文件序列化。 如果尚未完成此步驟，可能會發生資料轉換，這會導致 XML 無效或損毀。  
  
 以常值指定 XML 時，也有可能發生衝突。 例如，下列內容無效：  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 
 DBTYPE_XML 是新的資料類型的特定 OLE DB Driver for SQL Server 中的 XML。 此外，XML 資料可以透過 DBTYPE_BYTES、DBTYPE_WSTR、DBTYPE_BSTR、DBTYPE_XML、DBTYPE_STR、DBTYPE_VARIANT 和 DBTYPE_IUNKNOWN 的現有 OLE DB 類型進行存取。 儲存在 XML 類型資料行中的資料可以使用下列格式，從 OLE DB Driver for SQL Server 資料列集的資料行中擷取：  
  
-   文字字串  
  
-   **ISequentialStream**  
  
> [!NOTE]  
>  OLE DB Driver for SQL Server 不包含 SAX 讀取器，但是可以將 **ISequentialStream** 輕鬆地傳遞到 MSXML 中的 SAX 和 DOM 物件。  
  
 **ISequentialStream** 應該用於擷取大型 XML 文件。 用於其他大數值類型的相同技術也適用於 XML。 如需詳細資訊，請參閱 <<c0> [ 使用大型值型別](../../oledb/features/using-large-value-types.md)。  
  
 儲存在資料列集之 XML 類型資料行中的資料也可以由應用程式，透過 **IRow::GetColumns**、**IRowChange::SetColumns** 和 **ICommand::Execute** 之類的一般介面擷取、插入或更新。 類似於擷取情況，應用程式可以將文字字串或 **ISequentialStream** 傳遞到 OLE DB Driver for SQL Server。  
  
> [!NOTE]  
>  若要透過 **ISequentialStream** 介面傳送字串格式的 XML 資料，您必須指定 DBTYPE_IUNKNOWN 來取得 **ISequentialStream**，並在繫結中，將其 *pObject* 引數設定為 Null。  
  
 當擷取的 XML 資料因為取用者緩衝區太小而遭到截斷時，可以會將長度傳回為 0xffffffff，這表示長度不明。 這個行為與當作串流至用戶端，而不先傳送實際資料長度資訊之資料類型的實作一致。 在某些情況下，當提供者已經緩衝整個值 (例如 **IRowset::GetData**) 時，以及執行資料轉換時，可能會傳回實際長度。  
  
 伺服器會將傳送到 SQL Server 的 XML 資料視為二進位資料。 這個行為可以防止發生任何轉換，並允許 XML 剖析器自動偵測 XML 編碼。 這樣可以接受各種 XML 文件 (例如，以 UTF-8 編碼的文件) 做為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的輸入。  
  
 如果輸入 XML 繫結為 DBTYPE_WSTR，應用程式必須確定它已經使用 Unicode 編碼，才能避免因為不需要的資料轉換造成損毀的可能性。  
  
### <a name="data-bindings-and-coercions"></a>資料繫結和強制型轉  
 下表描述搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **xml** 資料類型使用列出的資料類型時，所發生的繫結和強制型轉。  
  
|資料類型|到伺服器<br /><br /> **XML**|到伺服器<br /><br /> **非 XML**|從伺服器<br /><br /> **XML**|從伺服器<br /><br /> **非 XML**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|通過<sup>6,7</sup>|錯誤<sup>1</sup>|確定<sup>11，6</sup>|錯誤<sup>8</sup>|  
|DBTYPE_BYTES|通過<sup>6,7</sup>|N/A<sup>2</sup>|沒有問題 <sup>11, 6</sup>|N/A <sup>2</sup>|  
|DBTYPE_WSTR|通過<sup>6,10</sup>|N/A <sup>2</sup>|確定<sup>4、 6、 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_BSTR|通過<sup>6,10</sup>|N/A <sup>2</sup>|沒有問題 <sup>3</sup>|N/A <sup>2</sup>|  
|DBTYPE_STR|確定<sup>6、 9、 10</sup>|N/A <sup>2</sup>|沒有問題<sup>5, 6, 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_IUNKNOWN|透過 **ISequentialStream** 的位元組資料流<sup>7</sup>|N/A <sup>2</sup>|透過 **ISequentialStream** 的位元組資料流<sup>11</sup>|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|通過<sup>6,7</sup>|N/A <sup>2</sup>|不適用|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|通過<sup>6,10</sup>|N/A <sup>2</sup>|沒有問題<sup>3</sup>|N/A <sup>2</sup>|  
  
 <sup>1</sup>如果使用 **ICommandWithParameters::SetParameterInfo** 指定 DBTYPE_XML 以外的伺服器類型，而且存取子類型為 DBTYPE_XML，則在執行陳述式 (DB_E_ERRORSOCCURRED，參數狀態為 DBSTATUS_E_BADACCESSOR) 時會發生錯誤；否則，資料會傳送到伺服器，但是伺服器會傳回錯誤，指出沒有從 XML 隱含地轉換為參數的資料類型。  
  
 <sup>2</sup> 超出此文章的範圍。  
  
 <sup>3</sup>格式為 UTF-16，無位元組順序標示 (BOM)，無編碼規格，無 Null 結束。  
  
 <sup>4</sup>格式為 UTF-16，無 BOM，無編碼規格，Null 結束。  
  
 <sup>5</sup>格式為以用戶端字碼頁搭配 Null 結束字元編碼的多位元組字元。 從伺服器提供的 Unicode 進行轉換可能會造成資料損毀；因此，建議您不要使用此繫結。  
  
 <sup>6</sup>可能會使用 BY_REF。  
  
 <sup>7</sup>UTF-16 資料必須以 BOM 開頭。 如果不是，伺服器可能無法正確辨識編碼。  
  
 <sup>8</sup>建立存取子時，或提取時，可能會進行驗證。 錯誤為 DB_E_ERRORSOCCURRED，繫結狀態設定為 DBBINDSTATUS_UNSUPPORTEDCONVERSION。  
  
 <sup>9</sup>資料會先使用用戶端字碼頁轉換為 Unicode，然後再傳送到伺服器。 如果文件編碼與用戶端字碼頁不符，可能會發生資料損毀；因此，強烈建議您不要使用此繫結。  
  
 <sup>10</sup>BOM 一律會新增到傳送至伺服器的資料中。 如果資料已經以 BOM 開頭，在緩衝區的開頭會有兩個 BOM。 伺服器會使用第一個 BOM 將編碼識別為 UTF-16，然後再捨棄它。 第二個 BOM 會解譯為零寬度的不分行空格字元。  
  
 <sup>11</sup>格式為 UTF-16，無編碼規格，BOM 會加入到接收自伺服器的資料中。 如果伺服器傳回空字串，仍然會將 BOM 傳回到應用程式。 如果緩衝區長度為奇數位元組，則會正確地截斷資料。 如果在區塊中傳回整個值，可以串連這些區塊以重新組成正確的值。  
  
 <sup>12</sup>如果緩衝區長度小於兩個字元 (也就是說，沒有足夠的空間給 Null 結束)，則會報告溢位錯誤。  
  
> [!NOTE]  
>  NULL XML 值不會傳回任何資料。  
  
 XML 標準需要以 UTF-16 編碼的 XML 來開始位元組順序標示 (BOM)，UTF-16 字元程式碼 0xFEFF。 使用 WSTR 和 BSTR 繫結時，OLE DB Driver for SQL Server 不需要或者不會新增 BOM，因為繫結已默許編碼。 使用 BYTES、XML 或 IUNKNOWN 繫結時，其用意在於提供處理其他 XML 處理器和儲存系統的單純性。 在此情況下，BOM 應該以 UTF-16 編碼的 XML 呈現，而且應用程式不需要在意實際編碼，因為多數 XML 處理器 (包括 SQL Server) 都會檢查值的前幾個位元組來推算編碼。 使用 BYTES、XML 或 IUNKNOWN 繫結，從 OLE DB Driver for SQL Server 接收的 XML 資料一律會以包含 BOM 的 UTF-16 編碼，而且不會有內嵌的編碼宣告。  
  
 OLE DB 核心服務 (**IDataConvert**) 提供的資料轉換不適用於 DBTYPE_XML。  
  
 當資料傳送到伺服器時，會執行驗證。 應由您的應用程式處理用戶端驗證和編碼變更。 建議您未直接處理 XML 資料，但應該改用 DOM 或 SAX 讀取器來處理它。  
  
 可以繫結 DBTYPE_NULL 和 DBTYPE_EMPTY 用於輸入參數，但是不能用於輸出參數或結果。 當針對輸入參數來繫結時，狀態必須設定為 DBSTATUS_S_ISNULL 或 DBSTATUS_S_DEFAULT。  
  
 DBTYPE_XML 可以轉換成 DBTYPE_EMPTY，而 DBTYPE_NULL、DBTYPE_EMPTY 可以轉換成 DBTYPE_XML，但是 DBTYPE_NULL 無法轉換成 DBTYPE_XML。 這與 DBTYPE_WSTR 一致。  
  
 DBTYPE_IUNKNOWN 是支援的繫結 (如上表所示)，但是在 DBTYPE_XML 和 DBTYPE_IUNKNOWN 之間沒有進行任何轉換。 DBTYPE_IUNKNOWN 可能無法搭配 DBTYPE_BYREF 使用。  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 資料列集的加入和變更  
 OLE DB Driver for SQL Server 會加入新的值，或變更許多核心 OLE DB 結構描述資料列。  
  
#### <a name="the-columns-and-procedureparameters-schema-rowsets"></a>COLUMNS 和 PROCEDURE_PARAMETERS 結構描述資料列集  
 COLUMNS 和 PROCEDURE_PARAMETERS 結構描述資料列集的新增項目包含下列資料行：  
  
|資料行名稱|類型|Description|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|定義 XML 結構描述集合所在目錄的名稱。 對於非 XML 資料行或不具類型的 XML 資料行，此為 NULL。|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|定義 XML 結構描述集合所在結構描述的名稱。 對於非 XML 資料行或不具類型的 XML 資料行，此為 NULL。|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|XML 結構描述集合的名稱。 對於非 XML 資料行或不具類型的 XML 資料行，此為 NULL。|  
  
#### <a name="the-providertypes-schema-rowset"></a>PROVIDER_TYPES 結構描述資料列集  
 在 PROVIDER_TYPES 結構描述資料列集中，如果是 **xml** 資料類型，COLUMN_SIZE 值為 0，而 DATA_TYPE 為 DBTYPE_XML。  
  
#### <a name="the-ssxmlschema-schema-rowset"></a>SS_XMLSCHEMA 結構描述資料列集  
 用戶端推出新的結構描述資料列集 SS_XMLSCHEMA 來擷取 XML 結構描述資訊。 SS_XMLSCHEMA 資料列集包含下列資料行：  
  
|資料行名稱|類型|Description|  
|-----------------|----------|-----------------|  
|SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 集合所屬的目錄。|  
|SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 集合所屬的結構描述。|  
|SCHEMACOLLECTIONNAME|DBTYPE_WSTR|具類型的 XML 資料行之 XML 結構描述集合的名稱，否則為 NULL。|  
|TARGETNAMESPACEURI|DBTYPE_WSTR|XML 結構描述的目標命名空間。|  
|SCHEMACONTENT|DBTYPE_WSTR|XML 結構描述內容。|  
  
 每個 XML 結構描述都是由目錄名稱、結構描述名稱、結構描述集合名稱，以及目標命名空間統一資源識別碼 (URI) 來限定範圍。 此外，也會定義名稱為 DBSCHEMA_XML_COLLECTIONS 的新 GUID。 限制的數目以及限制的 SS_XMLSCHEMA 結構描述資料列集資料行定義如下。  
  
|GUID|限制的數目|限制的資料行|  
|----------|----------------------------|------------------------|  
|DBSCHEMA_XML_COLLECTIONS|4|SCHEMACOLLECTION_CATALOGNAME<br /><br /> SCHEMACOLLECTION_SCHEMANAME<br /><br /> SCHEMACOLLECTIONNAME<br /><br /> TARGETNAMESPACEURI|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>OLE DB 屬性集的加入和變更  
 OLE DB Driver for SQL Server 加入新的值或變更加入到許多核心 OLE DB 屬性集。  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER 屬性集  
 為了透過 OLE DB 支援 **xml** 資料類型，OLE DB Driver for SQL Server 會實作新的 DBPROPSET_SQLSERVERPARAMETER 屬性集，其中包含以下值。  
  
|[屬性]|類型|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|定義 XML 結構描述集合所在目錄 (資料庫) 的名稱。 SQL 三部分名稱識別碼的一部分。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|結構描述集合內，XML 結構描述的名稱。 SQL 三部分名稱識別碼的一部分。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|在 SQL 三部分名稱識別碼的目錄 A 部分中，XML 結構描述集合的名稱。|  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN 屬性集  
 為了支援 **ITableDefinition** 介面中的資料表建立，OLE DB Driver for SQL Server 會將三個新的資料行新增到 DBPROPSET_SQLSERVERCOLUMN 屬性集。  
  
|[屬性]|類型|Description|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|如果是具類型的 XML 資料行，這個屬性是指定儲存 XML 結構描述所在之目錄名稱的字串。 如果是其他資料行類型，這個屬性會傳回空字串。|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|如果是具類型的 XML 資料行，這個屬性是指定定義此資料行之 XML 結構描述名稱的字串。|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|如果是具類型的 XML 資料行，這個屬性是指定定義值之結構描述 XML 結構描述集合名稱的字串。|  
  
 如同 SSPROP_PARAM 值，這些所有屬性都是選擇性的，而且預設為空。 只有在指定 SSPROP_COL_XML_SCHEMACOLLECTIONNAME 時，才可能指定 SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME 和 SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME。 將 XML 傳遞到伺服器時，如果包含這些值，系統會針對目前的資料庫檢查這些值是否存在 (有效性)，並針對結構描述檢查執行個體資料。 在所有情況下，這些值必須全部為空或全部填入，才會有效。  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB 介面的加入和變更  
 OLE DB Driver for SQL Server 會將新的值，或變更到許多核心 OLE DB 介面。  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters 介面  
 為了透過 OLE DB 支援 **xml** 資料類型，OLE DB Driver for SQL Server 會實作一些變更，其中包括新增 [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) 介面。 這個新的介面繼承自核心的 OLE DB 介面 **ICommandWithParameters**。 除了繼承自 **ICommandWithParameters** 的三種方法 (**GetParameterInfo**、**MapParameterNames** 和 **SetParameterInfo**)，**ISSCommandWithParameters** 也提供用來處理伺服器特定資料類型的 [GetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md) 和 [SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) 方法。  
  
> [!NOTE]  
>  **ISSCommandWithParameters** 介面也會使用新的 SSPARAMPROPS 結構。  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset 介面  
 OLE DB Driver for SQL Server 會將下列 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 專屬的資料行新增到 **IColumnRowset::GetColumnsRowset** 方法所傳回的資料列集。 這些資料行包含 XML 結構描述集合的三部分名稱。 對於非 XML 資料行或不具類型的 XML 資料行，所有三個資料行都會使用 NULL 的預設值。  
  
|資料行名稱|類型|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 結構描述集合所屬的目錄，<br /><br /> 否則為 NULL。|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 結構描述集合所屬的結構描述， 否則為 NULL。|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|具類型的 XML 資料行之 XML 結構描述集合的名稱，否則為 NULL。|  
  
#### <a name="the-irowset-interface"></a>IRowset 介面  
 XML 資料行中的 XML 執行個體會透過 **IRowset::GetData** 方法擷取。 根據用戶端所指定的繫結，可以將 XML 執行個體當做 DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML、DBTYPE_STR、DBTYPE_BYTES 擷取，或透過 DBTYPE_IUNKNOWN，當做介面擷取。 如果取用者指定 DBTYPE_BSTR、DBTYPE_WSTR 或 DBTYPE_VARIANT，提供者會將 XML 執行個體轉換為使用者要求的類型，並將其放入對應繫結中所指定的位置。  
  
 如果取用者指定 DBTYPE_IUNKNOWN，並將 *pObject* 引數設定為 NULL，或將 *pObject* 引數設定為 IID_IsequentialStream，提供者會將 **ISequentialStream** 介面傳回到取用者，讓取用者可以用資料流的形式，將 XML 資料傳出資料行。 **ISequentialStream** 接著會傳回 XML 資料，作為 Unicode 字元資料流。  
  
 傳回繫結至 DBTYPE_IUNKNOWN 的 XML 值時，提供者會報告 `sizeof (IUnknown *)` 的大小值。 這個行為與資料行繫結為 DBTYPE_IUnknown 或 DBTYPE_IDISPATCH 時所採取的方法一致，而且在無法判斷確實的資料行大小時，與 DBTYPE_IUNKNOWN/ISequentialStream 所採取的方法一致。  
  
#### <a name="the-irowsetchange-interface"></a>IRowsetChange 介面  
 取用者可以在資料行中更新 XML 結構描述的方式有兩種。 第一種方式是透過提供者所建立的儲存物件 **ISequentialStream**。 取用者可以呼叫 **ISequentialStream::Write** 方法來直接更新提供者所傳回的 XML 執行個體。  
  
 第二個方式是透過 **IRowsetChange::SetData** 或 **IRowsetChange::InsertRow** 方法。 利用這個方式，取用者緩衝區中的 XML 執行個體可以在類型 DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML 或 DBTYPE_IUNKNOWN 的繫結中指定。  
  
 如果指定 DBTYPE_BSTR、DBTYPE_WSTR 或 DBTYPE_VARIANT，提供者會將位於取用者緩衝區中的 XML 執行個體儲存到適當的資料行中。  
  
 如果指定 DBTYPE_IUNKNOWN/ISequentialStream，當取用者沒有指定任何儲存物件時，取用者必須事先建立 **ISequentialStream** 物件、使用該物件繫結 XML 文件，然後透過 **IRowsetChange::SetData** 方法，將該物件傳遞到提供者。 取用者也可以建立儲存物件、將 pObject 引數設定為 IID_IsequentialStream、建立 **ISequentialStream** 物件，然後將 **ISequentialStream** 物件傳遞到 **IRowsetChange::SetData** 方法。 在兩種情況下，提供者可以透過 **ISequentialStream** 物件擷取 XML 物件，並將其插入到適當的資料行中。  
  
#### <a name="the-irowsetupdate-interface"></a>IRowsetUpdate 介面  
 **IRowsetUpdate** 介面提供延遲更新的功能。 提供給資料列集的資料在取用者呼叫 **IRowsetUpdate:Update** 方法之前，不會提供給其他交易使用。  
  
#### <a name="the-irowsetfind-interface"></a>IRowsetFind 介面  
 **IRowsetFind::FindNextRow** 方法無法搭配 **xml** 資料類型使用。 呼叫 **IRowsetFind::FindNextRow** 而且 *hAccessor* 引數指定 DBTYPE_XML 的資料行時，會傳回 DB_E_BADBINDINFO。 不管要搜尋的是什麼資料行類型，都會發生這個狀況。 對於其他任何繫結類型，如果要搜尋的資料行屬於 **xml** 資料類型，**FindNextRow** 會失敗並傳回 DB_E_BADCOMPAREOP。  
 
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
