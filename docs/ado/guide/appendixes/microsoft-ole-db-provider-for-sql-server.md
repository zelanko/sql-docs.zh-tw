---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bd28ece0e82c4551409920c876d54fbd7dc501ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926619"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>適用于 SQL Server 的 Microsoft OLE DB 提供者總覽
適用于 SQL Server，SQLOLEDB 的 Microsoft OLE DB 提供者可讓 ADO 存取 Microsoft SQL Server。

> [!IMPORTANT]
> Microsoft OLE DB Provider for SQL Server （SQLOLEDB）仍保持淘汰，不建議將它用於新的開發工作。 請改為使用新的 [Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL)，其會進行更新且具備最新的伺服器功能。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到這個提供者，請將*提供者*引數設定為[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性，以執行下列動作：

```vb
SQLOLEDB
```

 這個值也可以使用[Provider](../../../ado/reference/ado-api/provider-property-ado.md)屬性來設定或讀取。

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
|**資料來源**或**伺服器**|指定伺服器的名稱。|
|**初始目錄**或**資料庫**|指定伺服器上的資料庫名稱。|
|**使用者識別碼**或**uid**|指定使用者名稱（用於 SQL Server 驗證）。|
|**Password**或**pwd**|指定使用者密碼（用於 SQL Server 驗證）。|

> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定**Trusted_Connection = yes**或**整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。

## <a name="provider-specific-connection-parameters"></a>提供者特定的連接參數
 除了 ADO 所定義的連接參數之外，提供者也支援數個提供者特定的連線參數。 如同 ADO 連接屬性，這些提供者專屬的屬性可以透過[連接](../../../ado/reference/ado-api/connection-object-ado.md)的[properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合來設定，也可以設定為**ConnectionString**的一部分。

|參數|說明|
|---------------|-----------------|
|Trusted_Connection|表示使用者驗證模式。 這可以設定為 **[是] 或 [** **否**]。 預設值為 [**否**]。 如果此屬性設定為 **[是]**，SQLOLEDB 會使用 MICROSOFT Windows NT 驗證模式來授權使用者存取**Location**和[Datasource](../../../ado/reference/ado-api/datasource-property-ado.md)屬性值所指定的 SQL Server 資料庫。 如果此屬性設定為 [**否**]，SQLOLEDB 會使用混合模式來授權使用者存取 SQL Server 資料庫。 [**使用者識別碼**] 和 [**密碼**] 屬性中指定了 SQL Server 登入和密碼。|
|目前的語言|表示 SQL Server 的語言名稱。 識別系統訊息選取與格式所使用的語言。 語言必須安裝在 SQL Server 上，否則開啟連接將會失敗。|
|網路位址|指出**Location**屬性所指定 SQL Server 的網路位址。|
|Network Library|指出用來與 SQL Server 通訊的網路程式庫（DLL）的名稱。 名稱不得包含路徑或 .dll 副檔名。 預設值是由 SQL Server 用戶端設定所提供。|
|使用準備程式|決定當準備命令時，SQL Server 是否會建立暫存預存程序（由**備**妥的屬性）。|
|自動轉譯|指出是否轉換 OEM/ANSI 字元。 這個屬性可以設定為**True**或**False**。 預設值是 **True**。 如果此屬性設定為**True**，則 SQLOLEDB 會在從 SQL Server 抓取多位元組字元字串或將其傳送至時，執行 OEM/ANSI 字元轉換。 如果此屬性設定為**False**，SQLOLEDB 不會在多位元組字元字串資料上執行 OEM/ANSI 字元轉換。|
|Packet Size|表示網路封包大小（以位元組為單位）。 封包大小屬性值必須介於512和32767之間。 預設的 SQLOLEDB 網路封包大小為4096。|
|應用程式名稱|表示用戶端應用程式名稱。|
|工作站 ID|識別工作站的字串。|

## <a name="command-object-usage"></a>命令物件使用方式
 SQLOLEDB 接受 ODBC、ANSI 和 SQL Server 特定 Transact-sql 的混合物，做為有效的語法。 例如，下列 SQL 陳述式會使用 ODBC SQL 逸出序列來指定 LCASE 字串函數：

```sql
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE 會傳回字元字串，將所有大寫字元轉換為其小寫的對等項目。 ANSI SQL 字串函數 LOWER 會執行相同的作業，因此下列 SQL 語句相當於稍早所提供的 ODBC 語句：

```sql
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB 在指定為命令的文字時，已成功處理任一形式的語句。

## <a name="stored-procedures"></a>預存程序
 使用 SQLOLEDB 命令執行 SQL Server 預存程式時，請使用命令文字中的 ODBC 程序呼叫 escape 順序。 然後 SQLOLEDB 會使用 SQL Server 的遠端程序呼叫機制來優化命令處理。 例如，下列 ODBC SQL 語句是 Transact-sql 形式上慣用的命令文字：

## <a name="odbc-sql"></a>ODBC SQL

```vb
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```sql
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>SQL Server 功能
 使用 SQL Server，ADO 可以使用 XML 進行**命令**輸入，並以 xml 資料流程格式（而不是在**記錄集**物件中）取得結果。 如需詳細資訊，請參閱[使用資料流程進行命令輸入](../../../ado/guide/data/command-streams.md)和將[結果集取出至資料流程](../../../ado/guide/data/retrieving-resultsets-into-streams.md)。

### <a name="accessing-sql_variant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>使用 MDAC 2.7、MDAC 2.8 或 Windows DAC 6.0 存取 SQL_variant 資料
 Microsoft SQL Server 具有稱為**SQL_variant**的資料類型。 類似于 OLE DB 的**DBTYPE_VARIANT**， **SQL_variant**資料類型可以儲存數個不同類型的資料。 不過， **DBTYPE_VARIANT**和**SQL_variant**之間有幾個主要差異。 ADO 也會處理儲存為**SQL_variant**值的資料，其方式與處理其他資料類型的方式不同。 下列清單描述當您存取儲存在**SQL_variant**類型之資料行中 SQL Server 資料時，所要考慮的問題。

-   在 MDAC 2.7、MDAC 2.8 和 Windows Data Access Components （Windows DAC）6.0 中，SQL Server 的 OLE DB 提供者支援**SQL_variant**類型。 ODBC 的 OLE DB 提供者不是。

-   **Sql_variant**類型不完全符合**DBTYPE_VARIANT**資料類型。  **Sql_variant**類型支援 DBTYPE_VARIANT 不支援的一些新子類型 **，** 包括**GUID**、 **ANSI** （非 UNICODE）字串和**BIGINT**。 使用先前所列以外的子類型將可正確運作。

-   **Sql_variant**的子類型**數值**不符合大小的**DBTYPE_DECIMAL** 。

-   多個資料類型強制型轉會導致類型不相符。 例如，將**GUID**的子類型的**SQL_variant**強迫為**DBTYPE_VARIANT**會產生**safearray**的子類型（位元組）。 將此類型轉換回**SQL_variant**將會產生**陣列**的新子類型（位元組）。

-   包含**SQL_variant**資料的**記錄集**欄位可以是 [遠端（封送處理）] 或 [只有在**SQL_variant**包含特定的子類型時才會保存。 嘗試使用下列不支援的子類型來遠端或保存資料，將會導致來自 Microsoft 持續性提供者（MSPersist）的執行階段錯誤（不支援的轉換）： **VT_VARIANT**、 **VT_RECORD**、 **VT_ILLEGAL**、 **VT_UNKNOWN**、 **VT_BSTR**和**VT_DISPATCH。**

-   MDAC 2.7、MDAC 2.8 和 Windows DAC 6.0 中 SQL Server 的 OLE DB 提供者有一個稱為「**允許原生變數**」的動態屬性，如其名，可讓開發人員以其原生格式存取**SQL_variant** ，而不是**DBTYPE_VARIANT**。 如果已設定此屬性，而且**記錄集**是以用戶端資料指標引擎（**adUseClient**）開啟，則**記錄集。開啟**呼叫將會失敗。 如果已設定此屬性，且**記錄集**是以伺服器資料指標（**adUseServer**）開啟，則**記錄集。開啟**呼叫將會成功，但存取類型**SQL_variant**的資料行將會產生錯誤。

-   在使用 MDAC 2.5 的用戶端應用程式中， **SQL_variant**資料可以與 Microsoft SQL Server 的查詢搭配使用。 不過， **SQL_variant**資料的值會被視為字串。 這類用戶端應用程式應該升級為 MDAC 2.7、MDAC 2.8 或 Windows DAC 6.0。

## <a name="recordset-behavior"></a>記錄集行為
 SQLOLEDB 無法使用 SQL Server 的資料指標來支援許多命令所產生的多重結果。 如果取用者要求需要 SQL Server 資料指標支援的記錄集，而使用的命令文字產生的一個以上的記錄集做為其結果，就會發生錯誤。

 SQL Server 資料指標支援可滾動的 SQLOLEDB 記錄集。 SQL Server 會對資料指標施加限制，這對於資料庫的其他使用者所做的變更很敏感。 具體而言，某些資料指標中的資料列無法排序，而且嘗試使用包含 SQL ORDER BY 子句的命令來建立記錄集可能會失敗。

## <a name="dynamic-properties"></a>動態屬性
 適用于 SQL Server 的 Microsoft OLE DB 提供者會在未[連接](../../../ado/reference/ado-api/connection-object-ado.md)的連線、[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)和[命令](../../../ado/reference/ado-api/command-object-ado.md)物件的**properties**集合中插入數個動態屬性。

 下表是每個動態屬性的 ADO 和 OLE DB 名稱的交互索引。 OLE DB 程式設計人員參考以「描述」一詞指的是 ADO 屬性名稱。 您可以在 OLE DB 程式設計人員參考中找到這些屬性的詳細資訊。 搜尋索引中的 OLE DB 屬性名稱，或參閱[附錄 C： OLE DB 屬性](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)。

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
|連接逾時|DBPROP_INIT_TIMEOUT|
|目前的目錄|DBPROP_CURRENTCATALOG|
|資料來源|DBPROP_INIT_DATASOURCE|
|資料來源名稱|DBPROP_DATASOURCENAME|
|資料來源物件執行緒模型|DBPROP_DSOTHREADMODEL|
|DBMS 名稱|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|擴充屬性|DBPROP_INIT_PROVIDERSTRING|
|群組依據支援|DBPROP_GROUPBY|
|異質資料表支援|DBPROP_HETEROGENEOUSTABLES|
|識別碼區分大小寫|DBPROP_IDENTIFIERCASE|
|初始目錄|DBPROP_INIT_CATALOG|
|隔離等級|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔離保留|DBPROP_SUPPORTEDTXNISORETAIN|
|地區設定識別碼|DBPROP_INIT_LCID|
|索引大小上限|DBPROP_MAXINDEXSIZE|
|最大資料列大小|DBPROP_MAXROWSIZE|
|最大資料列大小包含 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT 中的資料表上限|DBPROP_MAXTABLESINSELECT|
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
|保存安全性資訊|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
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
|固定資料列|DBPROP_IMMOBILEROWS|
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
|資料列集提取位置變更通知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|資料列集發行通知|DBPROP_NOTIFYROWSETRELEASE|
|向後滾動|DBPROP_CANSCROLLBACKWARDS|
|伺服器資料指標|DBPROP_SERVERCURSOR|
|略過已刪除的書簽|DBPROP_BOOKMARKSKIPPED|
|強式資料列識別|DBPROP_STRONGITDENTITY|
|唯一資料列|DBPROP_UNIQUEROWS|
|可更新性|DBPROP_UPDATABILITY|
|使用書簽|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令動態屬性
 下列屬性會加入至**Command**物件的**properties**集合中。

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
|固定資料列|DBPROP_IMMOBILEROWS|
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
|最大開啟資料列|DBPROP_MAXOPENROWS|
|暫止資料列數上限|DBPROP_MAXPENDINGROWS|
|最大資料列數|DBPROP_MAXROWS|
|通知資料細微性|DBPROP_NOTIFICATIONGRANULARITY|
|通知階段|DBPROP_NOTIFICATIONPHASES|
|物件交易|DBPROP_TRANSACTEDOBJECT|
|其他變更可見|DBPROP_OTHERUPDATEDELETE|
|其他的插入可見|DBPROP_OTHERINSERT|
|輸出編碼屬性|DBPROP_OUTPUTENCODING|
|輸出資料流程屬性|DBPROP_OUTPUTSTREAM|
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
|伺服器資料指標|DBPROP_SERVERCURSOR|
|插入時的伺服器資料|DBPROP_SERVERDATAONINSERT|
|略過已刪除的書簽|DBPROP_BOOKMARKSKIP|
|強式資料列識別|DBPROP_STRONGIDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用書簽|DBPROP_BOOKMARKS|
|XML 根|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 如需有關 Microsoft SQL Server OLE DB 提供者的特定執行詳細資料和功能資訊，請參閱[SQL Server 提供者](https://msdn.microsoft.com/adf1d6c4-5930-444a-9248-ff1979729635)。

## <a name="see-also"></a>另請參閱
 [ConnectionString 屬性（ado）](../../../ado/reference/ado-api/connectionstring-property-ado.md) [提供者屬性（Ado）](../../../ado/reference/ado-api/provider-property-ado.md) [Recordset 物件（ado）](../../../ado/reference/ado-api/recordset-object-ado.md)
