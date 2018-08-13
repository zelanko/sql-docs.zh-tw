---
title: SQLGetConnectAttr |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetConnectAttr function
ms.assetid: 26e4e69a-44fd-45e3-b47a-ae39184f041b
caps.latest.revision: 60
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: cd3f37e0f71824c5a9eab9d53f8bb54d2f3105f1
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39536948"
---
# <a name="sqlgetconnectattr"></a>SQLGetConnectAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會定義驅動程式特有的連接屬性。 有些屬性可供**SQLGetConnectAttr**，而函數用來報告其目前的設定。 針對這些屬性並不保證直到已連線或已設定屬性使用之後，報告的值[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
 本主題將列出唯讀屬性。 如需其他資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式特有的連接屬性，請參閱[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
## <a name="sqlcoptssconnectiondead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 SQL_COPT_SS_CONNECTION_DEAD 屬性會將連接的狀態報告給伺服器。 此驅動程式會查詢網路，以得知目前連接狀態。  
  
> [!NOTE]  
>  標準 ODBC 連接屬性 SQL_ATTR_CONNECTION_DEAD 會傳回最新的連接狀態。 這可能不是目前的連接狀態。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_CD_TRUE|已經遺失與伺服器的連接。|  
|SQL_CD_FALSE|連接已開啟，而且可用來處理陳述式。|  
  
## <a name="sqlcoptssclientconnectionid"></a>SQL_COPT_SS_CLIENT_CONNECTION_ID  
 SQL_COPT_SS_CLIENT_CONNECTION_ID 屬性擷取用戶端連接識別碼，然後可使用此識別碼尋找：  
  
-   啟用之 XEvents 記錄檔中的診斷資訊。  
  
-   連接信號緩衝區中的連接錯誤資訊。  
  
-   啟用之資料存取追蹤記錄檔中的診斷資訊。  
  
 如需詳細資訊，請參閱 <<c0> [ 擴充事件記錄檔中存取診斷資訊](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_ERROR|連接失敗。|  
|SQL_SUCCESS|此連接已成功。 輸出緩衝區中將可以找到用戶端連接識別碼。|  
  
## <a name="sqlcoptssperfdata"></a>SQL_COPT_SS_PERF_DATA  
 SQL_COPT_SS_PERF_DATA 屬性會傳回 SQLPERF 結構的指標，其中包含目前的驅動程式效能統計資料。 **SQLGetConnectAttr**時不會啟用效能記錄，將會傳回 NULL。 此驅動程式不會動態更新 SQLPERF 結構中的統計資料。 呼叫**SQLGetConnectAttr**每當效能統計資料需要重新整理。  
  
|值|描述|  
|-----------|-----------------|  
|NULL|未啟用效能記錄。|  
|任何其他值|SQLPERF 結構的指標。|  
  
## <a name="sqlcoptssperfquery"></a>SQL_COPT_SS_PERF_QUERY  
 如果啟用了長時間執行之查詢的記錄，SQL_COPT_SS_PERF_QUERY 屬性會傳回 TRUE。 如果查詢記錄不在使用中，要求會傳回 FALSE。  
  
## <a name="sqlcoptssuserdata"></a>SQL_COPT_SS_USER_DATA  
 SQL_COPT_SS_USER_DATA 屬性會擷取使用者-資料指標。 使用者資料會儲存在用戶端擁有的記憶體中，而且針對每個連接記錄下來。 如果尚未設定使用者-資料指標，便會傳回 SQL_UD_NOTSET (一種 NULL 指標)。  
  
|值|描述|  
|-----------|-----------------|  
|SQL_UD_NOTSET|不會設定任何使用者-資料指標。|  
|任何其他值|使用者資料的指標。|  
  
## <a name="sqlgetconnectattr-support-for-service-principal-names-spns"></a>服務主要名稱 (SPN) 的 SQLGetConnectAttr 支援  
 SQLGetConnectAttr 可用來查詢新的連接屬性 SQL_COPT_SS_SERVER_SPN、 SQL_COPT_SS_FAILOVER_PARTNER_SPN、 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 的值。 （SQLGetConnectOption 也可用來查詢這些值。）  
  
 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 只供使用 Windows 驗證的已開啟連接使用。  
  
 如果尚未設定 SQL_COPT_SS_SERVER_SPN 或 SQL_COPT_SS_FAILOVER_PARTNER，就會傳回預設值 (空字串)。  
  
 如需有關 Spn 的詳細資訊，請參閱 <<c0> [ 服務主體名稱&#40;Spn&#41;用戶端連接中&#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetConnectAttr 函數](http://go.microsoft.com/fwlink/?LinkId=59347)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
