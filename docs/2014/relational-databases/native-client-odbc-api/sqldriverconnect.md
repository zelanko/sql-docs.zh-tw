---
title: SQLDriverConnect |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
caps.latest.revision: 60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a9a7ab39d15b32a093cf7a9924645f2ad81f97e4
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426757"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會定義可取代或增強連接字串關鍵字的連接屬性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式已經指定數個連接字串關鍵字的預設值。  
  
 如需提供的關鍵字的清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式，請參閱[搭配 SQL Server Native Client 使用連接字串關鍵字](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 如需詳細資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接屬性與驅動程式預設行為，請參閱[SQLSetConnectAttr](sqlsetconnectattr.md)。  
  
 如需有效的連接字串關鍵字的討論[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端，請參閱[搭配 SQL Server Native Client 使用連接字串關鍵字](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 當`SQLDriverConnect` *DriverCompletion*參數值為 SQL_DRIVER_PROMPT、 SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會擷取關鍵字值顯示的對話方塊。 如果在連接字串中傳遞關鍵字值，而且使用者沒有在對話方塊中變更關鍵字的值，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會使用連接字串中的值。 如果沒有在連接字串中設定值，而且使用者沒有在對話方塊中進行指派，驅動程式會使用預設值。  
  
 `SQLDriverConnect` 必須指定有效*WindowHandle*任何時*DriverCompletion*值需要 （或可能需要） 的驅動程式的 [連線] 對話方塊中顯示。 無效的控制代碼會傳回 SQL_ERROR。  
  
 指定 DRIVER 或 DSN 關鍵字。 ODBC 敘述如果同時指定兩個關鍵字，驅動程式會使用最左邊的關鍵字，並忽略另一個關鍵字。 如果指定，則驅動程式，或最左邊的兩個，而`SQLDriverConnect` *DriverCompletion*參數值為 SQL_DRIVER_NOPROMPT 的 SERVER 關鍵字和適當的值所需。  
  
 指定 SQL_DRIVER_NOPROMPT 時，使用者驗證關鍵字與值必須同時存在。 驅動程式會確認字串 "Trusted_Connection=yes" 存在，或 UID 和 PWD 關鍵字同時存在。  
  
 如果*DriverCompletion*參數值為 SQL_DRIVER_NOPROMPT 或 SQL_DRIVER_COMPLETE_REQUIRED，而語言或資料庫來自連接字串，且其中一個無效，`SQLDriverConnect`會傳回 SQL_ERROR。  
  
 如果*DriverCompletion*參數值為 SQL_DRIVER_NOPROMPT 或 SQL_DRIVER_COMPLETE_REQUIRED，而語言或資料庫來自 ODBC 資料來源定義，且其中一個無效，`SQLDriverConnect`會使用預設值語言或資料庫指定的使用者識別碼並傳回 SQL_SUCCESS_WITH_INFO。  
  
 如果*DriverCompletion*參數值為 SQL_DRIVER_COMPLETE 或 SQL_DRIVER_PROMPT，而且如果語言或資料庫無效，`SQLDriverConnect`會重新顯示對話方塊。  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>高可用性/災害復原的 SQLDriverConnect 支援  
 如需使用詳細資訊`SQLDriverConnect`連接到[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]叢集，請參閱[SQL Server Native Client Support for High Availability，Disaster Recovery](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>服務主要名稱 (SPN) 的 SQLDriverConnect 支援  
 SQLDDriverConnect 會使用啟用對話方塊 boxwhen 提示時，ODBC 登入。 如此可允許同時針對主體伺服器和它的容錯移轉夥伴來輸入 SPN。  
  
 SQLDriverConnect 會接受新的連接字串關鍵字`ServerSPN`和`FailoverPartnerSPN`，而且將會識別新的連接屬性 SQL_COPT_SS_SERVER_SPN 和 SQL_COPT_SS_FAILOVER_PARTNER_SPN。  
  
 當指定連接屬性值一次以上時，以程式設計方式設定的值會優先於 DSN 中的值與連接字串中的值。 DSN 中的值優先於連接字串中的值。  
  
 開啟連接時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 會將 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 設定為開啟連接所使用的驗證方法。  
  
 如需有關 Spn 的詳細資訊，請參閱 <<c0> [ 服務主體名稱&#40;Spn&#41;用戶端連接中&#40;ODBC&#41;](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。</c0>  
  
## <a name="examples"></a>範例  
 下列呼叫說明最少的所需的資料`SQLDriverConnect`:  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 下列連接字串說明最小所需的資料時*DriverCompletion*參數值為 SQL_DRIVER_NOPROMPT:  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLDriverConnect 函數](http://go.microsoft.com/fwlink/?LinkId=59340)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)  
  
  
