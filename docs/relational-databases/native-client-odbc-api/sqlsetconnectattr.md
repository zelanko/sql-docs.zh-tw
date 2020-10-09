---
title: SQLSetConnectAttr |Microsoft Docs
description: 瞭解 SQLSetConnectAttr 中的連接屬性，包括它們的設定時間，以及 SQL Server Native Client ODBC 驅動程式中的可能值。
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetConnectAttr function
ms.assetid: d21b5cf1-3724-43f7-bc96-5097df0677b4
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 03dd345e2b7fc3be27b9bd1c61f3d252d7afb229
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867810"
---
# <a name="sqlsetconnectattr"></a>SQLSetConnectAttr

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會忽略 SQL_ATTR_CONNECTION_TIMEOUT 的設定。  
  
 也會忽略 SQL_ATTR_TRANSLATE_LIB；不支援指定其他的翻譯程式庫。 若要讓應用程式更容易匯出以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft ODBC 驅動程式，任何使用 SQL_ATTR_TRANSLATE_LIB 設定的值將會複製到驅動程式管理員中的緩衝區內外。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會將可重複的讀取交易隔離實作為可序列化。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 導入了新交易隔離屬性 SQL_COPT_SS_TXN_ISOLATION 的支援。 將 SQL_COPT_SS_TXN_ISOLATION 設定為 SQL_TXN_SS_SNAPSHOT 代表交易會在快照隔離等級之下發生。  
  
> [!NOTE]  
> SQL_ATTR_TXN_ISOLATION 可用來設定 SQL_TXN_SS_SNAPSHOT 以外的所有其他隔離等級。 如果您想要使用快照集隔離，就必須透過 SQL_COPT_SS_TXN_ISOLATION 設定 SQL_TXN_SS_SNAPSHOT。 不過，您可以使用 SQL_ATTR_TXN_ISOLATION 或 SQL_COPT_SS_TXN_ISOLATION 來擷取隔離等級。  
  
 將 ODBC 陳述式屬性升級至連接屬性可能會產生非預期的後果。 您可以將要求伺服器資料指標以進行結果集處理的陳述式屬性升級至連接。 例如，如果您將 ODBC 陳述式屬性 SQL_ATTR_CONCURRENCY 設定為比預設值 SQL_CONCUR_READ_ONLY 更具限制性的值，就會引導驅動程式針對在連接時送出的所有陳述式使用動態資料指標。 針對連接的陳述式執行 ODBC 目錄函數會傳回 SQL_SUCCESS_WITH_INFO 以及一個診斷記錄，表示資料指標行為已經變更成唯讀。 嘗試執行包含相同連接之 COMPUTE 子句的 Transact-SQL SELECT 陳述式會失敗。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會針對 sqlncli.h 中定義的 ODBC 連接屬性支援一些驅動程式特有的延伸模組。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式可能會要求在連接之前設定此屬性，否則如果已經設定，驅動程式可能會忽略此屬性。 下表將列出各項限制。  
  
