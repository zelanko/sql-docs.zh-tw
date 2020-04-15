---
title: SQLDriver連接 |微軟文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d1455f0b91313ea137ec9c13a2d318fba0807b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302544"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會定義可取代或增強連接字串關鍵字的連接屬性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式已經指定數個連接字串關鍵字的預設值。  
  
 關於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]這個機客戶端 ODBC 驅動程式中可用的關鍵字列表,請參閱[使用與 SQL Server 本機客戶端的連接字串關鍵字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連線屬性和驅動程式預設行為的詳細資訊,請參閱[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
 有關對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端有效的連接字串關鍵字的討論,請參閱[使用與 SQL Server 本機客戶端的連接字串關鍵字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 當**SQLDriverConnect**_驅動程式完成_參數值SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或SQL_DRIVER_COMPLETE_REQUIRED時, 本機用戶端 ODBC 驅動程式將從顯示的對話框中檢索關鍵字值。 如果在連接字串中傳遞關鍵字值，而且使用者沒有在對話方塊中變更關鍵字的值，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會使用連接字串中的值。 如果沒有在連接字串中設定值，而且使用者沒有在對話方塊中進行指派，驅動程式會使用預設值。  
  
 當任何*驅動程式完成*值需要(或可能需要)顯示驅動程式的連接對話方塊時,必須為**SQLDriverConnect**提供有效的*WindowHandle。* 無效的控制代碼會傳回 SQL_ERROR。  
  
 指定 DRIVER 或 DSN 關鍵字。 ODBC 敘述如果同時指定兩個關鍵字，驅動程式會使用最左邊的關鍵字，並忽略另一個關鍵字。 如果指定了 DRIVER,或者是兩個中最左側的,並且**SQLDriverConnect**_驅動程式完成_參數值SQL_DRIVER_NOPROMPT,則需要 SERVER 關鍵字和適當的值。  
  
 指定 SQL_DRIVER_NOPROMPT 時，使用者驗證關鍵字與值必須同時存在。 驅動程式會確認字串 "Trusted_Connection=yes" 存在，或 UID 和 PWD 關鍵字同時存在。  
  
 如果*Driver 完成*參數值SQL_DRIVER_NOPROMPT或SQL_DRIVER_COMPLETE_REQUIRED,並且語言或資料庫來自連接字串,並且其中一個無效,**則 SQLDriverConnect**返回SQL_ERROR。  
  
 如果*Driver 完成*參數值SQL_DRIVER_NOPROMPT或SQL_DRIVER_COMPLETE_REQUIRED,並且語言或資料庫來自 ODBC 資料來源定義,並且無效 **,SQLDriverConnect**使用預設語言或資料庫進行指定的使用者 ID 並返回SQL_SUCCESS_WITH_INFO。  
  
 如果*驅動程式完成*參數值為SQL_DRIVER_COMPLETE或SQL_DRIVER_PROMPT,並且語言或資料庫無效 **,SQLDriverConnect**將重新顯示該對話方塊。  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>高可用性/災害復原的 SQLDriverConnect 支援  
 有關使用**SQLDriverConnect**[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]連線到叢集的詳細資訊,請參考 SQL [Server 本機客戶端支援以進行高可用性、災難恢復](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>服務主要名稱 (SPN) 的 SQLDriverConnect 支援  
 啟用提示時,SQLDDriverConnect 將使用 ODBC 登錄對話方塊。 如此可允許同時針對主體伺服器和它的容錯移轉夥伴來輸入 SPN。  
  
 SQLDriverConnect 將接受新的連接字串關鍵字**ServerSPN**和**故障轉移合作夥伴SPN,** 並將SQL_COPT_SS_SERVER_SPN和SQL_COPT_SS_FAILOVER_PARTNER_SPN辨識新的連接屬性。  
  
 當指定連接屬性值一次以上時，以程式設計方式設定的值會優先於 DSN 中的值與連接字串中的值。 DSN 中的值優先於連接字串中的值。  
  
 開啟連接時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 會將 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 設定為開啟連接所使用的驗證方法。  
  
 有關 SPN 的詳細資訊,請參閱[用戶端連接中&#40;ODBC&#41;中的服務主體名稱&#40;SPN&#41;。](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
## <a name="examples"></a>範例  
 以下調用說明**SQLDriverConnect**所需的最少資料量:  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 當*驅動程式完成*參數值SQL_DRIVER_NOPROMPT時,以下連接字串說明瞭所需的最小資料:  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLDriver 連接功能](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [ODBC API 進行詳細資訊](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [&#40;交易-SQL&#41;ANSI_NULLS设置](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [set ANSI_PADDING&#40;轉算-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
