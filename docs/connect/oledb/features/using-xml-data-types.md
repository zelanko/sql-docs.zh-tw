---
title: 使用 XML 資料類型 |Microsoft 文件
description: 使用 OLE DB 驅動程式中的 XML 資料類型，適用於 SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
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
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 97a28369b44dd42bd9e587db094c29d1911de1ec
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2018
---
# <a name="using-xml-data-types"></a>使用 XML 資料類型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]導入**xml**資料型別，可讓您儲存 XML 文件和片段中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫。 **Xml**資料類型是中的內建資料型別[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，而且在某些方面類似於其他內建類型，例如**int**和**varchar**。 您可以使用其他內建類型， **xml**資料類型當做建立資料表時的資料行類型; 當做變數類型、 參數類型或函數傳回的類型; 或者在 CAST 和 CONVERT 函數。  
  
## <a name="programming-considerations"></a>程式設計考量  
 XML 可以是自我描述的，因為它可以選擇性地包含指定文件編碼的 XML 標頭，例如：  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 XML 標準描述 XML 處理器如何透過檢查文件的前幾個位元組來偵測用於文件的編碼。 應用程式所指定的編碼有時候會與文件所指定的編碼產生衝突。 對於當做繫結參數傳遞的文件，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會將 XML 視為二進位資料，因此不需要進行轉換，而且 XML 剖析器可以毫無問題地使用在文件中指定的編碼。 不過，對於繫結為 WSTR 的 XML 資料，則應用程式必須確認文件的編碼為 Unicode。 將文件載入 DOM、 變更為 Unicode，編碼方式和序列化文件，可能會發生這種情況。 如果未進行此步驟中，資料轉換可能會發生，產生的 XML 無效或損毀。  
  
 以常值指定 XML 時，也有可能發生衝突。 例如，下列內容無效：  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="ole-db-driver-for-sql-server"></a>SQL Server 的 OLE DB 驅動程式 
 DBTYPE_XML 是新的資料類型的特定 SQL Server OLE DB 驅動程式中的 XML。 此外，XML 資料可以透過 DBTYPE_BYTES、DBTYPE_WSTR、DBTYPE_BSTR、DBTYPE_XML、DBTYPE_STR、DBTYPE_VARIANT 和 DBTYPE_IUNKNOWN 的現有 OLE DB 類型進行存取。 可以從下列格式的資料列集 SQL Server OLE DB 驅動程式中的資料行擷取儲存在 XML 類型資料行的資料：  
  
-   文字字串  
  
-   **ISequentialStream**  
  
> [!NOTE]  
>  SQL Server OLE DB 驅動程式不包含 SAX 讀取器，但**ISequentialStream**可以輕鬆地傳遞到 MSXML 中的 SAX 和 DOM 物件。  
  
 **ISequentialStream**應該用於擷取大型 XML 文件。 用於其他大數值類型的相同技術也適用於 XML。 如需詳細資訊，請參閱[使用大型值型別](../../oledb/features/using-large-value-types.md)。  
  
 也可以擷取資料列集中的 XML，類型的資料行中儲存的資料，來插入或更新應用程式，透過的一般介面例如**irow:: Getcolumns**， **irowchange::**，和**icommand:: Execute**。 同樣地擷取的情況下，應用程式可以傳遞的文字字串或**ISequentialStream**至 SQL Server OLE DB 驅動程式。  
  
> [!NOTE]  
>  若要將 XML 資料字串格式，透過**ISequentialStream**介面，您必須取得**ISequentialStream**藉由指定 DBTYPE_IUNKNOWN，並設定其*pObject*繫結中的 null 引數。  
  
 當擷取的 XML 資料因為取用者緩衝區太小而遭到截斷時，可以會將長度傳回為 0xffffffff，這表示長度不明。 這是與它的實作一致為串流至用戶端，而不傳送實際資料的長度資訊的資料型別。 在某些情況下，實際長度可能會傳回提供者已經緩衝整個值，例如當**irowset:: Getdata**和執行資料轉換。  
  
 伺服器會將傳送到 SQL Server 的 XML 資料視為二進位資料。 此行為可避免發生任何轉換，並允許 XML 剖析器自動偵測 XML 編碼方式。 這樣可以接受各種 XML 文件 (例如，以 UTF-8 編碼的文件) 做為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的輸入。  
  
 如果輸入 XML 繫結為 DBTYPE_WSTR，應用程式必須確定它已經使用 Unicode 編碼，才能避免因為不需要的資料轉換造成損毀的可能性。  
  