|SQL Server 屬性|在連接至伺服器之前或之後設定|  
|--------------------------|----------------------------------------------|  
|SQL_COPT_SS_ANSI_NPW|之前|  
|SQL_COPT_SS_APPLICATION_INTENT|之前|  
|SQL_COPT_SS_ATTACHDBFILENAME|之前|  
|SQL_COPT_SS_BCP|之前|  
|SQL_COPT_SS_BROWSE_CONNECT|之前|  
|SQL_COPT_SS_BROWSE_SERVER|之前|  
|SQL_COPT_SS_CONCAT_NULL|之前|  
|SQL_COPT_SS_CONNECTION_DEAD|在|  
|SQL_COPT_SS_ENCRYPT|之前|  
|SQL_COPT_SS_ENLIST_IN_DTC|在|  
|SQL_COPT_SS_ENLIST_IN_XA|在|  
|SQL_COPT_SS_FALLBACK_CONNECT|之前|  
|SQL_COPT_SS_FAILOVER_PARTNER|之前|  
|SQL_COPT_SS_INTEGRATED_SECURITY|之前|  
|SQL_COPT_SS_MARS_ENABLED|之前|  
|SQL_COPT_SS_MULTISUBNET_FAILOVER|之前|  
|SQL_COPT_SS_OLDPWD|之前|  
|SQL_COPT_SS_PERF_DATA|在|  
|SQL_COPT_SS_PERF_DATA_LOG|在|  
|SQL_COPT_SS_PERF_DATA_LOG_NOW|在|  
|SQL_COPT_SS_PERF_QUERY|在|  
|SQL_COPT_SS_PERF_QUERY_INTERVAL|在|  
|SQL_COPT_SS_PERF_QUERY_LOG|在|  
|SQL_COPT_SS_PRESERVE_CURSORS|之前|  
|SQL_COPT_SS_QUOTED_IDENT|或|  
|SQL_COPT_SS_TRANSLATE|或|  
|SQL_COPT_SS_TRUST_SERVER_CERTIFICATE|之前|  
|SQL_COPT_SS_TXN_ISOLATION|或|  
|SQL_COPT_SS_USE_PROC_FOR_PREP|或|  
|SQL_COPT_SS_USER_DATA|或|  
|SQL_COPT_SS_WARN_ON_CP_ERROR|之前|  
  
 針對相同工作階段、資料庫或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 狀態使用預先連接屬性與對等 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命令，可能會產生非預期的行為。 例如，  
  
```  
SQLSetConnectAttr(SQL_COPT_SS_QUOTED_IDENT, SQL_QI_ON) // turn ON via attribute  
SQLDriverConnect(...);  
SQLExecDirect("SET QUOTED_IDENTIFIER OFF") // turn OFF via Transact-SQL  
SQLSetConnectAttr(SQL_ATTR_CURRENT_CATALOG, ...) // restores to pre-connect attribute value  
```  

<a name="sqlcoptssansinpw"></a>
## <a name="sql_copt_ss_ansi_npw"></a>SQL_COPT_SS_ANSI_NPW  
 SQL_COPT_SS_ANSI_NPW 會在比較與串連、字元資料類型填補和警告中啟用或停用 NULL ISO 處理的使用方式。 如需詳細資訊，請參閱 SET ANSI_NULLS、SET ANSI_PADDING、SET ANSI_WARNINGS 和 SET CONCAT_NULL_YIELDS_NULL。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_AD_ON|預設值。 連接會使用 ANSI 預設行為來處理 NULL 比較、填補、警告和 NULL 串連。|  
|SQL_AD_OFF|連接會針對 NULL、字元資料類型填補和警告使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定義的處理方式。|  
  
 如果您使用連接共用，SQL_COPT_SS_ANSI_NPW 應該在連接字串中設定，而不是在 SQLSetConnectAttr 中設定。 已經建立連接之後，在使用連接共用時，任何嘗試變更此屬性的行為將會以無訊息的方式發生失敗。  

<a name="sqlcoptssapplicationintent"></a>
## <a name="sql_copt_ss_application_intent"></a>SQL_COPT_SS_APPLICATION_INTENT  
 宣告連接到伺服器時的應用程式工作負載類型。 可能的值為 **Readonly** 和 **ReadWrite**。 例如：  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_APPLICATION_INTENT, TEXT("Readonly"), SQL_NTS)  
