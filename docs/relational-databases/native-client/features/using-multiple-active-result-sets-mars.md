---
title: 使用 Multiple Active Result Set (MARS) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, MARS
- SQLNCLI, MARS
- data access [SQL Server Native Client], MARS
- Multiple Active Result Sets
- SQL Server Native Client, MARS
- MARS [SQL Server]
- SQL Server Native Client ODBC driver, MARS
ms.assetid: ecfd9c6b-7d29-41d8-af2e-89d7fb9a1d83
caps.latest.revision: 56
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a6007a91d3704f6bf557c6a060bacee5788f751d
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703419"
---
# <a name="using-multiple-active-result-sets-mars"></a>使用 Multiple Active Result Sets (MARS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中導入支援對 multiple active result sets (MARS) 應用程式存取[!INCLUDE[ssDE](../../../includes/ssde-md.md)]。 在舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，資料庫應用程式無法在連接上維持多個作用中陳述式。 當使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設結果集時，應用程式必須從一個批次處理或取消所有結果集，然後才能夠在該連接上執行任何其他批次。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 導入了新的連接屬性，好讓應用程式在每個連接上可以有一個以上的暫止要求，而且特別是每個連接上可以有一個以上的使用中預設結果集。  
  
 MARS 會使用以下的新功能來簡化應用程式設計：  
  
-   應用程式可以開啟多個預設結果集，而且可以交錯讀取這些結果集。  
  
-   當開啟預設結果集時，應用程式可以執行其他陳述式 (例如 INSERT、UPDATE、DELETE 和預存程序呼叫)。  
  
 以下的指導方針對於使用 MARS 的應用程式非常有用：  
  
-   預設結果集應該用於單一 SQL 陳述式 (SELECT、DML with OUTPUT、RECEIVE、READ TEXT 等等) 所產生的短期或簡短結果集。  
  
-   伺服器資料指標應該用於單一 SQL 陳述式所產生的較長期或大型結果集。  
  
-   一定要針對程序要求 (不論它們是否會傳回結果) 以及可傳回多個結果的批次讀取到結果結尾。  
  
-   盡可能使用 API 呼叫來變更連接屬性，並優先管理交易，而非 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式。  
  
-   在 MARS 中，當執行並行批次時會禁止工作階段範圍的模擬。  
  
> [!NOTE]  
>  預設不會啟用 MARS 功能。 若要在利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時使用 MARS，您必須在連接字串中特別啟用它。 如需詳細資訊，請參閱本主題稍後的「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者」和「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式」章節。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不會限制連接上作用中陳述式的數目。  
  
 不需要有多個單一多重陳述式批次或預存程序同時執行的一般應用程式將會因為 MARS 而受益，而不必了解 MARS 的實作方式。 但是，具有更複雜需求的應用程式確實需要考量這件事。  
  
 MARS 可啟用單一連接內多個要求的交錯執行。 也就是說，它可允許批次執行，而且當它執行時，可允許其他要求執行。 但是請注意，MARS 是以交錯來定義，而不是以平行執行來定義。  
  
 MARS 基礎結構可讓多個批次以交錯方式執行，但是只能在定義良好的點上切換執行。 此外，大多數的陳述式都必須在批次內自動執行。 陳述式會傳回資料列至用戶端，有時稱為*產生點*，才能完成以前交錯執行時的資料列會傳送至用戶端，例如：  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 當執行可以切換到其他 MARS 要求之前，當做預存程序或批次的一部分執行的其他任何陳述式都必須執行到完成為止。  
  
 批次交錯執行的確切方式會受到一些因素的影響，而且很難預測包含產生點之多個批次中將要執行命令的確切順序。 請小心避免因為這類複雜批次的交錯執行所產生之不必要的副作用。  
  
 若要避免問題的發生，請使用 API 呼叫 (而非 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式) 來管理連接狀態 (SET、USE) 和交易 (BEGIN TRAN、COMMIT、ROLLBACK)，其方式是不要將這些陳述式併入同樣包含產生點的多重陳述式批次內，以及取用或取消所有結果來序列化這類批次的執行。  
  
