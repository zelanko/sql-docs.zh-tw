---
title: 適用于 Microsoft Jet 的 microsoft OLE DB 提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69d88aebe25f6cfa5490cce736c05780b87eee6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926640"
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Microsoft OLE DB Provider for Microsoft Jet 總覽
適用于 Microsoft Jet 的 OLE DB 提供者可讓 ADO 存取 Microsoft Jet 資料庫。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到這個提供者，請將[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性的*provider*引數設定為下列內容：

```vb
Microsoft.Jet.OLEDB.4.0
```

 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性也會傳回這個字串。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串為：

```vb
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 此字串包含下列關鍵字：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 Microsoft Jet 的 OLE DB 提供者。|
|**資料來源**|指定資料庫路徑和檔案名（例如， `c:\Northwind.mdb`）。|
|**使用者識別碼**|指定使用者名稱。 如果未指定此關鍵字，則預設會使用字串`admin`""。|
|**密碼**|指定使用者密碼。 如果未指定此關鍵字，則預設會使用空字串（""）。|

> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定**Trusted_Connection = yes**或**整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。

## <a name="provider-specific-connection-parameters"></a>提供者特定的連接參數
 除了 ADO 所定義的屬性以外，Microsoft Jet 的 OLE DB 提供者也支援數個提供者特定的動態內容。 如同所有其他**連接**參數，您可以使用**Connection**物件的**Properties**集合或連接字串的一部分來設定它們。

 下表列出這些屬性，以及括弧中對應的 OLE DB 屬性名稱。

|參數|描述|
|---------------|-----------------|
|Jet OLEDB：精簡回收的空間數量（DBPROP_JETOLEDB_COMPACTFREESPACESIZE）|表示壓縮資料庫可回收的空間量估計（以位元組為單位）。 只有在建立資料庫連接之後，這個值才有效。|
|Jet OLEDB：連接控制（DBPROP_JETOLEDB_CONNECTIONCONTROL）|指出使用者是否可以連接到資料庫。|
|Jet OLEDB：建立系統資料庫（DBPROP_JETOLEDB_CREATESYSTEMDATABASE）|指出建立新的資料來源時是否應該建立系統資料庫。|
|Jet OLEDB：資料庫鎖定模式（DBPROP_JETOLEDB_DATABASELOCKMODE）|表示此資料庫的鎖定模式。 開啟資料庫的第一個使用者會決定資料庫開啟時所使用的模式。|
|Jet OLEDB：資料庫密碼（DBPROP_JETOLEDB_DATABASEPASSWORD）|指出資料庫密碼。|
|Jet OLEDB：不復制 Compact 的地區設定（DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE）|指出當壓縮資料庫時，Jet 是否應複製地區設定資訊。|
|Jet OLEDB：加密資料庫（DBPROP_JETOLEDB_ENCRYPTDATABASE）|指出是否應該加密壓縮的資料庫。 如果未設定此屬性，當原始資料庫也已加密時，壓縮的資料庫將會加密。|
|Jet OLEDB：引擎類型（DBPROP_JETOLEDB_ENGINE）|表示用來存取目前資料存放區的儲存引擎。|
|Jet OLEDB：獨佔非同步延遲（DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY）|指出當以獨佔方式開啟資料庫時，Jet 可以延遲非同步寫入磁片的時間長度上限（以毫秒為單位）。<br /><br /> 除非**JET OLEDB： Flush Transaction Timeout**設定為0，否則會忽略這個屬性。|
|Jet OLEDB： Flush Transaction Timeout （DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT）|指出儲存在快取中以供非同步寫入的資料實際寫入磁片之前，所要等待的時間量。 此設定會覆寫 [ **JET oledb：共用非同步延遲**] 和 [ **Jet Oledb：獨佔非同步延遲**] 的值。|
|Jet OLEDB：全域大量交易（DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS）|指出是否已交易 SQL 大量交易。|
|Jet OLEDB：全域部分大量作業（DBPROP_JETOLEDB_GLOBALBULKPARTIAL）|指出用來開啟資料庫的密碼。|
|Jet OLEDB：隱含認可同步處理（DBPROP_JETOLEDB_IMPLICITCOMMITSYNC）|指出是否以同步或非同步模式寫入內部隱含交易中所做的變更。|
|Jet OLEDB：鎖定延遲（DBPROP_JETOLEDB_LOCKDELAY）|表示在先前的嘗試失敗之後嘗試取得鎖定之前，要等候的毫秒數。|
|Jet OLEDB：鎖定重試（DBPROP_JETOLEDB_LOCKRETRY）|指出多次嘗試存取鎖定頁面的次數。|
|Jet OLEDB：緩衝區大小上限（DBPROP_JETOLEDB_MAXBUFFERSIZE）|表示在開始排清磁片的變更之前，Jet 可以使用的記憶體數量上限（以 kb 為單位）。|
|Jet OLEDB：每個檔案的鎖定上限（DBPROP_JETOLEDB_MAXLOCKSPERFILE）|指出 Jet 可以在資料庫上放置的鎖定數目上限。 預設值為9500。|
|Jet OLEDB：新的資料庫密碼（DBPROP_JETOLEDB_NEWDATABASEPASSWORD）|指出要為此資料庫設定的新密碼。 舊密碼會儲存在**JET OLEDB：資料庫密碼**中。|
|Jet OLEDB： ODBC 命令逾時（DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT）|表示從 Jet 進行遠端 ODBC 查詢超時之前的毫秒數。|
|Jet OLEDB：鎖定資料表的頁面（DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK）|指出在 Jet 嘗試將鎖定升級為表鎖之前，必須在交易中鎖定的頁數。 如果此值為0，則永遠不會升級鎖定。|
|Jet OLEDB：頁面超時（DBPROP_JETOLEDB_PAGETIMEOUT）|指出 Jet 在檢查其快取是否已過期資料庫檔案之前，會等待的毫秒數。|
|Jet OLEDB：回收長值頁面（DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES）|指出 Jet 是否應該積極地嘗試在釋放 BLOB 頁面時進行回收。|
|Jet OLEDB：登錄路徑（DBPROP_JETOLEDB_REGPATH）|表示包含 Jet 資料庫引擎值的 Windows 登錄機碼。|
|Jet OLEDB：重設 ISAM 統計資料（DBPROP_JETOLEDB_RESETISAMSTATS）|指出架構**記錄集**DBSCHEMA_JETOLEDB_ISAMSTATS 是否應該在傳回效能資訊之後重設其效能計數器。|
|Jet OLEDB：共用的非同步延遲（DBPROP_JETOLEDB_SHAREDASYNCDELAY）|表示在多使用者模式中開啟資料庫時，Jet 可以延遲非同步寫入磁片的最大時間量（以毫秒為單位）。|
|Jet OLEDB：系統資料庫（DBPROP_JETOLEDB_SYSDBPATH）|指出工作組資訊檔案（系統資料庫）的路徑和檔案名。|
|Jet OLEDB：交易認可模式（DBPROP_JETOLEDB_TXNCOMMITMODE）|指出當認可交易時，Jet 會同步或非同步地將資料寫入磁片。|
|Jet OLEDB：使用者認可同步處理（DBPROP_JETOLEDB_USERCOMMITSYNC）|指出在交易中所做的變更是否以同步或非同步模式寫入。|

## <a name="provider-specific-recordset-and-command-properties"></a>提供者特定的記錄集和命令屬性
 Jet 提供者也支援數個提供者特定的**記錄集**和**命令**屬性。 這些屬性是透過**記錄集**或**命令**物件的**properties**集合來存取和設定。 資料表會列出 ADO 屬性名稱及其對應的 OLE DB 屬性名稱（以括弧括住）。

|屬性名稱|描述|
|-------------------|-----------------|
|Jet OLEDB：大量交易（DBPROP_JETOLEDB_BULKNOTRANSACTIONS）|指出 SQL 大量作業是否已交易。 由於資源延遲，大型大量作業可能會在交易時失敗。|
|Jet OLEDB：啟用 Fat 資料指標（DBPROP_JETOLEDB_ENABLEFATCURSOR）|指出當填入遠端資料列來源的記錄集時，Jet 是否應快取多個資料列。|
|Jet OLEDB： Fat 資料指標快取大小（DBPROP_JETOLEDB_FATCURSORMAXROWS）|指出使用遠端資料存放區資料列快取時要快取的資料列數目。 除非**JET OLEDB：啟用 Fat 資料指標**為 True，否則會忽略此值。|
|Jet OLEDB：不一致（DBPROP_JETOLEDB_INCONSISTENT）|指出查詢結果是否允許不一致的更新。|
|Jet OLEDB：鎖定資料細微性（DBPROP_JETOLEDB_LOCKGRANULARITY）|指出是否使用資料列層級鎖定來開啟資料表。|
|Jet OLEDB： ODBC 傳遞語句（DBPROP_JETOLEDB_ODBCPASSTHROUGH）|表示 Jet 應不改變地將**命令**物件中的 SQL 文字傳遞給後端。|
|Jet OLEDB：部分大量作業（DBPROP_JETOLEDB_BULKPARTIAL）|指出當 SQL DML 作業失敗時，Jet 的行為。|
|Jet OLEDB：通過查詢大量作業（DBPROP_JETOLEDB_PASSTHROUGHBULKOP）|指出不傳回**記錄集**的查詢是否原封不動地傳遞至資料來源。|
|Jet OLEDB：傳遞查詢連接字串（DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING）|表示用來連接到遠端資料存放區的 Jet 連接字串。 除非**JET OLEDB： ODBC 傳遞語句**為 True，否則會忽略此值。|
|Jet OLEDB：預存查詢（DBPROP_JETOLEDB_STOREDQUERY）|指出是否應將命令文字解讀為預存查詢，而不是 SQL 命令。|
|Jet OLEDB：驗證設定的規則（DBPROP_JETOLEDB_VALIDATEONSET）|指出當設定資料行資料或將變更認可至資料庫時，是否要評估 Jet 驗證規則。|

 根據預設，OLE DB Provider for Microsoft Jet 會以讀取/寫入模式開啟 Microsoft Jet 資料庫。 若要在唯讀模式中開啟資料庫，請將 ADO **Connection**物件上的[mode](../../../ado/reference/ado-api/mode-property-ado.md)屬性設定為**adModeRead**。

## <a name="command-object-usage"></a>命令物件使用方式
 [命令](../../../ado/reference/ado-api/command-object-ado.md)物件中的命令文字會使用 MICROSOFT Jet SQL 用語。 您可以在命令文字中指定資料列傳回的查詢、動作查詢和資料表名稱;不過，不支援預存程式，且不應指定。

## <a name="recordset-behavior"></a>記錄集行為
 Microsoft Jet 資料庫引擎不支援動態資料指標。 因此，適用于 Microsoft Jet 的 OLE DB 提供者不支援**adLockDynamic**資料指標類型。 當要求動態資料指標時，提供者會傳回索引鍵集資料指標，並重設[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)屬性，以指出所傳回之[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的類型。 此外，如果要求可更新的**記錄集**（**LockType**是**adLockOptimistic**、 **adLockBatchOptimistic**或**adLockPessimistic**），提供者也會傳回索引鍵集資料指標，並重設**CursorType**屬性。

## <a name="dynamic-properties"></a>動態屬性
 適用于 Microsoft Jet 的 OLE DB 提供者會將數個動態屬性插入至未打開之[連接](../../../ado/reference/ado-api/connection-object-ado.md)、[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)和[命令](../../../ado/reference/ado-api/command-object-ado.md)物件的**properties**集合中。

 下表是每個動態屬性的 ADO 和 OLE DB 名稱的交互索引。 OLE DB 程式設計人員參考以「描述」一詞指的是 ADO 屬性名稱。 您可以在 OLE DB 程式設計人員參考中找到這些屬性的詳細資訊。

## <a name="connection-dynamic-properties"></a>連接動態屬性
 下列屬性會加入至**Connection**物件的**properties**集合中。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|Active Sessions|DBPROP_ACTIVESESSIONS|
|非同步中止|DBPROP_ASYNCTXNABORT|
|非同步認可|DBPROP_ASYNCTNXCOMMIT|
|自動認可隔離等級|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|目錄位置|DBPROP_CATALOGLOCATION|
|目錄詞彙|DBPROP_CATALOGTERM|
|資料行定義|DBPROP_COLUMNDEFINITION|
|目前的目錄|DBPROP_CURRENTCATALOG|
|資料來源|DBPROP_INIT_DATASOURCE|
|資料來源名稱|DBPROP_DATASOURCENAME|
|資料來源物件執行緒模型|DBPROP_DSOTHREADMODEL|
|DBMS 名稱|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|群組依據支援|DBPROP_GROUPBY|
|異質資料表支援|DBPROP_HETEROGENEOUSTABLES|
|識別碼區分大小寫|DBPROP_IDENTIFIERCASE|
|隔離等級|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔離保留|DBPROP_SUPPORTEDTXNISORETAIN|
|地區設定識別碼|DBPROP_INIT_LCID|
|索引大小上限|DBPROP_MAXINDEXSIZE|
|最大資料列大小|DBPROP_MAXROWSIZE|
|最大資料列大小包含 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT 中的資料表上限|DBPROP_MAXTABLESINSELECT|
|模式|DBPROP_INIT_MODE|
|多個參數集|DBPROP_MULTIPLEPARAMSETS|
|多個結果|DBPROP_MULTIPLERESULTS|
|多個儲存物件|DBPROP_MULTIPLESTORAGEOBJECTS|
|多資料表更新|DBPROP_MULTITABLEUPDATE|
|Null 定序順序|DBPROP_NullCOLLATION|
|Null 串連行為|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 版本|DBPROP_PROVIDEROLEDBVER|
|OLE 物件支援|DBPROP_OLEOBJECTS|
|開放式資料列集支援|DBPROP_OPENROWSETSUPPORT|
|選取清單中的 ORDER BY 資料行|DBPROP_ORDERBYCOLUMNSINSELECT|
|輸出參數可用性|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|以 Ref 存取子傳遞|DBPROP_BYREFACCESSORS|
|密碼|DBPROP_AUTH_PASSWORD|
|持續性識別碼類型|DBPROP_PERSISTENTIDTYPE|
|準備中止行為|DBPROP_PREPAREABORTBEHAVIOR|
|準備認可行為|DBPROP_PREPARECOMMITBEHAVIOR|
|程式詞彙|DBPROP_PROCEDURETERM|
|Prompt|DBPROP_INIT_PROMPT|
|提供者易記名稱|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|提供者版本|DBPROP_PROVIDERVER|
|唯讀資料來源|DBPROP_DATASOURCEREADONLY|
|命令上的資料列集轉換|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|架構詞彙|DBPROP_SCHEMATERM|
|架構使用方式|DBPROP_SCHEMAUSAGE|
|SQL 支援|DBPROP_SQLSUPPORT|
|結構化儲存體|DBPROP_STRUCTUREDSTORAGE|
|子查詢支援|DBPROP_SUBQUERIES|
|資料表詞彙|DBPROP_TABLETERM|
|交易 DDL|DBPROP_SUPPORTEDTXNDDL|
|使用者識別碼|DBPROP_AUTH_USERID|
|使用者名稱|DBPROP_USERNAME|
|視窗控制碼|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>記錄集動態屬性
 下列屬性會加入至**記錄集**物件的**properties**集合中。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|僅附加資料列集|DBPROP_APPENDONLY|
|封鎖儲存物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書簽類型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|已排序書簽|DBPROP_ORDEREDBOOKMARKS|
|快取延遲的資料行|DBPROP_CACHEDEFERRED|
|變更插入的資料列|DBPROP_CHANGEINSERTEDROWS|
|資料行許可權|DBPROP_COLUMNRESTRICT|
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|
|資料行可寫入|DBPROP_MAYWRITECOLUMN|
|延遲資料行|DBPROP_DEFERRED|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後提取|DBPROP_CANFETCHBACKWARDS|
|保留資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|固定資料列|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|常值書簽|DBPROP_LITERALBOOKMARKS|
|常值資料列識別|DBPROP_LITERALIDENTITY|
|最大開啟資料列|DBPROP_MAXOPENROWS|
|暫止資料列數上限|DBPROP_MAXPENDINGROWS|
|最大資料列數|DBPROP_MAXROWS|
|記憶體使用量|DBPROP_MEMORYUSAGE|
|通知資料細微性|DBPROP_NOTIFICATIONGRANULARITY|
|通知階段|DBPROP_NOTIFICATIONPHASES|
|物件交易|DBPROP_TRANSACTEDOBJECT|
|其他變更可見|DBPROP_OTHERUPDATEDELETE|
|其他的插入可見|DBPROP_OTHERINSERT|
|可見的變更|DBPROP_OWNUPDATEDELETE|
|可見的插入|DBPROP_OWNINSERT|
|中止時保留|DBPROP_ABORTPRESERVE|
|在認可時保留|DBPROP_COMMITPRESERVE|
|快速重新開機|DBPROP_QUICKRESTART|
|重新進入事件|DBPROP_REENTRANTEVENTS|
|移除已刪除的資料列|DBPROP_REMOVEDELETED|
|報告多項變更|DBPROP_REPORTMULTIPLECHANGES|
|傳回暫止的插入|DBPROP_RETURNPENDINGINSERTS|
|資料列刪除通知|DBPROP_NOTIFYROWDELETE|
|資料列第一次變更通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|資料列插入通知|DBPROP_NOTIFYROWINSERT|
|資料列許可權|DBPROP_ROWRESTRICT|
|資料列重新同步通知|DBPROP_NOTIFYROWRESYNCH|
|資料列執行緒模型|DBPROP_ROWTHREADMODEL|
|資料列復原變更通知|DBPROP_NOTIFYROWUNDOCHANGE|
|資料列恢復刪除通知|DBPROP_NOTIFYROWUNDODELETE|
|資料列復原插入通知|DBPROP_NOTIFYROWUNDOINSERT|
|資料列更新通知|DBPROP_NOTIFYROWUPDATE|
|資料列集提取位置變更通知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|資料列集發行通知|DBPROP_NOTIFYROWSETRELEASE|
|向後滾動|DBPROP_CANSCROLLBACKWARDS|
|略過已刪除的書簽|DBPROP_BOOKMARKSKIPPED|
|強式資料列識別|DBPROP_STRONGITDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用書簽|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令動態屬性
 下列屬性會加入至**Command**物件的**properties**集合中。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|僅附加資料列集|DBPROP_APPENDONLY|
|封鎖儲存物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書簽類型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|變更插入的資料列|DBPROP_CHANGEINSERTEDROWS|
|資料行許可權|DBPROP_COLUMNRESTRICT|
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|
|延遲資料行|DBPROP_DEFERRED|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後提取|DBPROP_CANFETCHBACKWARDS|
|保留資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|固定資料列|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|常值書簽|DBPROP_LITERALBOOKMARKS|
|常值資料列識別|DBPROP_LITERALIDENTITY|
|鎖定模式|DBPROP_LOCKMODE|
|最大開啟資料列|DBPROP_MAXOPENROWS|
|暫止資料列數上限|DBPROP_MAXPENDINGROWS|
|最大資料列數|DBPROP_MAXROWS|
|通知資料細微性|DBPROP_NOTIFICATIONGRANULARITY|
|通知階段|DBPROP_NOTIFICATIONPHASES|
|物件交易|DBPROP_TRANSACTEDOBJECT|
|其他變更可見|DBPROP_OTHERUPDATEDELETE|
|其他的插入可見|DBPROP_OTHERINSERT|
|可見的變更|DBPROP_OWNUPDATEDELETE|
|可見的插入|DBPROP_OWNINSERT|
|中止時保留|DBPROP_ABORTPRESERVE|
|在認可時保留|DBPROP_COMMITPRESERVE|
|快速重新開機|DBPROP_QUICKRESTART|
|重新進入事件|DBPROP_REENTRANTEVENTS|
|移除已刪除的資料列|DBPROP_REMOVEDELETED|
|報告多項變更|DBPROP_REPORTMULTIPLECHANGES|
|傳回暫止的插入|DBPROP_RETURNPENDINGINSERTS|
|資料列刪除通知|DBPROP_NOTIFYROWDELETE|
|資料列第一次變更通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|資料列插入通知|DBPROP_NOTIFYROWINSERT|
|資料列許可權|DBPROP_ROWRESTRICT|
|資料列重新同步通知|DBPROP_NOTIFYROWRESYNCH|
|資料列執行緒模型|DBPROP_ROWTHREADMODEL|
|資料列復原變更通知|DBPROP_NOTIFYROWUNDOCHANGE|
|資料列恢復刪除通知|DBPROP_NOTIFYROWUNDODELETE|
|資料列復原插入通知|DBPROP_NOTIFYROWUNDOINSERT|
|資料列更新通知|DBPROP_NOTIFYROWUPDATE|
|資料列集提取位置變更通知|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|資料列集發行通知|DBPROP_NOTIFYROWSETRELEASE|
|向後滾動|DBPROP_CANSCROLLBACKWARDS|
|插入時的伺服器資料|DBPROP_SERVERDATAONINSERT|
|略過已刪除的書簽|DBPROP_BOOKMARKSKIP|
|強式資料列識別|DBPROP_STRONGIDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用書簽|DBPROP_BOOKMARKS|

 如需有關 Microsoft Jet 之 OLE DB 提供者的特定執行詳細資料和功能資訊，請參閱 OLE DB 檔中的[Jet 提供者](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx)。