```  
  
 預設值為 **ReadWrite**。 如需有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的 ag 支援的詳細資訊 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ，請參閱 [SQL Server Native Client 高可用性和嚴重損壞修復的支援](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  

<a name="sqlcoptssattachdbfilename"></a>
## <a name="sql_copt_ss_attachdbfilename"></a>SQL_COPT_SS_ATTACHDBFILENAME  
 SQL_COPT_SS_ATTACHDBFILENAME 會指定可附加資料庫的主要檔案名稱。 此資料庫會附加，而且變成連接的預設資料庫。 若要使用 SQL_COPT_SS_ATTACHDBFILENAME 您必須指定資料庫的名稱，做為連接屬性的值 SQL_ATTR_CURRENT_CATALOG 或在 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)的 database = 參數中。 如果該資料庫先前已附加，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將不會重新附加它。  
  
|值|描述|  
|-----------|-----------------|  
|字元字串的 SQLPOINTER|此字串包含要附加之資料庫的主要檔案名稱。 請加入檔案的完整路徑名稱。|  

<a name="sqlcoptssbcp"></a>
## <a name="sql_copt_ss_bcp"></a>SQL_COPT_SS_BCP  
 SQL_COPT_SS_BCP 會針對連接啟用大量複製函數。 如需詳細資訊，請參閱 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_BCP_OFF|預設值。 無法針對連接使用大量複製函數。|  
|SQL_BCP_ON|可以針對連接使用大量複製函數。|  

<a name="sqlcoptssbrowseconnect"></a>
## <a name="sql_copt_ss_browse_connect"></a>SQL_COPT_SS_BROWSE_CONNECT  
 這個屬性是用來自訂 [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)所傳回的結果集。 SQL_COPT_SS_BROWSE_CONNECT 會啟用或停用從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列舉執行個體傳回其他資訊的作業。 這可能會包括伺服器是否為叢集、不同執行個體的名稱，以及版本號碼等資訊。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_MORE_INFO_NO|預設值。 傳回伺服器的清單。|  
|SQL_MORE_INFO_YES|**SQLBrowseConnect** 會傳回伺服器屬性的擴充字串。|  

<a name="sqlcoptssbrowseserver"></a>
## <a name="sql_copt_ss_browse_server"></a>SQL_COPT_SS_BROWSE_SERVER  
 這個屬性是用來自訂 **SQLBrowseConnect**所傳回的結果集。 SQL_COPT_SS_BROWSE_SERVER 指定 **SQLBrowseConnect** 傳回信息的伺服器名稱。  
  
|值|描述|  
|-----------|-----------------|  
|computername|**SQLBrowseConnect** 會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指定電腦上的實例清單。 雙反斜線 (\\ \\) 不應該用於伺服器名稱 (例如，而不是使用 \\ \MyServer，則應該使用) 來取代 MyServer。|  
|NULL|預設值。 **SQLBrowseConnect** 會傳回網域中所有伺服器的資訊。|  

<a name="sqlcoptssconcatnull"></a>
## <a name="sql_copt_ss_concat_null"></a>SQL_COPT_SS_CONCAT_NULL  
 SQL_COPT_SS_CONCAT_NULL 會在串連字元時啟用或停用 NULL ISO 處理的使用方式。 如需詳細資訊，請參閱 SET CONCAT_NULL_YIELDS_NULL。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_CN_ON|預設值。 連接會在串連字串時使用 ISO 預設行為來處理 NULL 值。|  
|SQL_CN_OFF|連接會在串連字串時使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定義的行為來處理 NULL 值。|  

<a name="sqlcoptssencrypt"></a>
## <a name="sql_copt_ss_encrypt"></a>SQL_COPT_SS_ENCRYPT  
 控制連接的加密。  
  
 加密會使用伺服器上的憑證。 除非連接屬性 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE 設定為 SQL_TRUST_SERVER_CERTIFICATE_YES 或連接字串包含 "TrustServerCertificate=yes"，否則這個憑證必須經過憑證授權單位驗證。 如果其中一項條件成立，當伺服器上沒有任何憑證時，伺服器所產生並簽署的憑證就可用來加密連接。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_EN_ON|連接將會加密。|  
|SQL_EN_OFF|連接將不會加密。 此為預設值。|  

<a name="sqlcoptssenlistindtc"></a>
## <a name="sql_copt_ss_enlist_in_dtc"></a>SQL_COPT_SS_ENLIST_IN_DTC  
 用戶端會呼叫 Microsoft Distributed Transaction Coordinator (MS DTC) OLE DB **ITransactionDispenser：： BeginTransaction** 方法來開始 MS DTC 交易，並建立代表交易的 MS DTC 交易對象。 然後，應用程式會使用 SQL_COPT_SS_ENLIST_IN_DTC 選項來呼叫 **SQLSetConnectAttr** ，以便將交易對象與 ODBC 連接產生關聯。 所有相關的資料庫活動都將在 MS DTC 交易的保護底下進行。 應用程式會使用 SQL_DTC_DONE 來呼叫 **SQLSetConnectAttr** ，以結束連接的 DTC 關聯。  
  
|值|描述|  
|-----------|-----------------|  
|DTC object*|指定要匯出至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之交易的 MS DTC OLE 交易物件。|  
|SQL_DTC_DONE|分隔 DTC 交易的結尾。|  

<a name="sqlcoptssenlistinxa"></a>
## <a name="sql_copt_ss_enlist_in_xa"></a>SQL_COPT_SS_ENLIST_IN_XA  
 若要使用 XA 相容的交易處理器來開始 XA 交易 (TP) ，用戶端會呼叫 Open Group **tx_begin** 函數。 然後，應用程式會使用 SQL_COPT_SS_ENLIST_IN_XA 參數 TRUE 來呼叫 **SQLSetConnectAttr** ，以將 XA 交易與 ODBC 連接產生關聯。 所有相關的資料庫活動都將在 XA 交易的保護底下進行。 若要結束與 ODBC 連接的 XA 關聯，用戶端必須使用 SQL_COPT_SS_ENLIST_IN_XA 參數 FALSE 來呼叫 **SQLSetConnectAttr** 。 如需詳細資訊，請參閱 Microsoft 分散式交易協調器文件集。  
  
## <a name="sql_copt_ss_fallback_connect"></a>SQL_COPT_SS_FALLBACK_CONNECT  
 已不再支援這個屬性。  

<a name="sqlcoptssfailoverpartner"></a>
## <a name="sql_copt_ss_failover_partner"></a>SQL_COPT_SS_FAILOVER_PARTNER  
 用於指定或擷取在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中鏡像資料庫所使用之容錯移轉夥伴的名稱，而且這是以 null 結尾的字元字串，必須在一開始建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連接前設定。  
  
 進行連接之後，應用程式可以使用 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) 來查詢此屬性，以判斷容錯移轉夥伴的身分識別。 如果主要伺服器沒有容錯移轉夥伴，此屬性將會傳回空字串。 這可讓智慧型應用程式快取最近決定的備份伺服器，但是此類應用程式應該會注意到此資訊只會在第一次建立 (如果共用，則重設) 連接時更新，而且在長期連接後會變成過期。  
  
 如需詳細資訊，請參閱[使用資料庫鏡像](../../relational-databases/native-client/features/using-database-mirroring.md)。  

<a name="sqlcoptssintegratedsecurity"></a>
## <a name="sql_copt_ss_integrated_security"></a>SQL_COPT_SS_INTEGRATED_SECURITY  
 SQL_COPT_SS_INTEGRATED_SECURITY 會針對伺服器登入的存取驗證強制使用 Windows 驗證。 使用 Windows 驗證時，驅動程式會忽略 **SQLConnect**、 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)或 [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) 處理過程中所提供的使用者識別碼和密碼值。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_IS_OFF|預設值。 在登入時使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來驗證使用者識別碼和密碼。|  
|SQL_IS_ON|使用 Windows 驗證模式來驗證使用者對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的存取權限。|  

<a name="sqlcoptssmarsenabled"></a>
## <a name="sql_copt_ss_mars_enabled"></a>SQL_COPT_SS_MARS_ENABLED  
 這個屬性會啟用或停用 Multiple Active Result Sets (MARS)。 根據預設，MARS 已停用。 您應該在建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連接之前設定這個屬性。 開啟連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後，MARS 將會在連接期間維持啟用或停用狀態。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_MARS_ENABLED_NO|預設值。 停用 Multiple Active Result Sets (MARS)。|  
|SQL_MARS_ENABLED_YES|啟用 MARS。|  
  
 如需 MARS 的詳細資訊，請參閱 [使用 &#40;mars&#41;的 Multiple Active Result Sets ](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)。  

<a name="sqlcoptssmultisubnetfailover"></a>
## <a name="sql_copt_ss_multisubnet_failover"></a>SQL_COPT_SS_MULTISUBNET_FAILOVER  
 如果您的應用程式要連接到不同子網路上的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 可用性群組 (AG)，則這個連接屬性會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 來提供目前使用中伺服器的更快速偵測與連接。 例如：  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MULTISUBNET_FAILOVER, SQL_IS_ON, SQL_IS_INTEGER)  
```  
  
 如需有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的 ag 支援的詳細資訊 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ，請參閱 [SQL Server Native Client 高可用性和嚴重損壞修復的支援](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_IS_ON|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 會在發生容錯移轉時提供更快速的重新連接。|  
|SQL_IS_OFF|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 不會在發生容錯移轉時提供更快速的重新連接。|  

<a name="sqlcoptssoldpwd"></a>
## <a name="sql_copt_ss_oldpwd"></a>SQL_COPT_SS_OLDPWD  
 SQL Server 驗證的密碼逾期是在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中導入的。 目前加入了 SQL_COPT_SS_OLDPWD 屬性，可讓用戶端同時提供舊的和新的密碼進行連接。 設定這個屬性之後，提供者將不會針對第一次連接或後續連接使用連接集區，因為連接字串將會包含已經變更的「舊密碼」。  
  
 如需詳細資訊，請參閱 [以程式設計方式變更密碼](../../relational-databases/native-client/features/changing-passwords-programmatically.md)。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_COPT_SS_OLD_PASSWORD|包含舊密碼之字元字串的 SQLPOINTER。 這個值是唯寫的，而且必須在連接至伺服器之前設定。|  

<a name="sqlcoptssperfdata"></a>
## <a name="sql_copt_ss_perf_data"></a>SQL_COPT_SS_PERF_DATA  
 SQL_COPT_SS_PERF_DATA 會啟動或停止效能資料記錄。 您必須在啟動資料記錄之前設定資料記錄檔名稱。 請參閱下面的 SQL_COPT_SS_PERF_DATA_LOG。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_PERF_START|開始讓驅動程式進行效能資料取樣。|  
|SQL_PERF_STOP|停止讓計數器進行效能資料取樣。|  
  
 如需詳細資訊，請參閱 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)。  