> [!NOTE]  
>  在啟用 MARS 時啟動手動或隱含交易的批次或預存程序必須先完成交易，然後才能結束批次。 如果不是這樣的話，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會在批次完成時回復交易所做的所有變更。 這類交易是由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 當做批次範圍的交易來管理。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中導入了新類型的交易，好讓現有行為良好的預存程序在啟用 MARS 時可以使用。 如需批次範圍交易的詳細資訊，請參閱[Transaction 陳述式&#40;TRANSACT-SQL&#41;](~/t-sql/statements/statements.md)。  
  
 如需從 ADO 使用 MARS 的範例，請參閱[使用 ADO 搭配 SQL Server Native Client](../../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md)。  
  
## <a name="in-memory-oltp"></a>In-Memory OLTP  
 記憶體中 OLTP 支援 MARS 使用查詢和原生編譯的預存程序。 MARS 可讓您從多個查詢，而不需要完全擷取每個結果集之前從新的結果集提取資料列將要求傳送要求資料。 為了能夠成功讀取從多個開啟的結果集，您必須使用 MARS 啟用連接。  
  
 MARS 預設會停用，必須明確啟用它藉由新增`MultipleActiveResultSets=True`的連接字串。 下列範例會示範如何連接到 SQL server 執行個體，並指定已啟用 MARS:  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 使用記憶體內部 OLTP 的 MARS 實際上是 MARS 相同 SQL 引擎的其餘部分。 下面列出使用 MARS，在記憶體最佳化資料表和原生方式編譯預存程序時的差異。  
  
 **MARS 和記憶體最佳化資料表**  
  
 使用 MARS 啟用連接的磁碟和記憶體最佳化資料表之間的差異如下：  
  
-   兩個陳述式可以修改相同的目標物件中的資料，但是如果它們都嘗試修改同一筆記錄寫入-寫入衝突會導致新的作業失敗。 不過，如果這兩種作業修改了不同的記錄，作業將會成功。  
  
-   在快照隔離下的每個陳述式執行，因此新的作業無法查看現有的陳述式所做的變更。 即使在相同交易下執行並行的陳述式 SQL 引擎會建立批次範圍交易的每個陳述式與彼此隔離。 不過，批次範圍交易仍繫結在一起讓一個批次範圍交易的回復會影響其他在相同批次的。  
  
-   DDL 作業不允許在使用者交易中，它們將會立即失敗。  
  
 **MARS 和原生編譯的預存程序**  
  
 原生編譯的預存程序可以在啟用 MARS 連接執行，而且只有在遇到 yield 點時，才可產生另一個陳述式的執行。 Yield 點需要是唯一的陳述式可能會產生另一個陳述式執行原生編譯預存程序內的 SELECT 陳述式。 如果 SELECT 陳述式不存在於它不會產生的程序，它會執行到完成其他陳述式開始之前。  
  
 **MARS 和記憶體內部 OLTP 交易**  
  
 陳述式和為交錯的 atomic 區塊所做的變更會互相隔離。 比方說，如果一個陳述式或不可部分完成的區塊會進行一些變更，並接著就會產生另一個陳述式的執行，新的陳述式將不會看到第一個陳述式所做的變更。 此外，當第一個陳述式繼續執行時，它不會看到任何其他陳述式所做的任何變更。 陳述式只會看到，已完成並且陳述式開始之前認可的變更。  
  
 可以使用 BEGIN TRANSACTION 陳述式在目前的使用者交易中啟動新的使用者交易 – 這是支援只能在 interop 模式中，因此只能從 T-SQL 陳述式，呼叫 BEGIN TRANSACTION，不從內原生編譯預存程序。您可以建立儲存點使用 SAVE TRANSACTION 或應用程式開發介面呼叫交易的交易。Save(save_point_name) 回復到儲存點。 這項功能也會啟用只會從 T-SQL 陳述式，並不是從在原生編譯的預存程序。  
  
 **MARS 和資料行存放區索引**  
  
 SQL Server （從 2016年開始） 與資料行存放區索引支援 MARS。 SQL Server 2014 使用 MARS 來與具有資料行存放區索引的資料表進行唯讀連線。    不過，SQL Server 2014 不支援 MARS 在具備資料行存放區索引的資料表上，進行並行資料操作語言 (DML) 作業。 當發生這種情況時，SQL Server 將會終止連線，並中止交易。   SQL Server 2012 有唯讀資料行存放區索引，MARS 不適用於它們。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 提供者  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可透過 SSPROP_INIT_MARSCONNECTION 資料來源初始化屬性，這在 DBPROPSET_SQLSERVERDBINIT 屬性集中實作的加入來支援 MARS。 此外，新的連接字串關鍵字， **MarsConn**也已經加入。 它可接受**true**或**false**值;**false**是預設值。  
  
 資料來源屬性 DBPROP_MULTIPLECONNECTIONS 預設為 VARIANT_TRUE。 這表示，為了支援多個並行命令和資料列集物件，此提供者將會繁衍多個連接。 當啟用 MARS 時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端可以多個命令和資料列集物件上支援單一連接，好讓 multiple_connections 為 variant_false 預設。  
  
 如需有關對 DBPROPSET_SQLSERVERDBINIT 屬性集的增強功能的詳細資訊，請參閱[初始化和授權屬性](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
### <a name="sql-server-native-client-ole-db-provider-example"></a>SQL Server Native Client OLE DB 提供者範例  
 在此範例中，建立資料來源物件是使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生 OLE DB 提供者，而且 MARS 會使用 DBPROPSET_SQLSERVERDBINIT 屬性集的工作階段物件建立之前啟用。  
  
```  
#include <sqlncli.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL,  
   CLSCTX_INPROC_SERVER,  
   IID_IDBInitialize,   
    (void**)&pIDBInitialize);  
  
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void**)&pIDBProperties);  
  
// Set the MARS property.  
DBPROP rgPropMARS;  
  
// The following is necessary since MARS is off by default.  
rgPropMARS.dwPropertyID = SSPROP_INIT_MARSCONNECTION;  
rgPropMARS.dwOptions = DBPROPOPTIONS_REQUIRED;  
rgPropMARS.dwStatus = DBPROPSTATUS_OK;  
rgPropMARS.colid = DB_NULLID;  
V_VT(&(rgPropMARS.vValue)) = VT_BOOL;  
V_BOOL(&(rgPropMARS.vValue)) = VARIANT_TRUE;  
  
// Create the structure containing the properties.  
DBPROPSET PropSet;  
PropSet.rgProperties = &rgPropMARS;  
PropSet.cProperties = 1;  
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;  
  
// Get an IDBProperties pointer and set the initialization properties.  
pIDBProperties->SetProperties(1, &PropSet);  
pIDBProperties->Release();  
  
// Initialize the data source object.  
hr = pIDBInitialize->Initialize();  
  
//Create a session object from a data source object.  
IOpenRowset * pIOpenRowset = NULL;  
hr = IDBInitialize->QueryInterface(IID_IDBCreateSession, (void**)&pIDBCreateSession));  
hr = pIDBCreateSession->CreateSession(  
   NULL,             // pUnkOuter  
   IID_IOpenRowset,  // riid  
  &pIOpenRowset ));  // ppSession  
  
// Create a rowset with a firehose mode cursor.  
IRowset *pIRowset = NULL;  
DBPROP rgRowsetProperties[2];  
  
// To get a firehose mode cursor request a   
// forward only read only rowset.  
rgRowsetProperties[0].dwPropertyID = DBPROP_IRowsetLocate;  
rgRowsetProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[0].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[0].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[0].vValue));  
rgRowsetProperties[0].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[0].vValue.boolVal = VARIANT_FALSE;  
  
rgRowsetProperties[1].dwPropertyID = DBPROP_IRowsetChange;  
rgRowsetProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[1].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[1].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[1].vValue));  
rgRowsetProperties[1].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[1].vValue.boolVal = VARIANT_FALSE;  
  
DBPROPSET rgRowsetPropSet[1];  
rgRowsetPropSet[0].rgProperties = rgRowsetProperties  
rgRowsetPropSet[0].cProperties = 2  
rgRowsetPropSet[0].guidPropertySet = DBPROPSET_ROWSET;  
  
hr = pIOpenRowset->OpenRowset (NULL,  
   &TableID,  
   NULL,  
   IID_IRowset,  
   1,  
   rgRowsetPropSet  
   (IUnknown**)&pIRowset);  
```  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驅動程式  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式可透過 新增項目來支援 MARS [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)和[SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)函式。 已經加入 SQL_COPT_SS_MARS_ENABLED 來接受 SQL_MARS_ENABLED_YES 或 SQL_MARS_ENABLED_NO，而預設值為 SQL_MARS_ENABLED_NO。 此外，新的連接字串關鍵字， **Mars_Connection**也已經加入。 它可接受 "yes" 或 "no" 值；預設值是 "no"。  
  
### <a name="sql-server-native-client-odbc-driver-example"></a>SQL Server Native Client ODBC 驅動程式範例  
 在此範例中， **SQLSetConnectAttr**函式用來啟用 MARS，然後再呼叫**SQLDriverConnect**函式，連接至資料庫。 建立連接之後，兩個**SQLExecDirect**函式的呼叫相同的連接上建立兩個不同的結果集。  
  
```  
#include <sqlncli.h>  
  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MARS_ENABLED, SQL_MARS_ENABLED_YES, SQL_IS_UINTEGER);  
SQLDriverConnect(hdbc, hwnd,   
   "DRIVER=SQL Server Native Client 10.0;  
   SERVER=(local);trusted_connection=yes;", SQL_NTS, szOutConn,   
   MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt2);  
  
// The 2nd execute would have failed with connection busy error if  
// MARS were not enabled.  
SQLExecDirect(hstmt1, L”SELECT * FROM Authors”, SQL_NTS);  
SQLExecDirect(hstmt2, L”SELECT * FROM Titles”, SQL_NTS);  
  
// Result set processing can interleave.  
SQLFetch(hstmt1);  
SQLFetch(hstmt2);  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [使用 QL Server 預設結果集](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
  
