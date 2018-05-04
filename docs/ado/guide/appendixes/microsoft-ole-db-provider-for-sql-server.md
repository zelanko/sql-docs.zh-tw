---
title: Microsoft OLE DB Provider for SQL Server |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4002e1a8e0975d730d8947b452140665b6778f84
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>Microsoft OLE DB Provider for SQL Server 概觀
Microsoft OLE DB Provider for SQL Server，SQLOLEDB，可讓 ADO 存取 Microsoft SQL Server。

**注意：**不建議使用這個驅動程式，開發新項目。 新的 OLE DB 提供者會呼叫[Microsoft OLE DB 驅動程式的 SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) 這會更新為最新的伺服器功能從現在開始。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到此提供者，設定*提供者*引數[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性：

```
SQLOLEDB
```

 這個值也可以設定或讀取使用[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串是：

```
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 字串，包含這些關鍵字：

|關鍵字|Description|
|-------------|-----------------|
|**提供者**|指定 SQL Server 的 OLE DB 提供者。|
|**資料來源**或**伺服器**|指定伺服器的名稱。|
|**初始目錄**或**資料庫**|在伺服器上，指定資料庫的名稱。|
|**使用者識別碼**或**uid**|指定的使用者名稱 （適用於 SQL Server 驗證）。|
|**密碼**或**pwd**|指定的使用者密碼 （適用於 SQL Server 驗證）。|

> [!NOTE]
>  如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是使用者識別碼和密碼連接字串中的資訊。

## <a name="provider-specific-connection-parameters"></a>提供者特有的連接參數
 提供者支援數個提供者特有的連接參數，除了由 ADO 所定義。 使用 ADO 連接屬性，這些提供者特有的屬性可以設定透過[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合[連接](../../../ado/reference/ado-api/connection-object-ado.md)或可設定的一部分**ConnectionString**.

|매개 변수|Description|
|---------------|-----------------|
|Trusted_Connection|表示使用者驗證模式。 這可以設定為**是**或**否**。 預設值是 **否**。 如果這個屬性設定為**是**，SQLOLEDB 會使用 Microsoft Windows NT 驗證模式來授權使用者存取所指定的 SQL Server 資料庫**位置**和[資料來源](../../../ado/reference/ado-api/datasource-property-ado.md)屬性值。 如果這個屬性設定為**否**，SQLOLEDB 會使用混合模式來授權使用者存取 SQL Server 資料庫。 SQL Server 登入和密碼在指定**使用者識別碼**和**密碼**屬性。|
|目前的語言|表示 SQL Server 語言名稱。 識別系統訊息選取與格式所使用的語言。 語言必須安裝在 SQL Server 中的其他方式開啟連接將會失敗。|
|網路位址|指出所指定的 SQL 伺服器的網路位址**位置**屬性。|
|網路程式庫|表示用來與 SQL Server 通訊的網路程式庫 (DLL) 名稱。 名稱不得包含路徑或 .dll 副檔名。 預設值是由 SQL Server 用戶端設定中提供。|
|使用準備程序|決定 SQL Server 是否會在準備命令時建立暫存預存程序 (由**已準備**屬性)。|
|自動轉譯|指出是否要轉換的 OEM/ANSI 字元。 這個屬性可以設定為**True**或**False**。 預設值為 **True**。 如果這個屬性設定為**True**，SQLOLEDB 會多位元組字元字串是擷取自或傳送到 SQL Server 時，執行 OEM/ANSI 字元轉換。 如果這個屬性設定為**False**，SQLOLEDB 不會執行多位元組字元字串資料 OEM/ANSI 字元轉換。|
|Packet Size|指出網路封包大小 （位元組）。 封包大小屬性值必須是介於 512 和 32767 之間。 預設 SQLOLEDB 網路封包大小為 4096。|
|Application Name|表示用戶端應用程式名稱。|
|工作站 ID|識別工作站的字串。|

## <a name="command-object-usage"></a>命令物件使用方式
 SQLOLEDB 會接受 ODBC、 ANSI 和 SQL Server 特有的 TRANSACT-SQL 的混合物為有效的語法。 例如，下列 SQL 陳述式會使用 ODBC SQL 逸出序列來指定 LCASE 字串函數：

```
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE 會傳回字元字串，將所有大寫字元轉換為其小寫的對等項目。 ANSI SQL 字串函數 LOWER 執行相同的作業，因此下列 SQL 陳述式是 ANSI 相當於先前呈現的 ODBC 陳述式：

```
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB 成功處理任一種陳述式時指定為命令的文字形式。

## <a name="stored-procedures"></a>預存程序
 當執行 SQL Server 預存程序中使用的 SQLOLEDB 命令時，使用 ODBC 程序呼叫逸出序列中的命令文字。 SQLOLEDB 然後會使用 SQL Server 的遠端程序呼叫機制來最佳化命令處理。 例如，下列 ODBC SQL 陳述式是慣用的命令文字的 TRANSACT-SQL 表單上：

## <a name="odbc-sql"></a>ODBC SQL

```
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>SQL Server 功能
 SQL Server，ADO 可以使用 XML for**命令**輸入和擷取結果，而不是在 XML 資料流格式**資料錄集**物件。 如需詳細資訊，請參閱[使用命令的輸入資料流](../../../ado/guide/data/command-streams.md)和[成資料流擷取結果集](../../../ado/guide/data/retrieving-resultsets-into-streams.md)。

### <a name="accessing-sqlvariant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>存取使用 MDAC 2.7、 MDAC 2.8 或 Windows DAC 6.0 的 sql_variant 資料
 Microsoft SQL Server 具有資料類型，稱為**sql_variant**。 類似於 OLE DB 的**DBTYPE_VARIANT**、 **sql_variant**資料類型可以儲存多種不同類型的資料。 不過，有幾個主要的差異之間**DBTYPE_VARIANT**和**sql_variant**。 ADO 也會處理資料儲存為**sql_variant**值不同於其他資料型別的處理方式。 下列清單將描述 SQL Server 資料類型的資料行中儲存的存取時應該考量的問題**sql_variant**。

-   MDAC 2.7、 MDAC 2.8 和 Windows Data Access Components (Windows DAC) 6.0，OLE DB Provider for SQL Server 支援**sql_variant**型別。 OLE DB Provider for ODBC 則否。

-   **Sql_variant**型別沒有完全符合**DBTYPE_VARIANT**資料型別。  **Sql_variant**型別支援幾個新的子類型不支援**DBTYPE_VARIANT、**包括**GUID**， **ANSI** (非 UNICODE)字串，並**BIGINT**。 除了使用子類型稍早所列的正常運作。

-   **Sql_variant**子型別**數值**不符**DBTYPE_DECIMAL**的大小。

-   不相符的型別會造成多個資料類型強制型轉。 比方說，強制型轉**sql_variant**的子類型與**GUID**至**DBTYPE_VARIANT**的子類型會導致**safearray**（位元組）. 此型別轉換回**sql_variant**會導致新的子類型**陣列**（位元組）。

-   **資料錄集**包含的欄位**sql_variant**資料可以進行遠端通訊 （封送處理） 或持續性的才**sql_variant**包含特定的子類型。 嘗試遠端或保存資料與不支援下列子型別會造成執行階段錯誤 （不支援轉換），從 Microsoft 持續性提供者 (MSPersist): **VT_VARIANT**， **VT_RECORD**， **VT_ILLEGAL**， **VT_UNKNOWN**， **VT_BSTR**，和**VT_DISPATCH。**

-   MDAC 2.7、 MDAC 2.8 和 Windows DAC 6.0 中的 SQL Server OLE DB 提供者具有動態名**允許原生變異**，正如其名，可讓開發人員存取**sql_variant**中與原生形式**DBTYPE_VARIANT**。 如果這個屬性設定，以及**資料錄集**開啟與用戶端游標引擎 (**adUseClient**)、 **Recordset.Open**呼叫將會失敗。 如果這個屬性設定，且**資料錄集**開啟伺服器資料指標 (**adUseServer**)、 **Recordset.Open**呼叫將會成功，但存取類型的資料行**sql_variant**都會產生錯誤。

-   在用戶端應用程式中使用 MDAC 2.5 **sql_variant**資料可以搭配 Microsoft SQL Server 查詢。 不過，值**sql_variant**資料會視為字串。 這類用戶端應用程式應該要升級到 MDAC 2.7、 MDAC 2.8 或 Windows DAC 6.0。

## <a name="recordset-behavior"></a>資料錄集行為
 SQLOLEDB 無法使用 SQL Server 資料指標來支援許多命令所產生多個結果。 如果取用者要求需要 SQL Server 資料指標支援資料錄集時，如果所使用的命令文字產生多個單一資料錄集做為其結果，也會發生錯誤。

 SQL Server 資料指標支援可捲動的 SQLOLEDB 資料錄集。 SQL Server 來加上其他使用者的資料庫所做的變更影響的資料指標的限制。 具體來說，某些資料指標中的資料列無法進行排序，而且嘗試建立使用命令，其中包含 SQL ORDER BY 子句的資料錄集可能會失敗。

## <a name="dynamic-properties"></a>動態屬性
 Microsoft OLE DB Provider for SQL Server 會插入至數個動態屬性**屬性**集合未開啟[連接](../../../ado/reference/ado-api/connection-object-ado.md)，[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，和[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。

 下表是 cross-index ADO 和 OLE DB 名稱的每個動態屬性。 OLE DB 程式設計人員參考所參考的 ADO 屬性名稱的詞彙 「 描述 」。 您可以在 OLE DB 程式設計人員參考中找到這些屬性的詳細資訊。 搜尋索引中的 OLE DB 屬性名稱，或參閱[附錄 c: OLE DB 屬性](http://msdn.microsoft.com/en-us/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)。

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
|連接逾時|DBPROP_INIT_TIMEOUT|
|目前的目錄|DBPROP_CURRENTCATALOG|
|資料來源|DBPROP_INIT_DATASOURCE|
|資料來源名稱|DBPROP_DATASOURCENAME|
|資料來源物件執行緒模型|DBPROP_DSOTHREADMODEL|
|DBMS 名稱|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|擴充屬性|DBPROP_INIT_PROVIDERSTRING|
|支援群組|DBPROP_GROUPBY|
|異質性資料表支援|DBPROP_HETEROGENEOUSTABLES|
|識別項區分大小寫|DBPROP_IDENTIFIERCASE|
|初始目錄|DBPROP_INIT_CATALOG|
|隔離等級|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔離保留|DBPROP_SUPPORTEDTXNISORETAIN|
|地區設定識別碼|DBPROP_INIT_LCID|
|索引大小上限|DBPROP_MAXINDEXSIZE|
|資料列大小上限|DBPROP_MAXROWSIZE|
|資料列大小上限包括 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|在選取的最大資料表|DBPROP_MAXTABLESINSELECT|
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
|保存安全性資訊|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
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
|區塊存放裝置物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書籤型別|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|將插入的資料列的變更|DBPROP_CHANGEINSERTEDROWS|
|資料行權限|DBPROP_COLUMNRESTRICT|
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|
|命令逾時|DBPROP_COMMANDTIMEOUT|
|延後的資料行|DBPROP_DEFERRED|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後擷取|DBPROP_CANFETCHBACKWARDS|
|保存資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|固定的資料列|DBPROP_IMMOBILEROWS|
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
|常值的書籤|DBPROP_LITERALBOOKMARKS|
|常值的資料列識別|DBPROP_LITERALIDENTITY|
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
|資料列集擷取位置變更告知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|資料列集的發行通知|DBPROP_NOTIFYROWSETRELEASE|
|向後捲動|DBPROP_CANSCROLLBACKWARDS|
|伺服器資料指標|DBPROP_SERVERCURSOR|
|略過刪除書籤|DBPROP_BOOKMARKSKIPPED|
|強式資料列識別|DBPROP_STRONGITDENTITY|
|唯一的資料列|DBPROP_UNIQUEROWS|
|可更新性|DBPROP_UPDATABILITY|
|使用書籤|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令的動態屬性
 下列屬性會新增至**屬性**集合**命令**物件。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|基底路徑|SSPROP_STREAM_BASEPATH|
|區塊存放裝置物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書籤型別|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|將插入的資料列的變更|DBPROP_CHANGEINSERTEDROWS|
|資料行權限|DBPROP_COLUMNRESTRICT|
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|
|內容類型|SSPROP_STREAM_CONTENTTYPE|
|資料指標自動提取|SSPROP_CURSORAUTOFETCH|
|延後的資料行|DBPROP_DEFERRED|
|延遲準備|SSPROP_DEFERPREPARE|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後擷取|DBPROP_CANFETCHBACKWARDS|
|保存資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|固定的資料列|DBPROP_IMMOBILEROWS|
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
|輸出的編碼屬性|DBPROP_OUTPUTENCODING|
|輸出資料流屬性|DBPROP_OUTPUTSTREAM|
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
|伺服器資料指標|DBPROP_SERVERCURSOR|
|插入的伺服器資料|DBPROP_SERVERDATAONINSERT|
|略過刪除書籤|DBPROP_BOOKMARKSKIP|
|強式資料列識別|DBPROP_STRONGIDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用書籤|DBPROP_BOOKMARKS|
|XML 根|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 特定的實作詳細資料和 Microsoft SQL Server OLE DB 提供者的功能資訊，請參閱[SQL Server 提供者](http://msdn.microsoft.com/en-us/adf1d6c4-5930-444a-9248-ff1979729635)。

## <a name="see-also"></a>另請參閱
 [ConnectionString 屬性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