<a name="sqlcoptssperfdatalog"></a>
## <a name="sql_copt_ss_perf_data_log"></a>SQL_COPT_SS_PERF_DATA_LOG  
 SQL_COPT_SS_PERF_DATA_LOG 會指派用來記錄效能資料之記錄檔的名稱。 此記錄檔名稱是以 Null 結束的 ANSI 或 Unicode 字串，端視應用程式編譯方式而定。 應 SQL_NTS *StringLength* 引數。  

<a name="sqlcoptssperfdatalognow"></a>
## <a name="sql_copt_ss_perf_data_log_now"></a>SQL_COPT_SS_PERF_DATA_LOG_NOW  
 SQL_COPT_SS_PERF_DATA_LOG_NOW 會指示驅動程式將統計資料記錄項目寫入磁碟。 應 SQL_NTS *StringLength* 引數。  

<a name="sqlcoptssperfquery"></a>
## <a name="sql_copt_ss_perf_query"></a>SQL_COPT_SS_PERF_QUERY  
 SQL_COPT_SS_PERF_QUERY 會啟動或停止長時間執行查詢的記錄。 您必須在啟動記錄之前提供查詢記錄檔名稱。 應用程式可以透過設定記錄的間隔，定義「長時間執行」。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_PERF_START|啟動長時間執行查詢記錄。|  
