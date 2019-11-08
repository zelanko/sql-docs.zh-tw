---
title: 使用 Multiple Active Result Sets （MARS） |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b72f93aa979c504c0f6eeb6a3b867cc8360728f
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761308"
---
# <a name="using-multiple-active-result-sets-mars"></a>使用 Multiple Active Result Sets (MARS)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 在存取 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 的應用程式中導入了對 Multiple Active Result Set (MARS) 的支援。 在舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，資料庫應用程式無法在連接上維持多個作用中陳述式。 當使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設結果集時，應用程式必須從一個批次處理或取消所有結果集，然後才能夠在該連接上執行任何其他批次。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 導入了新的連接屬性，好讓應用程式在每個連接上可以有一個以上的暫止要求，而且特別是每個連接上可以有一個以上的使用中預設結果集。  
  
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
> 根據預設，驅動程式不會啟用 MARS 功能。 若要在使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時使用 MARS，您必須在連接字串中特別啟用 MARS。 不過，如果應用程式偵測到驅動程式支援 MARS，某些應用程式可能會預設啟用 MARS。 針對這些應用程式，您可以視需要停用連接字串中的 MARS。 如需詳細資訊，請參閱本主題稍後的「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者」和「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式」章節。

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不會限制連接上作用中陳述式的數目。  
  
 不需要同時執行多個單一多重語句批次或預存程式的一般應用程式，將受益于 MARS，而不必瞭解如何實作為 MARS。 但是，具有更複雜需求的應用程式確實需要考量這件事。  
  
 MARS 可啟用單一連接內多個要求的交錯執行。 也就是說，它可允許批次執行，而且當它執行時，可允許其他要求執行。 但是請注意，MARS 是以交錯來定義，而不是以平行執行來定義。  
  
 MARS 基礎結構可讓多個批次以交錯方式執行，但是只能在定義良好的點上切換執行。 此外，大多數的陳述式都必須在批次內自動執行。 傳回資料列給用戶端的語句（有時也稱為「*產生點*」），可以在資料列傳送到用戶端時，于完成前交錯執行，例如：  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 當執行可以切換到其他 MARS 要求之前，當做預存程序或批次的一部分執行的其他任何陳述式都必須執行到完成為止。  
  
 批次交錯執行的確切方式會受到一些因素的影響，而且很難預測包含產生點之多個批次中將要執行命令的確切順序。 請小心避免因為這類複雜批次的交錯執行所產生之不必要的副作用。  
  
 若要避免問題的發生，請使用 API 呼叫 (而非 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式) 來管理連接狀態 (SET、USE) 和交易 (BEGIN TRAN、COMMIT、ROLLBACK)，其方式是不要將這些陳述式併入同樣包含產生點的多重陳述式批次內，以及取用或取消所有結果來序列化這類批次的執行。  
  
