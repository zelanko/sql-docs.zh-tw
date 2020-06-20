---
title: SQLDriverConnect |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: rothja
ms.author: jroth
ms.openlocfilehash: 40691dfb381883b59155607fb56f4933820e3e44
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022635"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會定義可取代或增強連接字串關鍵字的連接屬性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式已經指定數個連接字串關鍵字的預設值。  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式中可用的關鍵字清單，請參閱搭配[使用連接字串關鍵字與 SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接屬性和驅動程式預設行為的詳細資訊，請參閱[SQLSetConnectAttr](sqlsetconnectattr.md)。  
  
 如需對 Native Client 有效之連接字串關鍵字的討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱搭配[使用連接字串關鍵字與 SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 當 `SQLDriverConnect` *DriverCompletion*參數值 SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會從顯示的對話方塊中抓取關鍵字值。 如果在連接字串中傳遞關鍵字值，而且使用者沒有在對話方塊中變更關鍵字的值，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會使用連接字串中的值。 如果沒有在連接字串中設定值，而且使用者沒有在對話方塊中進行指派，驅動程式會使用預設值。  
  
 `SQLDriverConnect`當有任何*DriverCompletion*值需要（或可能需要） [驅動程式連接] 對話方塊的顯示時，必須提供有效的*WindowHandle* 。 無效的控制代碼會傳回 SQL_ERROR。  
  
 指定 DRIVER 或 DSN 關鍵字。 ODBC 敘述如果同時指定兩個關鍵字，驅動程式會使用最左邊的關鍵字，並忽略另一個關鍵字。 如果已指定 DRIVER，或為兩者的最左邊，而且 `SQLDriverConnect` *DriverCompletion*參數值為 SQL_DRIVER_NOPROMPT，則需要 SERVER 關鍵字和適當的值。  
  
 指定 SQL_DRIVER_NOPROMPT 時，使用者驗證關鍵字與值必須同時存在。 驅動程式會確認字串 "Trusted_Connection=yes" 存在，或 UID 和 PWD 關鍵字同時存在。  
  
 如果*DriverCompletion*參數值為 SQL_DRIVER_NOPROMPT 或 SQL_DRIVER_COMPLETE_REQUIRED，而語言或資料庫來自連接字串，且其中一個無效，則會傳回 `SQLDriverConnect` SQL_ERROR。  
  
 如果*DriverCompletion*參數值 SQL_DRIVER_NOPROMPT 或 SQL_DRIVER_COMPLETE_REQUIRED，而語言或資料庫來自 ODBC 資料來源定義，而且兩者都無效，則會 `SQLDriverConnect` 針對指定的使用者識別碼使用預設的語言或資料庫，並傳回 SQL_SUCCESS_WITH_INFO。  
  
 如果*DriverCompletion*參數值為 SQL_DRIVER_COMPLETE 或 SQL_DRIVER_PROMPT，而語言或資料庫無效，則會重新引發 `SQLDriverConnect` 對話方塊。  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>高可用性/災害復原的 SQLDriverConnect 支援  
 如需使用連線到叢集的詳細資訊 `SQLDriverConnect` [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ，請參閱[高可用性和嚴重損壞修復 SQL Server Native Client 支援](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>服務主要名稱 (SPN) 的 SQLDriverConnect 支援  
 SQLDDriverConnect 將會使用 [ODBC 登入] 對話方塊 boxwhen 提示已啟用。 如此可允許同時針對主體伺服器和它的容錯移轉夥伴來輸入 SPN。  
  
 SQLDriverConnect 將會接受新的連接字串關鍵字 `ServerSPN` 和 `FailoverPartnerSPN` ，並將會辨識新的連接屬性 SQL_COPT_SS_SERVER_SPN 和 SQL_COPT_SS_FAILOVER_PARTNER_SPN。  
  
 當指定連接屬性值一次以上時，以程式設計方式設定的值會優先於 DSN 中的值與連接字串中的值。 DSN 中的值優先於連接字串中的值。  
  
 開啟連接時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 會將 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 設定為開啟連接所使用的驗證方法。  
  
 如需 Spn 的詳細資訊，請參閱[&#40;ODBC&#41;的用戶端連接中 &#40;spn&#41; 的服務主體名稱](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。  
  
## <a name="examples"></a>範例  
 下列呼叫說明所需的最少量資料量 `SQLDriverConnect` ：  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 下列連接字串說明 SQL_DRIVER_NOPROMPT *DriverCompletion*參數值時所需的最小資料：  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLDriverConnect 函式](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [ODBC API 的執行詳細資料](odbc-api-implementation-details.md)   
 [設定 ANSI_NullS &#40;Transact-sql&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [設定 ANSI_PADDING &#40;Transact-sql&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)  
  
  
