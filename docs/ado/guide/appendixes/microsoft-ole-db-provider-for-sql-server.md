---
description: 適用于 SQL Server 的 Microsoft OLE DB 提供者總覽
title: 適用于 SQL Server 的 Microsoft OLE DB 提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
author: rothja
ms.author: jroth
ms.openlocfilehash: ffb627b0994afbe2b51f946e4ab7dca881e9a9a4
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806549"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>適用于 SQL Server 的 Microsoft OLE DB 提供者總覽
適用于 SQL Server、SQLOLEDB 的 Microsoft OLE DB 提供者，可讓 ADO 存取 Microsoft SQL Server。

> [!IMPORTANT]
> 適用于 SQL Server (SQLOLEDB) 的 Microsoft OLE DB 提供者仍會被取代，因此不建議用於新的開發工作。 請改為使用新的 [Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL)，其會進行更新且具備最新的伺服器功能。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到這個提供者，請將[ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)屬性的*提供者*引數設定為：

```vb
SQLOLEDB
```

 您也可以使用 [Provider](../../reference/ado-api/provider-property-ado.md) 屬性來設定或讀取這個值。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串為：

```vb
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 此字串包含下列關鍵字：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 SQL Server 的 OLE DB 提供者。|
|**資料來源** 或 **伺服器**|指定伺服器的名稱。|
|**初始目錄** 或 **資料庫**|指定伺服器上資料庫的名稱。|
|**使用者識別碼** 或 **uid**|為 SQL Server 驗證) 指定使用者名稱 (。|
|**密碼** 或 **pwd**|指定 SQL Server 驗證) 的使用者密碼 (。|

> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定 **Trusted_Connection = yes** 或 **整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。

## <a name="provider-specific-connection-parameters"></a>提供者特定的連接參數
 除了 ADO 定義的連接參數之外，提供者還支援數個提供者特定的連接參數。 如同 ADO 連接屬性，可以透過[連接](../../reference/ado-api/connection-object-ado.md)的[properties](../../reference/ado-api/properties-collection-ado.md)集合來設定這些提供者特有的屬性，或將其設定為**ConnectionString**的一部分。

|參數|描述|
|---------------|-----------------|
|Trusted_Connection|指出使用者驗證模式。 這可以設定為 **[是] 或 [** **否**]。 預設值為 [ **否**]。 如果這個屬性設定為 **[是]**，SQLOLEDB 會使用 Microsoft Windows NT 驗證模式，以授權使用者存取 **Location** 和 [Datasource](../../reference/ado-api/datasource-property-ado.md) 屬性值所指定的 SQL Server 資料庫。 如果這個屬性設定為 [ **否**]，SQLOLEDB 會使用混合模式來授權使用者存取 SQL Server 資料庫。 SQL Server 的登入和密碼都是在 [ **使用者識別碼** ] 和 [ **密碼** ] 屬性中指定。|
|目前的語言|指出 SQL Server 的語言名稱。 識別系統訊息選取與格式所使用的語言。 語言必須安裝在 SQL Server 上，否則開啟連接將會失敗。|
|網路位址|指出 **Location** 屬性所指定之 SQL Server 的網路位址。|
|Network Library|指出 (DLL) 用來與 SQL Server 通訊的網路程式庫名稱。 名稱不得包含路徑或 .dll 副檔名。 預設值是由 SQL Server 用戶端設定所提供。|
|使用準備的程式|決定 **當準備的屬性) ** (準備命令時，SQL Server 是否建立暫存預存程序。|
|自動轉譯|指出是否轉換 OEM/ANSI 字元。 這個屬性可以設定為 **True** 或 **False**。 預設值是 **True**。 如果這個屬性設定為 **True**，當多位元組字元字串取自或傳送至 SQL Server 時，SQLOLEDB 會執行 OEM/ANSI 字元轉換。 如果這個屬性設定為 **False**，SQLOLEDB 不會在多位元組字元字串資料上執行 OEM/ANSI 字元轉換。|
|Packet Size|表示網路封包大小（以位元組為單位）。 封包大小屬性值必須介於512到32767之間。 預設 SQLOLEDB 網路封包大小為4096。|
|應用程式名稱|指出用戶端應用程式名稱。|
|工作站 ID|識別工作站的字串。|

## <a name="command-object-usage"></a>命令物件使用方式
 SQLOLEDB 接受混合物 ODBC、ANSI 和 SQL Server 特定的 Transact-sql 作為有效的語法。 例如，下列 SQL 陳述式會使用 ODBC SQL 逸出序列來指定 LCASE 字串函數：

```sql
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE 會傳回字元字串，將所有大寫字元轉換為其小寫的對等項目。 ANSI SQL 字串函數 LOWER 會執行相同的作業，因此，下列 SQL 語句是相當於先前所提供 ODBC 語句的 ANSI：

