---
title: Microsoft OLE DB Provider for Microsoft Jet |Microsoft 文件
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
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0046abe221607ff85b237c1b15ad331ba09c4e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Microsoft OLE DB Provider for Microsoft Jet 概觀
Microsoft Jet OLE DB 提供者可讓 ADO 可以存取 Microsoft Jet 資料庫。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到此提供者，設定*提供者*引數的[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性如下：

```
Microsoft.Jet.OLEDB.4.0
```

 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性也會傳回這個字串。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串是：

```
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 字串，包含這些關鍵字：

|關鍵字|Description|
|-------------|-----------------|
|**提供者**|指定 Microsoft Jet OLE DB 提供者。|
|**資料來源**|指定資料庫的路徑和檔案名稱 (例如， `c:\Northwind.mdb`)。|
|**使用者識別碼**|指定使用者名稱。 如果未指定此關鍵字，字串"`admin`」，依預設會使用。|
|**密碼**|指定的使用者密碼。 如果未指定此關鍵字，則為空字串 ("")，預設會使用。|

> [!NOTE]
>  如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是使用者識別碼和密碼連接字串中的資訊。

## <a name="provider-specific-connection-parameters"></a>提供者特有的連接參數
 Microsoft Jet OLE DB 提供者支援數個提供者專屬除了 ADO 所定義的動態屬性。 如同所有其他**連接**參數，您可以設定使用**屬性**集合**連接**物件或連接字串的一部分。

 下表列出這些屬性以及括號中相對應的 OLE DB 屬性名稱。

|매개 변수|Description|
|---------------|-----------------|
|Jet OLEDB:Compact 回收的空間量 (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|表示估計量的空間，以位元組為單位，可以回收壓縮資料庫。 建立資料庫連接之後，這個值才有效。|
|Jet OLEDB:Connection 控制項 (DBPROP_JETOLEDB_CONNECTIONCONTROL)|指出使用者是否可以連線到資料庫。|
|Jet OLEDB： 建立系統資料庫 (DBPROP_JETOLEDB_CREATESYSTEMDATABASE)|指出建立新的資料來源時，是否應該建立系統資料庫。|
|Jet OLEDB:Database 鎖定模式 (DBPROP_JETOLEDB_DATABASELOCKMODE)|指出這個資料庫的鎖定模式。 開啟資料庫的第一個使用者決定資料庫在開啟時使用的模式。|
|Jet OLEDB:Database 密碼 (DBPROP_JETOLEDB_DATABASEPASSWORD)|指出資料庫密碼。|
|Jet OLEDB： 不要複製光碟 (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE) 上的地區設定|表示 Jet 是否應該壓縮的資料庫複製地區設定資訊。|
|Jet OLEDB： 加密資料庫 (DBPROP_JETOLEDB_ENCRYPTDATABASE)|指出是否應該加密已壓縮的資料庫。 如果未設定這個屬性，如果原始資料庫也已加密，將會加密已壓縮的資料庫。|
|Jet OLEDB:Engine 類型 (DBPROP_JETOLEDB_ENGINE)|表示用來存取目前的資料存放區的儲存引擎。|
|Jet OLEDB:Exclusive 非同步延遲 (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|表示時間 （毫秒），Jet 可能會延遲非同步寫入磁碟時資料庫以獨佔方式開啟的最大長度。<br /><br /> 會忽略這個屬性，除非**Jet OLEDB:Flush 交易逾時**設為 0。|
|Jet OLEDB:Flush 交易逾時 (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|表示非同步寫入快取中儲存的資料實際上寫入之前等待的時間量磁碟。 此設定會覆寫的值**Jet OLEDB： 共用非同步延遲**和**Jet OLEDB:Exclusive 非同步延遲**。|
|Jet OLEDB： 全域大量交易 (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|表示 SQL 大量交易是否已交易。|
|Jet OLEDB： 全域部分大量 Ops (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|表示用來開啟資料庫的密碼。|
|Jet OLEDB： 隱含 Commit 同步處理 (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|指出是否在內部的隱含交易中所做的變更會寫入以同步或非同步模式。|
|Jet OLEDB:Lock 延遲 (DBPROP_JETOLEDB_LOCKDELAY)|表示嘗試取得鎖定後先前嘗試失敗之前等候的毫秒數。|
|Jet OLEDB:Lock 重試 (DBPROP_JETOLEDB_LOCKRETRY)|表示嘗試存取鎖定的分頁會重複出現的次數。|
|Jet OLEDB:Max 緩衝區大小 (DBPROP_JETOLEDB_MAXBUFFERSIZE)|表示最大數量的記憶體，以 kb 為單位，Jet 之前，可以使用開始清除至磁碟的變更。|
|每個檔案 (DBPROP_JETOLEDB_MAXLOCKSPERFILE) 的 jet OLEDB:Max 鎖定|表示 Jet 可放置在資料庫的鎖定的最大數目。 預設值是 9500。|
|Jet OLEDB： 新的資料庫密碼 (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|表示要為此資料庫的新密碼。 舊密碼儲存在**Jet OLEDB:Database 密碼**。|
|Jet OLEDB:ODBC 命令逾時 (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|表示將會逾時之前從 Jet 將遠端 ODBC 查詢的毫秒數。|
|Jet OLEDB:Page 會鎖定資料表鎖定 (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|表示 Jet 嘗試升級資料表鎖定來鎖定之前，必須在交易內鎖定多少頁。 如果此值為 0，會永遠不會升級鎖定。|
|Jet OLEDB:Page 逾時 (DBPROP_JETOLEDB_PAGETIMEOUT)|表示 Jet 會檢查以查看其快取是否已過期，且資料庫檔案之前等候的毫秒數。|
|Jet OLEDB:Recycle 長時間值頁面 (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|指出是否 Jet 應該積極嘗試它們的釋出物件時，回收 BLOB 的頁面。|
|Jet OLEDB:Registry 路徑 (DBPROP_JETOLEDB_REGPATH)|表示包含值的 Jet 資料庫引擎的 Windows 登錄機碼。|
|Jet OLEDB:Reset ISAM 統計資料 (DBPROP_JETOLEDB_RESETISAMSTATS)|指出是否在結構描述**資料錄集**DBSCHEMA_JETOLEDB_ISAMSTATS 應該重設其效能計數器，傳回效能資訊之後。|
|Jet OLEDB： 共用非同步延遲 (DBPROP_JETOLEDB_SHAREDASYNCDELAY)|表示最大數量的時間，以毫秒為單位，Jet 可能會延遲非同步寫入磁碟時資料庫多使用者模式開啟。|
|Jet oledb: system Database (DBPROP_JETOLEDB_SYSDBPATH)|表示工作群組資訊檔案 （系統資料庫） 的路徑和檔案名稱。|
|Jet OLEDB:Transaction 認可模式 (DBPROP_JETOLEDB_TXNCOMMITMODE)|指出是否 Jet 會將資料寫入磁碟以同步或非同步方式認可交易時。|
|Jet OLEDB:User 認可同步處理 (DBPROP_JETOLEDB_USERCOMMITSYNC)|指出是否在交易中所做的變更會寫入以同步或非同步模式。|

## <a name="provider-specific-recordset-and-command-properties"></a>提供者特定資料錄集和命令屬性
 Jet 提供者也支援數個提供者專屬**資料錄集**和**命令**屬性。 存取這些屬性，透過設定**屬性**集合**資料錄集**或**命令**物件。 此資料表列出的 ADO 屬性名稱，以及在括號中的其對應 OLE DB 屬性名稱。

|屬性名稱|Description|
|-------------------|-----------------|
|Jet OLEDB:Bulk 交易 (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|指出是否已交易的大量 SQL 作業。 當交易，因為資源的延遲，大規模的大量作業可能會失敗。|
|Jet OLEDB:Enable Fat 資料指標 (DBPROP_JETOLEDB_ENABLEFATCURSOR)|指出是否 Jet 應該快取多個資料列擴展的遠端資料來源的資料錄集時。|
|Jet OLEDB:Fat 資料指標快取大小 (DBPROP_JETOLEDB_FATCURSORMAXROWS)|使用遠端資料存放區資料列快取時，表示要快取的資料列數目。 這個值會被忽略，除非**Jet OLEDB:Enable Fat 資料指標**為 True。|
|Jet OLEDB： 不一致 (DBPROP_JETOLEDB_INCONSISTENT)|表示查詢結果是否允許不一致的更新。|
|Jet OLEDB： 鎖定資料粒度 (DBPROP_JETOLEDB_LOCKGRANULARITY)|指出資料表是否使用資料列層級鎖定已開啟。|
|Jet OLEDB:ODBC 傳遞陳述式 (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|表示 Jet 應該傳遞中的 SQL 文字**命令**不變，與後端的物件。|
|Jet OLEDB:Partial 大量 Ops (DBPROP_JETOLEDB_BULKPARTIAL)|表示 Jet 的行為，當 SQL DML 作業會失敗。|
|透過查詢大量作業 (DBPROP_JETOLEDB_PASSTHROUGHBULKOP) 的 jet OLEDB:Pass|指出是否查詢，並不會傳回**資料錄集**會傳遞至資料來源不變。|
|透過查詢 jet OLEDB:Pass 連接字串 (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING)|表示所使用的 Jet 連接字串連接至遠端資料存放區。 這個值會被忽略，除非**Jet OLEDB:ODBC 傳遞陳述式**為 True。|
|Jet OLEDB： 儲存查詢 (DBPROP_JETOLEDB_STOREDQUERY)|指出是否應該做為預存的查詢，而不是 SQL 命令解譯命令文字。|
|Jet OLEDB： 驗證規則集 (DBPROP_JETOLEDB_VALIDATEONSET)|指出當設定資料行的資料，或在向資料庫認可變更時，是否會評估 Jet 驗證規則。|

 根據預設，Microsoft Jet OLE DB 提供者會以讀取/寫入模式開啟 Microsoft Jet 資料庫。 若要開啟 資料庫唯讀模式中，設定[模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性之 ADO**連接**物件**adModeRead**。

## <a name="command-object-usage"></a>命令物件使用方式
 指令文字中的[命令](../../../ado/reference/ado-api/command-object-ado.md)物件使用的 Microsoft Jet SQL 用語。 您可以在命令文字; 指定傳回資料列的查詢、 執行查詢和資料表名稱不過，預存程序不支援，而且不應指定。

## <a name="recordset-behavior"></a>資料錄集行為
 Microsoft Jet 資料庫引擎不支援動態資料指標。 因此，Microsoft Jet OLE DB 提供者不支援**adLockDynamic**資料指標類型。 提供者要求動態資料指標時，將會傳回索引鍵集資料指標，然後重設[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)屬性來表示的型別[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)傳回。 此外，如果更新**資料錄集**要求 (**LockType**是**Adlockreadonly**， **Adlockpessimistic**，或**Locktype**) 提供者也會傳回索引鍵集資料指標並重設**CursorType**屬性。

## <a name="dynamic-properties"></a>動態屬性
 Microsoft Jet OLE DB 提供者插入至數個動態屬性**屬性**集合未開啟[連接](../../../ado/reference/ado-api/connection-object-ado.md)，[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，和[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。

 下表是 cross-index ADO 和 OLE DB 名稱的每個動態屬性。 OLE DB 程式設計人員參考所參考的 ADO 屬性名稱的詞彙，「 描述 」。 您可以在 OLE DB 程式設計人員參考中找到這些屬性的詳細資訊。

## <a name="connection-dynamic-properties"></a>連線的動態內容
 下列屬性會新增至**屬性**集合**連接**物件。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|Active Sessions|DBPROP_ACTIVESESSIONS|
|非同步中止|DBPROP_ASYNCTXNABORT|
|非同步認可|DBPROP_ASYNCTNXCOMMIT|
|自動認可隔離等級|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|類別目錄位置|DBPROP_CATALOGLOCATION|
|目錄詞彙|DBPROP_CATALOGTERM|
|資料行定義|DBPROP_COLUMNDEFINITION|
|目前的目錄|DBPROP_CURRENTCATALOG|
|資料來源|DBPROP_INIT_DATASOURCE|
|資料來源名稱|DBPROP_DATASOURCENAME|
|資料來源物件執行緒模型|DBPROP_DSOTHREADMODEL|
|DBMS 名稱|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|支援群組|DBPROP_GROUPBY|
|異質性資料表支援|DBPROP_HETEROGENEOUSTABLES|
|識別項區分大小寫|DBPROP_IDENTIFIERCASE|
|隔離等級|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔離保留|DBPROP_SUPPORTEDTXNISORETAIN|
|地區設定識別碼|DBPROP_INIT_LCID|
|索引大小上限|DBPROP_MAXINDEXSIZE|
|資料列大小上限|DBPROP_MAXROWSIZE|
|資料列大小上限包括 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|在選取的最大資料表|DBPROP_MAXTABLESINSELECT|
|模式|DBPROP_INIT_MODE|
|多個參數集|DBPROP_MULTIPLEPARAMSETS|
|多個結果|DBPROP_MULTIPLERESULTS|
|多個儲存體物件|DBPROP_MULTIPLESTORAGEOBJECTS|
|多重資料表更新|DBPROP_MULTITABLEUPDATE|
|NULL 的定序順序|DBPROP_NULLCOLLATION|
|NULL 串連行為|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 版本|DBPROP_PROVIDEROLEDBVER|
|OLE 物件支援|DBPROP_OLEOBJECTS|
|開啟資料列集支援|DBPROP_OPENROWSETSUPPORT|
|ORDER BY 選取清單中的資料行|DBPROP_ORDERBYCOLUMNSINSELECT|
|輸出參數使用|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|傳址存取子|DBPROP_BYREFACCESSORS|
|密碼|DBPROP_AUTH_PASSWORD|
|持續性的識別碼型別|DBPROP_PERSISTENTIDTYPE|
|準備中止行為|DBPROP_PREPAREABORTBEHAVIOR|
|準備認可行為|DBPROP_PREPARECOMMITBEHAVIOR|
|程序詞彙|DBPROP_PROCEDURETERM|
|提示|DBPROP_INIT_PROMPT|
|提供者易記名稱|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|提供者版本|DBPROP_PROVIDERVER|
|唯讀資料來源|DBPROP_DATASOURCEREADONLY|
|在命令上的資料列集轉換|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|結構描述的詞彙|DBPROP_SCHEMATERM|
|結構描述的使用方式|DBPROP_SCHEMAUSAGE|
|SQL 支援|DBPROP_SQLSUPPORT|
|結構化儲存體|DBPROP_STRUCTUREDSTORAGE|
|子查詢支援|DBPROP_SUBQUERIES|
|資料表的詞彙|DBPROP_TABLETERM|
|交易的 DDL|DBPROP_SUPPORTEDTXNDDL|
|使用者識別碼|DBPROP_AUTH_USERID|
|使用者名稱|DBPROP_USERNAME|
|視窗控制代碼|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>資料錄集的動態內容
 下列屬性會新增至**屬性**集合**資料錄集**物件。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|僅能附加的資料列集|DBPROP_APPENDONLY|
|區塊存放裝置物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書籤型別|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|排序的書籤|DBPROP_ORDEREDBOOKMARKS|
|快取延後的資料行|DBPROP_CACHEDEFERRED|
|將插入的資料列的變更|DBPROP_CHANGEINSERTEDROWS|
|資料行權限|DBPROP_COLUMNRESTRICT|
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|
|可寫入的資料行|DBPROP_MAYWRITECOLUMN|
|延後的資料行|DBPROP_DEFERRED|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後擷取|DBPROP_CANFETCHBACKWARDS|
|保存資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|固定的資料列|DBPROP_IMMOBILEROWS|
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
|常值的書籤|DBPROP_LITERALBOOKMARKS|
|常值的資料列識別|DBPROP_LITERALIDENTITY|
|開啟資料列的最大值|DBPROP_MAXOPENROWS|
|暫止資料列的最大值|DBPROP_MAXPENDINGROWS|
|最大資料列|DBPROP_MAXROWS|
|記憶體使用量|DBPROP_MEMORYUSAGE|
|通知資料粒度|DBPROP_NOTIFICATIONGRANULARITY|
|告知階段|DBPROP_NOTIFICATIONPHASES|
|交易的物件|DBPROP_TRANSACTEDOBJECT|
|可見的其他變更|DBPROP_OTHERUPDATEDELETE|
|可見的其他插入|DBPROP_OTHERINSERT|
|擁有變更可見|DBPROP_OWNUPDATEDELETE|
|可見自己插入|DBPROP_OWNINSERT|
|在中止上保留|DBPROP_ABORTPRESERVE|
|認可時保留|DBPROP_COMMITPRESERVE|
|快速重新啟動|DBPROP_QUICKRESTART|
|可重新進入的事件|DBPROP_REENTRANTEVENTS|
|移除刪除的資料列|DBPROP_REMOVEDELETED|
|報告多個變更|DBPROP_REPORTMULTIPLECHANGES|
|傳回暫止插入|DBPROP_RETURNPENDINGINSERTS|
|資料列刪除通知|DBPROP_NOTIFYROWDELETE|
|資料列的第一個變更告知|DBPROP_NOTIFYROWFIRSTCHANGE|
|資料列插入告知|DBPROP_NOTIFYROWINSERT|
|資料列的權限|DBPROP_ROWRESTRICT|
|資料列重新同步處理通知|DBPROP_NOTIFYROWRESYNCH|
|執行緒模型的資料列|DBPROP_ROWTHREADMODEL|
|資料列復原變更告知|DBPROP_NOTIFYROWUNDOCHANGE|
|資料列復原刪除告知|DBPROP_NOTIFYROWUNDODELETE|
|資料列復原插入告知|DBPROP_NOTIFYROWUNDOINSERT|
|資料列更新通知|DBPROP_NOTIFYROWUPDATE|
|資料列集擷取位置變更告知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|資料列集的發行通知|DBPROP_NOTIFYROWSETRELEASE|
|向後捲動|DBPROP_CANSCROLLBACKWARDS|
|略過刪除書籤|DBPROP_BOOKMARKSKIPPED|
|強式資料列識別|DBPROP_STRONGITDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用書籤|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令的動態屬性
 下列屬性會新增至**屬性**集合**命令**物件。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|僅能附加的資料列集|DBPROP_APPENDONLY|
|區塊存放裝置物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書籤型別|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|將插入的資料列的變更|DBPROP_CHANGEINSERTEDROWS|
|資料行權限|DBPROP_COLUMNRESTRICT|
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|
|延後的資料行|DBPROP_DEFERRED|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後擷取|DBPROP_CANFETCHBACKWARDS|
|保存資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|固定的資料列|DBPROP_IMMOBILEROWS|
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
|常值的書籤|DBPROP_LITERALBOOKMARKS|
|常值的資料列識別|DBPROP_LITERALIDENTITY|
|鎖定模式|DBPROP_LOCKMODE|
|開啟資料列的最大值|DBPROP_MAXOPENROWS|
|暫止資料列的最大值|DBPROP_MAXPENDINGROWS|
|最大資料列|DBPROP_MAXROWS|
|通知資料粒度|DBPROP_NOTIFICATIONGRANULARITY|
|告知階段|DBPROP_NOTIFICATIONPHASES|
|交易的物件|DBPROP_TRANSACTEDOBJECT|
|可見的其他變更|DBPROP_OTHERUPDATEDELETE|
|可見的其他插入|DBPROP_OTHERINSERT|
|擁有變更可見|DBPROP_OWNUPDATEDELETE|
|可見自己插入|DBPROP_OWNINSERT|
|在中止上保留|DBPROP_ABORTPRESERVE|
|認可時保留|DBPROP_COMMITPRESERVE|
|快速重新啟動|DBPROP_QUICKRESTART|
|可重新進入的事件|DBPROP_REENTRANTEVENTS|
|移除刪除的資料列|DBPROP_REMOVEDELETED|
|報告多個變更|DBPROP_REPORTMULTIPLECHANGES|
|傳回暫止插入|DBPROP_RETURNPENDINGINSERTS|
|資料列刪除通知|DBPROP_NOTIFYROWDELETE|
|資料列的第一個變更告知|DBPROP_NOTIFYROWFIRSTCHANGE|
|資料列插入告知|DBPROP_NOTIFYROWINSERT|
|資料列的權限|DBPROP_ROWRESTRICT|
|資料列重新同步處理通知|DBPROP_NOTIFYROWRESYNCH|
|執行緒模型的資料列|DBPROP_ROWTHREADMODEL|
|資料列復原變更告知|DBPROP_NOTIFYROWUNDOCHANGE|
|資料列復原刪除告知|DBPROP_NOTIFYROWUNDODELETE|
|資料列復原插入告知|DBPROP_NOTIFYROWUNDOINSERT|
|資料列更新通知|DBPROP_NOTIFYROWUPDATE|
|資料列集擷取位置變更告知|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|資料列集的發行通知|DBPROP_NOTIFYROWSETRELEASE|
|向後捲動|DBPROP_CANSCROLLBACKWARDS|
|插入的伺服器資料|DBPROP_SERVERDATAONINSERT|
|略過刪除書籤|DBPROP_BOOKMARKSKIP|
|強式資料列識別|DBPROP_STRONGIDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用書籤|DBPROP_BOOKMARKS|

 特定的實作詳細資料和 Microsoft Jet OLE DB 提供者的功能資訊，請參閱[Jet 提供者](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx)OLE DB 文件中。