> [!NOTE]  
>  在啟用 MARS 時啟動手動或隱含交易的批次或預存程序必須先完成交易，然後才能結束批次。 如果不是這樣的話，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會在批次完成時回復交易所做的所有變更。 這類交易是由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 當做批次範圍的交易來管理。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中導入了新類型的交易，好讓現有行為良好的預存程序在啟用 MARS 時可以使用。 如需批次範圍交易的詳細資訊，請參閱[Transaction 語句&#40;transact-sql&#41;](~/t-sql/statements/statements.md)。  
  
 如需從 ADO 使用 MARS 的範例，請參閱搭配[使用 ado 與 SQL Server Native Client](../../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md)。  
  
## <a name="in-memory-oltp"></a>In-Memory OLTP  
 記憶體內部 OLTP 支援使用查詢和原生編譯預存程式的 MARS。 MARS 可讓您從多個查詢要求資料，而不需要在傳送要求以從新的結果集提取資料列之前，完全取得每個結果集。 若要成功讀取多個開啟的結果集，您必須使用已啟用 MARS 的連接。  
  
 MARS 預設為停用，因此您必須藉由將 `MultipleActiveResultSets=True` 新增至連接字串來明確加以啟用。 下列範例示範如何連接到 SQL Server 的實例，並指定啟用 MARS：  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 具有記憶體內部 OLTP 的 MARS 基本上與其他 SQL 引擎中的 MARS 相同。 以下列出在記憶體優化資料表和原生編譯的預存程式中使用 MARS 時的差異。  
  
 **MARS 和記憶體優化資料表**  
  
 以下是使用 MARS 啟用的連接時，磁片型和記憶體優化資料表之間的差異：  
  
-   兩個語句可以修改相同目標物件中的資料，但如果兩者都嘗試修改相同的記錄，則寫入寫入衝突會導致新的作業失敗。 不過，如果這兩個作業都修改不同的記錄，作業將會成功。  
  
-   每個語句都會在快照集隔離下執行，因此新的作業無法看到現有語句所做的變更。 即使並行語句是在相同的交易下執行，SQL 引擎還是會針對每個彼此隔離的語句，建立批次範圍的交易。 不過，批次範圍的交易仍會系結在一起，因此，回復一個批次範圍的交易會影響相同批次中的其他交易。  
  
-   使用者交易中不允許使用 DDL 作業，因此它們會立即失敗。  
  
 **MARS 和原生編譯的預存程序**  
  
 原生編譯的預存程式可以在已啟用 MARS 的連接中執行，而且只有在遇到產生點時，才會產生另一個語句的執行。 「產生點」需要 SELECT 語句，這是原生編譯預存程式內的唯一語句，可以產生對另一個語句的執行。 如果 SELECT 語句不存在於程式中，就不會產生它，而是在其他語句開始之前執行到完成。  
  
 **MARS 和記憶體內部 OLTP 交易**  
  
 語句所做的變更，以及交錯式的不可部分完成區塊會彼此隔離。 例如，如果一個語句或不可部分完成的區塊會進行一些變更，然後產生另一個語句的執行，新的語句就不會看到第一個語句所做的變更。 此外，當第一個語句繼續執行時，不會看到任何其他語句所做的任何變更。 語句只會在語句啟動之前，看到已經完成和認可的變更。  
  
 使用 BEGIN TRANSACTION 語句，可以在目前的使用者交易內啟動新的使用者交易-這只在 interop 模式中受到支援，因此只能從 T-sql 語句呼叫 BEGIN TRANSACTION，而不是從原生編譯的預存步.您可以使用 SAVE TRANSACTION 或對交易的 API 呼叫，在交易中建立儲存點。儲存（save_point_name）以回復到儲存點。 這項功能也只能從 T-sql 語句啟用，而不是從原生編譯的預存程式中啟用。  
  
 **MARS 和資料行存放區索引**  
  
 SQL Server （從2016開始）支援 MARS 搭配資料行存放區索引。 SQL Server 2014 使用 MARS 來與具有資料行存放區索引的資料表進行唯讀連線。    不過，SQL Server 2014 不支援 MARS 在具備資料行存放區索引的資料表上，進行並行資料操作語言 (DML) 作業。 發生這種情況時，SQL Server 會終止連接並中止交易。   SQL Server 2012 具有唯讀的資料行存放區索引，而 MARS 則不適用。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 提供者  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者透過新增 SSPROP_INIT_MARSCONNECTION 資料來源初始化屬性（在 DBPROPSET_SQLSERVERDBINIT 屬性集內執行）來支援 MARS。 此外，也已經加入新的連接字串關鍵字 **MarsConn**。 它接受**true**或**false**值;預設值為**false** 。  
  
 資料來源屬性 DBPROP_MULTIPLECONNECTIONS 預設為 VARIANT_TRUE。 這表示，為了支援多個並行命令和資料列集物件，此提供者將會繁衍多個連接。 啟用 MARS 時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 可以在單一連接上支援多個命令和資料列集物件，因此 MULTIPLE_CONNECTIONS 預設會設定為 [VARIANT_FALSE]。  
  
 如需 DBPROPSET_SQLSERVERDBINIT 屬性集之增強功能的詳細資訊，請參閱[初始化和授權屬性](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
### <a name="sql-server-native-client-ole-db-provider-example"></a>SQL Server Native Client OLE DB 提供者範例  
 在此範例中，會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native OLE DB 提供者建立資料來源物件，而且在建立會話物件之前，會使用 DBPROPSET_SQLSERVERDBINIT 屬性集來啟用 MARS。  
  
```cpp
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
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式透過 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 和[SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)函式的新增功能支援 MARS。 已經加入 SQL_COPT_SS_MARS_ENABLED 來接受 SQL_MARS_ENABLED_YES 或 SQL_MARS_ENABLED_NO，而預設值為 SQL_MARS_ENABLED_NO。 此外，也會加入新的連接字串關鍵字**Mars_Connection**。 它可接受 "yes" 或 "no" 值；預設值是 "no"。  
  
### <a name="sql-server-native-client-odbc-driver-example"></a>SQL Server Native Client ODBC 驅動程式範例  
 在此範例中， **SQLSetConnectAttr**函數是用來在呼叫**SQLDriverConnect**函式來連接資料庫之前啟用 MARS。 一旦建立連接，就會呼叫兩個**SQLExecDirect**函數，以在相同的連接上建立兩個不同的結果集。  
  
```cpp
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
SQLExecDirect(hstmt1, L"SELECT * FROM Authors", SQL_NTS);  
SQLExecDirect(hstmt2, L"SELECT * FROM Titles", SQL_NTS);  
  
// Result set processing can interleave.  
SQLFetch(hstmt1);  
SQLFetch(hstmt2);  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [使用 QL Server 預設結果集](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
  