```sql
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB 在指定為命令的文字時，會成功處理任一形式的語句。

## <a name="stored-procedures"></a>預存程序
 使用 SQLOLEDB 命令執行 SQL Server 預存程式時，請使用命令文字中的 ODBC 程序呼叫 escape 序列。 SQLOLEDB 接著會使用 SQL Server 的遠端程序呼叫機制來優化命令處理。 例如，下列 ODBC SQL 語句是 Transact-sql 表單上慣用的命令文字：

## <a name="odbc-sql"></a>ODBC SQL

```vb
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```sql
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>SQL Server 功能
 使用 SQL Server，ADO 可以使用 XML 進行 **命令** 輸入，並以 xml 資料流程格式取得結果，而不是在 **記錄集** 物件中取得結果。 如需詳細資訊，請參閱 [使用資料流程進行命令輸入](../data/command-streams.md) 和將 [結果集取出至資料流程](../data/retrieving-resultsets-into-streams.md)。

### <a name="accessing-sql_variant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>使用 MDAC 2.7、MDAC 2.8 或 Windows DAC 6.0 存取 SQL_variant 資料
 Microsoft SQL Server 的資料類型稱為 **SQL_variant**。 類似于 OLE DB 的 **DBTYPE_VARIANT**， **SQL_variant** 資料類型可以儲存數種不同類型的資料。 不過， **DBTYPE_VARIANT** 和 **SQL_variant**之間有幾個主要差異。 ADO 也會處理儲存為 **SQL_variant** 值的資料，其方式與處理其他資料類型的方式不同。 下列清單描述當您存取儲存在 **SQL_variant**類型資料行中 SQL Server 資料時所要考慮的問題。

-   在 MDAC 2.7、MDAC 2.8 及 Windows 資料存取元件 (Windows DAC) 6.0，SQL Server 的 OLE DB 提供者支援 **SQL_variant** 類型。 ODBC 的 OLE DB 提供者不是。

-   **Sql_variant**類型不完全符合**DBTYPE_VARIANT**資料類型。  **Sql_variant**類型支援 DBTYPE_VARIANT 不支援的一些新子類型 **，** 包括**GUID**、 **ANSI** (非 UNICODE) 字串和**BIGINT**。 使用先前所列以外的子類型將可正常運作。

-   **Sql_variant**的子類型**數值**不符合大小的**DBTYPE_DECIMAL** 。

-   多個資料類型的強制型轉會產生不相符的類型。 例如，將**GUID**的子類型的**SQL_variant**強迫為**DBTYPE_VARIANT**將會產生**safearray** (個位元組) 的子類型。 將此類型轉換回 **SQL_variant** 將會產生 **陣列** (位元組) 的新子類型。

-   包含**SQL_variant**資料的**記錄集**欄位可以是 (封送處理) 的遠端處理，或只有在**SQL_variant**包含特定子類型時才能保存。 嘗試以下列不支援的子類型進行遠端或保存資料時，將會造成執行階段錯誤 (從 Microsoft 持續性提供者 (MSPersist) 中) 不支援的轉換： **VT_VARIANT**、 **VT_RECORD**、 **VT_ILLEGAL**、 **VT_UNKNOWN**、 **VT_BSTR**和 **VT_DISPATCH。**

-   MDAC 2.7、MDAC 2.8 以及 Windows DAC 6.0 中 SQL Server 的 OLE DB 提供者都有一個稱為「 **允許原生** 變異」的動態屬性（顧名思義），可讓開發人員以原生形式存取 **SQL_variant** ，而不是 **DBTYPE_VARIANT**。 如果已設定此屬性，並使用用戶端資料指標引擎開啟 **記錄集** (**AdUseClient**) ，則 **記錄集。開啟** 的呼叫將會失敗。 如果已設定此屬性，並使用伺服器資料指標開啟 **記錄集** (**AdUseServer**) ，則 **記錄集。開啟** 呼叫會成功，但存取 **SQL_variant** 類型的資料行將會產生錯誤。

-   在使用 MDAC 2.5 的用戶端應用程式中， **SQL_variant** 資料可以搭配 Microsoft SQL Server 的查詢使用。 不過， **SQL_variant** 資料的值會被視為字串。 這類用戶端應用程式應升級為 MDAC 2.7、MDAC 2.8 或 Windows DAC 6.0。

## <a name="recordset-behavior"></a>記錄集行為
 SQLOLEDB 無法使用 SQL Server 資料指標來支援許多命令所產生的多個結果。 如果取用者要求需要 SQL Server 資料指標支援的記錄集，則如果使用的命令文字會產生一個以上的記錄集做為其結果，就會發生錯誤。

 SQL Server 資料指標支援可滾動的 SQLOLEDB 記錄集。 SQL Server 會對資料指標強加限制，而這些資料指標對資料庫的其他使用者所做的變更很敏感。 具體而言，某些資料指標中的資料列無法進行排序，且嘗試使用包含 SQL ORDER BY 子句的命令來建立記錄集可能會失敗。

## <a name="dynamic-properties"></a>動態屬性
 適用于 SQL Server 的 Microsoft OLE DB 提供者會將數個動態屬性插入未開啟之[連接](../../reference/ado-api/connection-object-ado.md)、[記錄集](../../reference/ado-api/recordset-object-ado.md)和[命令](../../reference/ado-api/command-object-ado.md)物件的**properties**集合中。

 下表是每個動態屬性之 ADO 和 OLE DB 名稱的交叉索引。 OLE DB 程式設計人員參考是依「描述」一詞來參考 ADO 屬性名稱。 您可以在 OLE DB 程式設計人員參考中找到這些屬性的詳細資訊。 在索引中搜尋 OLE DB 的屬性名稱，或參閱 [附錄 C： OLE DB 屬性](/previous-versions/windows/desktop/ms723130(v=vs.85))。

## <a name="connection-dynamic-properties"></a>連接動態屬性
 下列屬性會加入至**Connection**物件的**properties**集合中。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|Active Sessions|DBPROP_ACTIVESESSIONS|
|Asynchable 中止|DBPROP_ASYNCTXNABORT|
|Asynchable 認可|DBPROP_ASYNCTNXCOMMIT|
|自動認可隔離等級|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|目錄位置|DBPROP_CATALOGLOCATION|
|目錄詞彙|DBPROP_CATALOGTERM|
|資料行定義|DBPROP_COLUMNDEFINITION|
|連接逾時|DBPROP_INIT_TIMEOUT|
|目前的目錄|DBPROP_CURRENTCATALOG|
|資料來源|DBPROP_INIT_DATASOURCE|
|資料來源名稱|DBPROP_DATASOURCENAME|
|資料來源物件執行緒模型|DBPROP_DSOTHREADMODEL|
|DBMS 名稱|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|擴充屬性|DBPROP_INIT_PROVIDERSTRING|
|依支援分組|DBPROP_GROUPBY|
|異質資料表支援|DBPROP_HETEROGENEOUSTABLES|
|識別碼區分大小寫|DBPROP_IDENTIFIERCASE|
|初始目錄|DBPROP_INIT_CATALOG|
|隔離等級|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔離保留|DBPROP_SUPPORTEDTXNISORETAIN|
|地區設定識別碼|DBPROP_INIT_LCID|
|索引大小上限|DBPROP_MAXINDEXSIZE|
|最大資料列大小|DBPROP_MAXROWSIZE|
|最大資料列大小包括 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT 中的資料表上限|DBPROP_MAXTABLESINSELECT|
|多個參數集|DBPROP_MULTIPLEPARAMSETS|
|多個結果|DBPROP_MULTIPLERESULTS|
|多個儲存物件|DBPROP_MULTIPLESTORAGEOBJECTS|
|多資料表更新|DBPROP_MULTITABLEUPDATE|
|Null 定序順序|DBPROP_NullCOLLATION|
|Null 串連行為|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 版本|DBPROP_PROVIDEROLEDBVER|
|OLE 物件支援|DBPROP_OLEOBJECTS|
|開啟資料列集支援|DBPROP_OPENROWSETSUPPORT|
|選取清單中的 ORDER BY 資料行|DBPROP_ORDERBYCOLUMNSINSELECT|
|輸出參數可用性|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|以 Ref 存取子傳遞|DBPROP_BYREFACCESSORS|
|密碼|DBPROP_AUTH_PASSWORD|
|保存安全性資訊|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
|持續性識別碼類型|DBPROP_PERSISTENTIDTYPE|
|準備中止行為|DBPROP_PREPAREABORTBEHAVIOR|
|準備認可行為|DBPROP_PREPARECOMMITBEHAVIOR|
|程式期限|DBPROP_PROCEDURETERM|
|Prompt|DBPROP_INIT_PROMPT|
|提供者易記名稱|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|提供者版本|DBPROP_PROVIDERVER|
|唯讀資料來源|DBPROP_DATASOURCEREADONLY|
|命令的資料列集轉換|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|架構詞彙|DBPROP_SCHEMATERM|
|架構使用方式|DBPROP_SCHEMAUSAGE|
|SQL 支援|DBPROP_SQLSUPPORT|
|結構化儲存體|DBPROP_STRUCTUREDSTORAGE|
|子查詢支援|DBPROP_SUBQUERIES|
|資料表詞彙|DBPROP_TABLETERM|
|交易 DDL|DBPROP_SUPPORTEDTXNDDL|
|使用者識別碼|DBPROP_AUTH_USERID|
|使用者名稱|DBPROP_USERNAME|
|視窗控制代碼|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>記錄集動態屬性
 下列屬性會加入至**記錄集**物件的**properties**集合中。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|封鎖儲存物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書簽類型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|變更插入的資料列|DBPROP_CHANGEINSERTEDROWS|
|資料行許可權|DBPROP_COLUMNRESTRICT|
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|
|命令逾時|DBPROP_COMMANDTIMEOUT|
|延遲資料行|DBPROP_DEFERRED|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後提取|DBPROP_CANFETCHBACKWARDS|
|保留資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Immobile 資料列|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|常值書簽|DBPROP_LITERALBOOKMARKS|
|常值資料列識別|DBPROP_LITERALIDENTITY|
|開啟的資料列數上限|DBPROP_MAXOPENROWS|
|暫止的資料列數上限|DBPROP_MAXPENDINGROWS|
|最大資料列數|DBPROP_MAXROWS|
|通知細微性|DBPROP_NOTIFICATIONGRANULARITY|
|通知階段|DBPROP_NOTIFICATIONPHASES|
|物件交易|DBPROP_TRANSACTEDOBJECT|
|他人的變更可見|DBPROP_OTHERUPDATEDELETE|
|其他人的插入可見|DBPROP_OTHERINSERT|
|可見的變更|DBPROP_OWNUPDATEDELETE|
|擁有可見的插入|DBPROP_OWNINSERT|
|中止時保留|DBPROP_ABORTPRESERVE|
|在認可時保留|DBPROP_COMMITPRESERVE|
|快速重新開機|DBPROP_QUICKRESTART|
|重新進入事件|DBPROP_REENTRANTEVENTS|
|移除刪除的資料列|DBPROP_REMOVEDELETED|
|報告多項變更|DBPROP_REPORTMULTIPLECHANGES|
|傳回暫止的插入|DBPROP_RETURNPENDINGINSERTS|
|資料列刪除通知|DBPROP_NOTIFYROWDELETE|
|Row First 變更通知|DBPROP_NOTIFYROWFIRSTCHANGE|
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
|伺服器資料指標|DBPROP_SERVERCURSOR|
|略過已刪除的書簽|DBPROP_BOOKMARKSKIPPED|
|強式資料列識別|DBPROP_STRONGITDENTITY|
|唯一資料列|DBPROP_UNIQUEROWS|
|更新|DBPROP_UPDATABILITY|
|使用書簽|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令動態屬性
 下列屬性會新增至**Command**物件的**properties**集合中。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|基底路徑|SSPROP_STREAM_BASEPATH|
|封鎖儲存物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書簽類型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|變更插入的資料列|DBPROP_CHANGEINSERTEDROWS|
|資料行許可權|DBPROP_COLUMNRESTRICT|
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|
|內容類型|SSPROP_STREAM_CONTENTTYPE|
|資料指標自動提取|SSPROP_CURSORAUTOFETCH|
|延遲資料行|DBPROP_DEFERRED|
|延遲準備|SSPROP_DEFERPREPARE|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後提取|DBPROP_CANFETCHBACKWARDS|
|保留資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Immobile 資料列|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch|DBPROP_IRowsetResynch|
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|常值書簽|DBPROP_LITERALBOOKMARKS|
|常值資料列識別|DBPROP_LITERALIDENTITY|
|鎖定模式|DBPROP_LOCKMODE|
|開啟的資料列數上限|DBPROP_MAXOPENROWS|
|暫止的資料列數上限|DBPROP_MAXPENDINGROWS|
|最大資料列數|DBPROP_MAXROWS|
|通知細微性|DBPROP_NOTIFICATIONGRANULARITY|
|通知階段|DBPROP_NOTIFICATIONPHASES|
|物件交易|DBPROP_TRANSACTEDOBJECT|
|他人的變更可見|DBPROP_OTHERUPDATEDELETE|
|其他人的插入可見|DBPROP_OTHERINSERT|
|輸出編碼屬性|DBPROP_OUTPUTENCODING|
|輸出資料流程屬性|DBPROP_OUTPUTSTREAM|
|可見的變更|DBPROP_OWNUPDATEDELETE|
|擁有可見的插入|DBPROP_OWNINSERT|
|中止時保留|DBPROP_ABORTPRESERVE|
|在認可時保留|DBPROP_COMMITPRESERVE|
|快速重新開機|DBPROP_QUICKRESTART|
|重新進入事件|DBPROP_REENTRANTEVENTS|
|移除刪除的資料列|DBPROP_REMOVEDELETED|
|報告多項變更|DBPROP_REPORTMULTIPLECHANGES|
|傳回暫止的插入|DBPROP_RETURNPENDINGINSERTS|
|資料列刪除通知|DBPROP_NOTIFYROWDELETE|
|Row First 變更通知|DBPROP_NOTIFYROWFIRSTCHANGE|
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
|伺服器資料指標|DBPROP_SERVERCURSOR|
|插入時的伺服器資料|DBPROP_SERVERDATAONINSERT|
|略過已刪除的書簽|DBPROP_BOOKMARKSKIP|
|強式資料列識別|DBPROP_STRONGIDENTITY|
|更新|DBPROP_UPDATABILITY|
|使用書簽|DBPROP_BOOKMARKS|
|XML 根目錄|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 如需有關 Microsoft SQL Server OLE DB 提供者的特定執行詳細資料和功能資訊，請參閱 [SQL Server 提供者](/previous-versions/windows/desktop/ms720897(v=vs.85))。

## <a name="see-also"></a>另請參閱
 [ConnectionString 屬性 (ado) ](../../reference/ado-api/connectionstring-property-ado.md) [Provider 屬性 (ado) ](../../reference/ado-api/provider-property-ado.md) [記錄集物件 (ado) ](../../reference/ado-api/recordset-object-ado.md)