|SQL_PERF_STOP|停止長時間執行查詢的記錄。|  
  
 如需詳細資訊，請參閱 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)。  

<a name="sqlcoptssperfqueryinterval"></a>
## <a name="sql_copt_ss_perf_query_interval"></a>SQL_COPT_SS_PERF_QUERY_INTERVAL  
 SQL_COPT_SS_PERF_QUERY_INTERVAL 會設定查詢記錄臨界值 (以毫秒為單位)。 沒有在此臨界值內解決的查詢就會記錄在長時間執行查詢記錄檔中。 查詢臨界值沒有任何上限。 如果查詢臨界值為零，就會導致系統記錄所有查詢。  

<a name="sqlcoptssperfquerylog"></a>
## <a name="sql_copt_ss_perf_query_log"></a>SQL_COPT_SS_PERF_QUERY_LOG  
 SQL_COPT_SS_PERF_QUERY_LOG 會指派用於記錄長時間執行查詢資料之記錄檔的名稱。 此記錄檔名稱是以 Null 結束的 ANSI 或 Unicode 字串，端視應用程式編譯方式而定。 *StringLength*引數應該是 SQL_NTS 或字串的長度（以位元組為單位）。  

<a name="sqlcoptsspreservecursors"></a>
## <a name="sql_copt_ss_preserve_cursors"></a>SQL_COPT_SS_PRESERVE_CURSORS  
 這個屬性可讓您查詢並設定在認可/回復交易時，連接是否要保留資料指標。 此設定為 SQL_PC_ON 或 SQL_PC_OFF。 預設值為 SQL_PC_OFF。 當您呼叫 [SQLEndTran](../../relational-databases/native-client-odbc-api/sqlendtran.md) (或 SQLTransact) 時，此設定會控制驅動程式是否會關閉游標 (s) 。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_PC_OFF|預設值。 使用 **SQLEndTran**認可或回復交易時，會關閉資料指標。|  
