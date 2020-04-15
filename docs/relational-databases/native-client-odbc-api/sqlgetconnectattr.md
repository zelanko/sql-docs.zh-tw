---
title: SQLGetConnectAttr |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetConnectAttr function
ms.assetid: 26e4e69a-44fd-45e3-b47a-ae39184f041b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 590d47d65ab3893dbc9eefc3facd224671668378
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302142"
---
# <a name="sqlgetconnectattr"></a>SQLGetConnectAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會定義驅動程式特有的連接屬性。 某些屬性可用於**SQLGetConnectAttr,** 該函數用於報告其當前設置。 在建立連接或使用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)設置屬性之前,不會保證為這些屬性報告的值。  
  
 本主題將列出唯讀屬性。 有關其他[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 ODBC 特定於驅動程式的連線屬性的資訊,請參閱[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
## <a name="sql_copt_ss_connection_dead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 SQL_COPT_SS_CONNECTION_DEAD 屬性會將連接的狀態報告給伺服器。 此驅動程式會查詢網路，以得知目前連接狀態。  
  
> [!NOTE]  
>  標準 ODBC 連接屬性 SQL_ATTR_CONNECTION_DEAD 會傳回最新的連接狀態。 這可能不是目前的連接狀態。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_CD_TRUE|已經遺失與伺服器的連接。|  
|SQL_CD_FALSE|連接已開啟，而且可用來處理陳述式。|  
  
## <a name="sql_copt_ss_client_connection_id"></a>SQL_COPT_SS_CLIENT_CONNECTION_ID  
 SQL_COPT_SS_CLIENT_CONNECTION_ID 屬性擷取用戶端連接識別碼，然後可使用此識別碼尋找：  
  
-   啟用之 XEvents 記錄檔中的診斷資訊。  
  
-   連接信號緩衝區中的連接錯誤資訊。  
  
-   啟用之資料存取追蹤記錄檔中的診斷資訊。  
  
 有關詳細資訊,請參閱[在擴展事件紀錄中存取診斷資訊](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_ERROR|連接失敗。|  
|SQL_SUCCESS|此連接已成功。 輸出緩衝區中將可以找到用戶端連接識別碼。|  
  
## <a name="sql_copt_ss_perf_data"></a>SQL_COPT_SS_PERF_DATA  
 SQL_COPT_SS_PERF_DATA 屬性會傳回 SQLPERF 結構的指標，其中包含目前的驅動程式效能統計資料。 如果未啟用性能日誌記錄 **,SQLGetConnectAttr**將返回 NULL。 此驅動程式不會動態更新 SQLPERF 結構中的統計資料。 每次需要刷新性能統計資訊時,都會調用**SQLGetConnect Attr。**  
  
|值|描述|  
|-----------|-----------------|  
|NULL|未啟用效能記錄。|  
|任何其他值|SQLPERF 結構的指標。|  
  
## <a name="sql_copt_ss_perf_query"></a>SQL_COPT_SS_PERF_QUERY  
 如果啟用了長時間執行之查詢的記錄，SQL_COPT_SS_PERF_QUERY 屬性會傳回 TRUE。 如果查詢記錄不在使用中，要求會傳回 FALSE。  
  
## <a name="sql_copt_ss_user_data"></a>SQL_COPT_SS_USER_DATA  
 SQL_COPT_SS_USER_DATA 屬性會擷取使用者-資料指標。 使用者資料會儲存在用戶端擁有的記憶體中，而且針對每個連接記錄下來。 如果尚未設定使用者-資料指標，便會傳回 SQL_UD_NOTSET (一種 NULL 指標)。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_UD_NOTSET|不會設定任何使用者-資料指標。|  
|任何其他值|使用者資料的指標。|  
  
## <a name="sqlgetconnectattr-support-for-service-principal-names-spns"></a>服務主要名稱 (SPN) 的 SQLGetConnectAttr 支援  
 SQLGetConnectAttr 可用於查詢新連接屬性的值,SQL_COPT_SS_SERVER_SPN、SQL_COPT_SS_FAILOVER_PARTNER_SPN、SQL_COPT_SS_MUTUALLY_AUTHENTICATED和SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD。 (SQLGetConnectOption 還可用於查詢這些值。  
  
 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 只供使用 Windows 驗證的已開啟連接使用。  
  
 如果尚未設定 SQL_COPT_SS_SERVER_SPN 或 SQL_COPT_SS_FAILOVER_PARTNER，就會傳回預設值 (空字串)。  
  
 有關 SPN 的詳細資訊,請參閱[用戶端連接中&#40;ODBC&#41;中的服務主體名稱&#40;SPN&#41;。](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetConnectAttr 函數](https://go.microsoft.com/fwlink/?LinkId=59347)   
 [ODBC API 進行詳細資訊](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [&#40;转算-SQL&#41;QUOTED_IDENTIFIER设置](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [&#40;交易-SQL&#41;ANSI_NULLS设置](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [set ANSI_PADDING&#40;轉算-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
