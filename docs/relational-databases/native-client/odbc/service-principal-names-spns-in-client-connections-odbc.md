---
title: 用戶端連接 (ODBC) 中的服務主體名稱 (Spn) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1d60cb30-4c46-49b2-89ab-701e77a330a2
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 73d8cb7b88513173d9342d3910e1f2c959d1c42e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32951013"
---
# <a name="service-principal-names-spns-in-client-connections-odbc"></a>用戶端連接 (ODBC) 中的服務主要名稱 (SPN)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主題描述可在用戶端應用程式內支援服務主要名稱 (SPN) 的 ODBC 屬性和函數。 如需有關 Spn 的用戶端應用程式，請參閱[服務主要名稱 & #40;SPN & #41;在用戶端連接中的支援](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)和[取得相互 Kerberos 驗證](../../../relational-databases/native-client-odbc-how-to/get-mutual-kerberos-authentication.md)。  
  
## <a name="connection-string-keywords"></a>連接字串關鍵字  
 下列連接字串關鍵字可讓用戶端應用程式指定 SPN。  
  
|關鍵字|Value|  
|-------------|-----------|  
|**ServerSPN**|伺服器的 SPN。 預設值為空字串，它可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用驅動程式產生的預設 SPN。|  
|**FailoverPartnerSPN**|容錯移轉夥伴的 SPN。 預設值為空字串，它可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用驅動程式產生的預設 SPN。|  
  
## <a name="connection-attributes"></a>連接屬性  
 下列連接屬性可讓用戶端應用程式指定 SPN，並查詢是否有驗證方法。  
  
|名稱|型別|使用方式|  
|----------|----------|-----------|  
|SQL_COPT_SS_SERVER_SPN<br /><br /> SQL_COPT_SS_FAILOVER_PARTNER_SPN|SQLTCHAR，讀取/寫入|指定伺服器的 SPN。 預設值為空字串，它可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用驅動程式產生的預設 SPN。<br /><br /> 只有當已經以程式設計方式設定這個屬性之後，或是在已經開啟連接之後，才可以查詢這個屬性。 如果嘗試在尚未開啟的連接上查詢這個屬性，而且尚未以程式設計方式設定此屬性，就會傳回 SQL_ERROR，而且會將診斷記錄記錄下來，其中包含 SQLState 08003 和「未開啟連接」訊息。<br /><br /> 如果嘗試在已開啟連接時設定這個屬性，就會傳回 SQL_ERROR，而且會將診斷記錄記錄下來，其中包含 SQLState HY011 和「此時作業無效」訊息。|  
|SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD|SQLTCHAR，唯讀|傳回連接所使用的驗證方法。 傳給應用程式的值就是 Windows 傳給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的值。 可能的值為：<br /><br /> "NTLM"，當使用 NTLM 驗證開啟連接時所傳回。<br /><br /> "Kerberos"，當使用 Kerberos 驗證開啟連接時所傳回。<br /><br /> <br /><br /> 只能針對使用 Windows 驗證的開啟連接來讀取這個屬性。 如果嘗試在開啟連接之前讀取這個屬性，就會傳回 SQL_ERROR，而且會將錯誤記錄下來，其中包含 SQLState 08003 和「未開啟連接」訊息。<br /><br /> 如果在尚未使用 Windows 驗證的連接上查詢這個屬性，就會傳回 SQL_ERROR，而且會將錯誤記錄下來，其中包含 SQLState HY092 和「屬性/選項識別碼無效 (SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 只適用於信任連接)」訊息。<br /><br /> 如果無法判斷驗證方法，就會傳回 SQL_ERROR，而且會將錯誤記錄下來，其中包含 SQLState HY000 和「一般錯誤」訊息。|  
|SQL_COPT_SS_MUTUALLY_AUTHENTICATED|SQLSMALLINT，唯讀|如果連接中的伺服器已互相驗證過，則會傳回 SQL_TRUE，否則會傳回 SQL_FALSE。<br /><br /> 只能針對開啟的連接來讀取這個屬性。 如果嘗試在開啟連接之前讀取這個屬性，就會傳回 SQL_ERROR，而且會將錯誤記錄下來，其中包含 SQLState 08003 和「未開啟連接」訊息。<br /><br /> 如果針對未使用 Windows 驗證的連接來查詢這個屬性，就會傳回 SQL_FALSE。|  
  
## <a name="odbc-function-support-for-specifying-spns"></a>用來指定 SPN 的 ODBC 函數支援  
 下列 ODBC 函數可支援用戶端應用程式和 SPN：  
  
-   [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
-   [SQLConnect](../../../relational-databases/native-client-odbc-api/sqlconnect.md)  
  
-   [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)  
  
-   [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)  
  
-   [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client & #40; ODBC & #41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
