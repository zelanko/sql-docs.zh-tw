---
title: 用戶端連接 (ODBC) 中的服務主體名稱 (Spn) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 1d60cb30-4c46-49b2-89ab-701e77a330a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f45e6124dbbad79802e290f935ccc6f3f45cee0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63144400"
---
# <a name="service-principal-names-spns-in-client-connections-odbc"></a>用戶端連接 (ODBC) 中的服務主要名稱 (SPN)
  本主題描述可在用戶端應用程式內支援服務主要名稱 (SPN) 的 ODBC 屬性和函數。 用戶端應用程式 Spn 的相關資訊，請參閱[服務主體名稱&#40;SPN&#41;用戶端連接中的支援](../features/service-principal-name-spn-support-in-client-connections.md)並[取得 Kerberos 相互驗證](../../native-client-odbc-how-to/get-mutual-kerberos-authentication.md)。  
  
## <a name="connection-string-keywords"></a>連接字串關鍵字  
 下列連接字串關鍵字可讓用戶端應用程式指定 SPN。  
  
|關鍵字|值|  
|-------------|-----------|  
|`ServerSPN`|伺服器的 SPN。 預設值為空字串，它可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用驅動程式產生的預設 SPN。|  
|`FailoverPartnerSPN`|容錯移轉夥伴的 SPN。 預設值為空字串，它可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用驅動程式產生的預設 SPN。|  
  
## <a name="connection-attributes"></a>連接屬性  
 下列連接屬性可讓用戶端應用程式指定 SPN，並查詢是否有驗證方法。  
  
|名稱|類型|使用量|  
|----------|----------|-----------|  
|SQL_COPT_SS_SERVER_SPN<br /><br /> SQL_COPT_SS_FAILOVER_PARTNER_SPN|SQLTCHAR，讀取/寫入|指定伺服器的 SPN。 預設值為空字串，它可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用驅動程式產生的預設 SPN。<br /><br /> 只有當已經以程式設計方式設定這個屬性之後，或是在已經開啟連接之後，才可以查詢這個屬性。 如果嘗試在尚未開啟的連接上查詢這個屬性，而且尚未以程式設計方式設定此屬性，就會傳回 SQL_ERROR，而且會將診斷記錄記錄下來，其中包含 SQLState 08003 和「未開啟連接」訊息。<br /><br /> 如果嘗試在已開啟連接時設定這個屬性，就會傳回 SQL_ERROR，而且會將診斷記錄記錄下來，其中包含 SQLState HY011 和「此時作業無效」訊息。|  
|SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD|SQLTCHAR，唯讀|傳回連接所使用的驗證方法。 傳給應用程式的值就是 Windows 傳給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的值。 可能的值為：<br /><br /> -"NTLM"，使用 NTLM 驗證開啟連接時傳回。<br />-"Kerberos"，當使用 Kerberos 驗證開啟連接時傳回。<br /><br /> 只能針對使用 Windows 驗證的開啟連接來讀取這個屬性。 如果嘗試在開啟連接之前讀取這個屬性，就會傳回 SQL_ERROR，而且會將錯誤記錄下來，其中包含 SQLState 08003 和「未開啟連接」訊息。<br /><br /> 如果在尚未使用 Windows 驗證的連接上查詢這個屬性，就會傳回 SQL_ERROR，而且會將錯誤記錄下來，其中包含 SQLState HY092 和「屬性/選項識別碼無效 (SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 只適用於信任連接)」訊息。<br /><br /> 如果無法判斷驗證方法，就會傳回 SQL_ERROR，而且會將錯誤記錄下來，其中包含 SQLState HY000 和「一般錯誤」訊息。|  
|SQL_COPT_SS_MUTUALLY_AUTHENTICATED|SQLSMALLINT，唯讀|如果連接中的伺服器已互相驗證過，則會傳回 SQL_TRUE，否則會傳回 SQL_FALSE。<br /><br /> 只能針對開啟的連接來讀取這個屬性。 如果嘗試在開啟連接之前讀取這個屬性，就會傳回 SQL_ERROR，而且會將錯誤記錄下來，其中包含 SQLState 08003 和「未開啟連接」訊息。<br /><br /> 如果針對未使用 Windows 驗證的連接來查詢這個屬性，就會傳回 SQL_FALSE。|  
  
## <a name="odbc-function-support-for-specifying-spns"></a>用來指定 SPN 的 ODBC 函數支援  
 下列 ODBC 函數可支援用戶端應用程式和 SPN：  
  
-   [SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md)  
  
-   [SQLConnect](../../native-client-odbc-api/sqlconnect.md)  
  
-   [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md)  
  
-   [SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md)  
  
-   [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