### <a name="data-bindings-and-coercions"></a>資料繫結和強制型轉  
 下表描述的繫結和使用列出的資料類型使用時所發生強制型轉[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **xml**資料型別。  
  
|資料類型|到伺服器<br /><br /> **XML**|到伺服器<br /><br /> **非 XML**|從伺服器<br /><br /> **XML**|從伺服器<br /><br /> **非 XML**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|通過<sup>6,7</sup>|錯誤<sup>1</sup>|確定<sup>11，6</sup>|錯誤<sup>8</sup>|  
|DBTYPE_BYTES|通過<sup>6,7</sup>|N/A<sup>2</sup>|確定<sup>11，6</sup>|N/A <sup>2</sup>|  
|DBTYPE_WSTR|通過<sup>6，10</sup>|N/A <sup>2</sup>|確定<sup>4、 6、 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_BSTR|通過<sup>6，10</sup>|N/A <sup>2</sup>|OK <sup>3</sup>|N/A <sup>2</sup>|  
|DBTYPE_STR|確定<sup>6、 9、 10</sup>|N/A <sup>2</sup>|確定<sup>5、 6、 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_IUNKNOWN|位元組資料流透過**ISequentialStream**<sup>7</sup>|N/A <sup>2</sup>|位元組資料流透過**ISequentialStream**<sup>11</sup>|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|通過<sup>6,7</sup>|N/A <sup>2</sup>|해당 사항 없음|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|通過<sup>6，10</sup>|N/A <sup>2</sup>|OK<sup>3</sup>|N/A <sup>2</sup>|  
  
 <sup>1</sup>如果的伺服器類型與指定 DBTYPE_XML 以外**icommandwithparameters:: Setparameterinfo**和存取子類型為 DBTYPE_XML，陳述式執行時，就會發生錯誤 （DB_E_ERRORSOCCURRED，參數狀態為 DBSTATUS_E_BADACCESSOR）; 否則將資料傳送到伺服器，但是伺服器會傳回錯誤，指出從 XML 到參數的資料類型的隱含轉換。  
  
 <sup>2</sup>超出本文的範圍。  
  
 <sup>3</sup>格式為 utf-16，無位元組順序標示 (BOM)，無編碼規格，無 null 結束。  
  
 <sup>4</sup>格式為 utf-16，BOM，無編碼規格，null 結束。  
  
 <sup>5</sup>格式是用戶端字碼頁搭配 null 結束字元編碼的多位元組字元。 轉換從伺服器提供的 Unicode 可能會造成資料損毀，因此不建議使用這個繫結。  
  
 <sup>6</sup>可能會使用 BY_REF。  
  
 <sup>7</sup>utf-16 資料必須以 BOM 開頭。 如果不是，伺服器可能無法正確辨識編碼。  
  
 <sup>8</sup>驗證建立存取子或提取時可能發生在。 錯誤為 DB_E_ERRORSOCCURRED，繫結狀態設定為 DBBINDSTATUS_UNSUPPORTEDCONVERSION。  
  
 <sup>9</sup>資料會轉換成 Unicode 使用用戶端字碼頁，再傳送至伺服器。 如果文件的編碼方式不符合用戶端字碼頁，可能發生資料損毀，因此強烈建議您不要此繫結。  
  
 <sup>10</sup>BOM 永遠會加入至傳送到伺服器的資料。 如果資料已經啟動以包含 BOM，緩衝區開頭會有兩個 Bom。 伺服器會使用第一個 BOM 將編碼識別為 UTF-16，然後再捨棄它。 第二個 BOM 會解譯為零寬度的不分行空格字元。  
  
 <sup>11</sup>格式為 utf-16，無編碼規格，BOM 會加入至從伺服器收到的資料。 如果伺服器傳回空字串，仍然會將 BOM 傳回到應用程式。 如果緩衝區長度為奇數位元組，則會正確地截斷資料。 如果在區塊中傳回整個值，可以串連這些區塊以重新組成正確的值。  
  
 <sup>12</sup>如果緩衝區長度少於兩個字元-也就是說，沒有足夠的空間給 null 結束-報告溢位錯誤。  
  
> [!NOTE]  
>  NULL XML 值不會傳回任何資料。  
  
 XML 標準需要以 UTF-16 編碼的 XML 來開始位元組順序標示 (BOM)，UTF-16 字元程式碼 0xFEFF。 當使用 WSTR 和 BSTR 繫結，OLE DB 驅動程式的 SQL Server 就不需要或加入 BOM 做為繫結所默許的編碼方式。 使用 BYTES、XML 或 IUNKNOWN 繫結時，其用意在於提供處理其他 XML 處理器和儲存系統的單純性。 在此情況下，BOM 應該會出現以 utf-16 編碼的 XML，而且應用程式不需要在意實際編碼，因為多數 XML 處理器 （包括 SQL Server） 會推算藉由檢查值的前幾個位元組的編碼方式。 XML 資料從 OLE DB 驅動程式收到適用於 SQL Server 使用位元組，XML 或 IUNKNOWN 繫結永遠以 utf-16 BOM 或內嵌編碼宣告無編碼。  
  
 OLE DB 核心服務所提供的資料轉換 (**IDataConvert**) 不適用於 DBTYPE_XML。  
  
 當資料傳送到伺服器時，會執行驗證。 應由您的應用程式處理用戶端驗證和編碼變更。 建議您不直接處理 XML 資料，但是應該改用 DOM 或 SAX 讀取器來處理它。  
  
 可以繫結 DBTYPE_NULL 和 DBTYPE_EMPTY 用於輸入參數，但是不能用於輸出參數或結果。 當針對輸入參數來繫結時，狀態必須設定為 DBSTATUS_S_ISNULL 或 DBSTATUS_S_DEFAULT。  
  
 DBTYPE_XML 可以轉換成 DBTYPE_EMPTY，而 DBTYPE_NULL、DBTYPE_EMPTY 可以轉換成 DBTYPE_XML，但是 DBTYPE_NULL 無法轉換成 DBTYPE_XML。 這與 DBTYPE_WSTR 一致。  
  
 DBTYPE_IUNKNOWN 是支援的繫結 （如下所示在上表中），但沒有 DBTYPE_XML 和 DBTYPE_IUNKNOWN 之間轉換。 DBTYPE_IUNKNOWN 可能無法搭配 DBTYPE_BYREF 使用。  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 資料列集的加入和變更  
 OLE DB 驅動程式的 SQL Server 加入新的值，或變更到許多核心 OLE DB 結構描述資料列。  
  
#### <a name="the-columns-and-procedureparameters-schema-rowsets"></a>COLUMNS 和 PROCEDURE_PARAMETERS 結構描述資料列集  
 COLUMNS 和 PROCEDURE_PARAMETERS 結構描述資料列的新增項目包括下列資料行：  
  
|資料行名稱|類型|Description|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|定義 XML 結構描述集合所在目錄的名稱。 非 XML 資料行或不具類型的 XML 資料行是 NULL。|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|定義 XML 結構描述集合所在結構描述的名稱。 非 XML 資料行或不具類型的 XML 資料行是 NULL。|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|XML 結構描述集合的名稱。 非 XML 資料行或不具類型的 XML 資料行是 NULL。|  
  
#### <a name="the-providertypes-schema-rowset"></a>PROVIDER_TYPES 結構描述資料列集  
 在 PROVIDER_TYPES 結構描述資料列集，COLUMN_SIZE 值是 0 代表**xml**資料型別，而 DATA_TYPE 為 DBTYPE_XML。  
  
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
 OLE DB 驅動程式的 SQL Server 會將新值加入或變更加入到許多核心 OLE DB 屬性集。  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER 屬性集  
 為了支援**xml**資料類型到 OLE DB、 OLE DB 驅動程式的 SQL Server 會實作新的 DBPROPSET_SQLSERVERPARAMETER 屬性集，其中包含下列值。  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|定義 XML 結構描述集合所在目錄 (資料庫) 的名稱。 SQL 三部分名稱識別碼的一部分。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|結構描述集合內，XML 結構描述的名稱。 SQL 三部分名稱識別碼的一部分。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|在 SQL 三部分名稱識別碼的目錄 A 部分中，XML 結構描述集合的名稱。|  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN 屬性集  
 若要支援中的資料表建立**ITableDefinition**介面、 OLE DB 驅動程式的 SQL Server 會將三個新的資料行加入到 DBPROPSET_SQLSERVERCOLUMN 屬性集。  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|如果是具類型的 XML 資料行，這個屬性是指定儲存 XML 結構描述所在之目錄名稱的字串。 如果是其他資料行類型，這個屬性會傳回空字串。|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|如果是具類型的 XML 資料行，這個屬性是指定定義此資料行之 XML 結構描述名稱的字串。|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|如果是具類型的 XML 資料行，這個屬性是指定定義值之結構描述 XML 結構描述集合名稱的字串。|  
  
 如同 SSPROP_PARAM 值，這些所有屬性都是選擇性的，而且預設為空。 只有在指定 SSPROP_COL_XML_SCHEMACOLLECTIONNAME 時，才可能指定 SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME 和 SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME。 將 XML 傳遞到伺服器時，如果包含這些值，系統會針對目前的資料庫檢查這些值是否存在 (有效性)，並針對結構描述檢查執行個體資料。 在所有情況下，這些值必須全部為空或全部填入，才會有效。  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB 介面的加入和變更  
 OLE DB 驅動程式的 SQL Server 會將新的值，或變更到許多核心 OLE DB 介面。  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters 介面  
 為了支援**xml** OLE DB 驅動程式的 SQL Server 透過 OLE DB 的資料類型會實作一些變更包括加入[ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)介面。 這個新介面繼承自核心的 OLE DB 介面**ICommandWithParameters**。 除了繼承自的三種方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，和**SetParameterInfo**;**ISSCommandWithParameters**提供[GetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)和[SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)用來處理伺服器特定的方法資料型別。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**介面也可使用新的 ssparamprops 結構。  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset 介面  
 OLE DB 驅動程式的 SQL Server 會加入下列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-專屬的資料行所傳回的資料列集**icolumnrowset:: Getcolumnsrowset**方法。 這些資料行包含 XML 結構描述集合的三部分名稱。 對於非 XML 資料行或不具類型的 XML 資料行，所有三個資料行都會使用 NULL 的預設值。  
  
|資料行名稱|類型|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 結構描述集合所屬的目錄，<br /><br /> 否則為 NULL。|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 結構描述集合所屬的結構描述， 否則為 NULL。|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|具類型的 XML 資料行之 XML 結構描述集合的名稱，否則為 NULL。|  
  
#### <a name="the-irowset-interface"></a>IRowset 介面  
 XML 資料行中的 XML 執行個體透過擷取**irowset:: Getdata**方法。 根據用戶端所指定的繫結，可以將 XML 執行個體當做 DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML、DBTYPE_STR、DBTYPE_BYTES 擷取，或透過 DBTYPE_IUNKNOWN，當做介面擷取。 如果取用者指定 DBTYPE_BSTR、DBTYPE_WSTR 或 DBTYPE_VARIANT，提供者會將 XML 執行個體轉換為使用者要求的類型，並將其放入對應繫結中所指定的位置。  
  
 如果取用者指定 DBTYPE_IUNKNOWN，並設定*pObject*引數為 NULL 或設定*pObject*引數為 IID_ISequentialStream，提供者會傳回**ISequentialStream**介面讓取用者，因此取用者可以串流 XML 資料傳出資料行。 **ISequentialStream**則會傳回 XML 資料做為 Unicode 字元資料流。  
  
 傳回繫結至 DBTYPE_IUNKNOWN 的 XML 值時，提供者會報告 `sizeof (IUnknown *)` 的大小值。 這是與資料行繫結為 DBTYPE_IUnknown 或 DBTYPE_IDISPATCH，和 DBTYPE_IUNKNOWN/ISequentialStream 所無法判斷精確的資料行大小時採取的方法一致。  
  
#### <a name="the-irowsetchange-interface"></a>IRowsetChange 介面  
 取用者可以在資料行中更新 XML 結構描述的方式有兩種。 第一個是透過儲存體物件**ISequentialStream**提供者所建立。 取用者可以呼叫**isequentialstream:: Write**方法來直接更新提供者所傳回的 XML 執行個體。  
  
 第二種方法是透過**irowsetchange:: Setdata**或**irowsetchange:: Insertrow**方法。 利用這個方式，取用者緩衝區中的 XML 執行個體可以在類型 DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML 或 DBTYPE_IUNKNOWN 的繫結中指定。  
  
 如果指定 DBTYPE_BSTR、 DBTYPE_WSTR 或 DBTYPE_VARIANT，提供者會儲存成適當的資料行位於取用者緩衝區之 XML 執行個體。  
  
 取用者指定 DBTYPE_IUNKNOWN/ISequentialStream，如果取用者未指定任何儲存物件時，如果必須建立**ISequentialStream**事先物件、 繫結物件時，XML 文件，然後再傳遞透過提供者的物件**irowsetchange:: Setdata**方法。 取用者也可以建立儲存體物件、 將 pObject 引數設定為 IID_ISequentialStream、 建立**ISequentialStream**物件，然後再傳遞**ISequentialStream**物件**irowsetchange:: Setdata**方法。 在這兩種情況下，提供者可以擷取 XML 物件透過**ISequentialStream**物件，並將其插入到適當的資料行。  
  
#### <a name="the-irowsetupdate-interface"></a>IRowsetUpdate 介面  
 **IRowsetUpdate**介面提供延遲更新的功能。 提供給資料列集的資料不供其他交易直到取用者呼叫**irowsetupdate:: Update**方法。  
  
#### <a name="the-irowsetfind-interface"></a>IRowsetFind 介面  
 **Irowsetfind:: Findnextrow**方法不適用於**xml**資料型別。 當**irowsetfind:: Findnextrow**稱為和*hAccessor*引數指定 DBTYPE_XML 的資料行，會傳回 DB_E_BADBINDINFO。 不管要搜尋的是什麼資料行類型，都會發生這個狀況。 其他繫結型別， **FindNextRow**包含 DB_E_BADCOMPAREOP 失敗時，如果要搜尋的資料行的**xml**資料型別。  
 
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 功能的 OLE DB 驅動程式](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