|SQL_PC_ON|使用 **SQLEndTran**認可或回復交易時，不會關閉資料指標，但在非同步模式中使用靜態或索引鍵集資料指標時除外。 如果您在資料指標的母體未完成時發出了回復，就會關閉資料指標。|  

<a name="sqlcoptssquotedident"></a>
## <a name="sql_copt_ss_quoted_ident"></a>SQL_COPT_SS_QUOTED_IDENT  
 SQL_COPT_SS_QUOTED_IDENT 允許在連接時送出的 ODBC 和 Transact-SQL 陳述式中使用引號識別碼。 透過提供引號識別碼，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會允許其他無效的物件名稱，例如 "My Table" (識別碼包含空格字元)。 如需詳細資訊，請參閱 SET QUOTED_IDENTIFIER。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_QI_OFF|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接不允許在送出的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用引號識別碼。|  
|SQL_QI_ON|預設值。 連接允許在送出的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用引號識別碼。|  

<a name="sqlcoptsstranslate"></a>
## <a name="sql_copt_ss_translate"></a>SQL_COPT_SS_TRANSLATE  
 SQL_COPT_SS_TRANSLATE 會在交換 MBCS 資料時，讓驅動程式在用戶端與伺服器字碼頁之間轉譯字元。 屬性只會影響儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char**、 **Varchar**和**text**資料行中的資料。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_XL_OFF|此驅動程式不會在用戶端與伺服器之間交換的字元資料中，將字元從某個字碼頁轉譯至另一個字碼頁。|  
|SQL_XL_ON|預設值。 此驅動程式會在用戶端與伺服器之間交換的字元資料中，將字元從某個字碼頁轉譯至另一個字碼頁。 此驅動程式會自動設定字元轉譯，並判斷伺服器所安裝的字碼頁以及用戶端使用中的字碼頁。|  

<a name="sqlcoptsstrustservercertificate"></a>
## <a name="sql_copt_ss_trust_server_certificate"></a>SQL_COPT_SS_TRUST_SERVER_CERTIFICATE  
 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE 會在使用加密時，讓驅動程式啟用或停用憑證驗證。 雖然此屬性是讀取/寫入值，但是在建立連接之後設定此屬性沒有任何作用。  
  
 用戶端應用程式可以在開啟連接之後查詢此屬性，以便判斷使用中的實際加密和驗證設定。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_TRUST_SERVER_CERTIFICATE_NO|預設值。 不啟用沒有憑證驗證的加密。|  
|SQL_TRUST_SERVER_CERTIFICATE_YES|啟用沒有憑證驗證的加密。|  

<a name="sqlcoptsstxnisolation"></a>
## <a name="sql_copt_ss_txn_isolation"></a>SQL_COPT_SS_TXN_ISOLATION  
 SQL_COPT_SS_TXN_ISOLATION 會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特有的快照集隔離屬性。 您無法使用 SQL_ATTR_TXN_ISOLATION 來設定快照集隔離，因為此值是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特有的。 不過，您可以使用 SQL_ATTR_TXN_ISOLATION 或 SQL_COPT_SS_TXN_ISOLATION 來擷取此值。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_TXN_SS_SNAPSHOT|表示您無法從某個交易看到在其他交易中所產生的變更，而且即使重新查詢，您也無法看見變更。|  
  
 如需快照集隔離的詳細資訊，請參閱 [使用快照集隔離](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)。  
  
## <a name="sql_copt_ss_use_proc_for_prep"></a>SQL_COPT_SS_USE_PROC_FOR_PREP

 已不再支援這個屬性。  

<a name="sqlcoptssuserdata"></a>
## <a name="sql_copt_ss_user_data"></a>SQL_COPT_SS_USER_DATA  
 SQL_COPT_SS_USER_DATA 會設定使用者資料指標。 使用者資料是針對每個連接記錄在用戶端擁有的記憶體中。  
  
 如需詳細資訊，請參閱 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)。  

<a name="sqlcoptsswarnoncperror"></a>
## <a name="sql_copt_ss_warn_on_cp_error"></a>SQL_COPT_SS_WARN_ON_CP_ERROR  
 這個屬性會決定如果字碼頁轉換期間發生資料遺失，您是否將收到警告。 這個屬性僅適用於來自伺服器的資料。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_WARN_YES|在字碼頁轉換期間發生資料遺失時產生警告。|  
|SQL_WARN_NO|(預設值) 在字碼頁轉換期間發生資料遺失時不產生警告。|  
  
## <a name="sqlsetconnectattr-support-for-service-principal-names-spns"></a>服務主要名稱 (SPN) 的 SQLSetConnectAttr 支援

 SQLSetConnectAttr 可以用來設定新的連接屬性值 SQL_COPT_SS_SERVER_SPN 和 SQL_COPT_SS_FAILOVER_PARTNER_SPN。 這些屬性無法在連接已開啟時設定。如果您嘗試在連接已開啟時設定這些屬性，就會傳回錯誤 HY011 並顯示「此時作業無效」訊息  (的 SQLSetConnectOption 也可以用來設定這些值。 )   
  
 如需 Spn 的詳細資訊，請參閱 [&#40;ODBC&#41;之用戶端連接中的服務主體名稱 &#40;spn&#41; ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。  

<a name="sqlcoptssconnectiondead"></a>
## <a name="sql_copt_ss_connection_dead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 這是唯讀的屬性。  
  
 如需 SQL_COPT_SS_CONNECTION_DEAD 的詳細資訊，請參閱 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) 和 [連接至資料來源 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md)。  
  
## <a name="example"></a>範例

 這則範例會記錄效能資料。  
  
```  
SQLPERF*     pSQLPERF;  
SQLINTEGER   nValue;  
  
// See if you are already logging. SQLPERF* will be NULL if not.  
SQLGetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA, &pSQLPERF,  
    sizeof(SQLPERF*), &nValue);  
  
if (pSQLPERF == NULL)  
    {  
    // Set the performance log file name.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG,  
        (SQLPOINTER) "\\My LogDirectory\\MyServerLog.txt", SQL_NTS);  
  
    // Start logging...  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
        (SQLPOINTER) SQL_PERF_START, SQL_IS_INTEGER);  
    }  
else  
    {  
    // Take a snapshot now so that your performance statistics are discernible.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
    }  
  
    // ...perform some action...  
  
// ...take a performance data snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
    // ...perform more actions...  
  
// ...take another snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
// ...and disable logging.  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
    (SQLPOINTER) SQL_PERF_STOP, SQL_IS_INTEGER);  
  
// Continue on...  
```  
  
## <a name="see-also"></a>另請參閱

 [SQLSetConnectAttr 函式](../../odbc/reference/syntax/sqlsetconnectattr-function.md)   
 [ODBC API 的執行詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SQLPrepare 函式](../../odbc/reference/syntax/sqlprepare-function.md)   
 [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md)  
  
