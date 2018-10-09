---
title: ODBC Driver for SQL Server 中可感知驅動程式的連線共用 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 455ab165-8e4d-4df9-a1d7-2b532bfd55d6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f8557d34acd3de425f4d6932eca95fbe6e2d334
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784936"
---
# <a name="driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server"></a>ODBC Driver for SQL Server 中可感知驅動程式的連接共用
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]支援[可感知驅動程式的連線共用](http://msdn.microsoft.com/library/hh405031(VS.85).aspx)。 本主題描述 Windows 版 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的「可感知驅動程式的連線共用」有哪些增強功能：  
  
-   無論連線屬性為何，使用 `SQLDriverConnect` 的連線都會進入與使用 `SQLConnect` 的連線不同的個別集區。
- 在使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證和可感知驅動程式的連線共用時，驅動程式並不會使用目前執行緒的 Windows 使用者安全性內容，來區隔集區中的連線。 也就是說，如果連接對於具有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的 Windows 模擬案例使用了相同的參數，並且使用相同的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證認證連接到後端，則不同的 Windows 使用者將可能使用相同的連接集區。 在使用 Windows 驗證和可感知驅動程式的連接共用時，驅動程式會使用目前 Windows 使用者的安全性內容來區隔集區中的連接。 也就是說，在 Windows 模擬案例中，即使連接使用相同的參數，不同的 Windows 使用者也不會共用連接。
- 使用 Azure Active Directory 和可感知驅動程式的連接共用時，驅動程式也使用的驗證值來判斷連接集區中的成員資格。
  
-   可感知驅動程式的連接共用可防止從集區傳回錯誤的連接。  
  
-   可感知驅動程式的連接共用可辨識驅動程式的特定連接屬性。 因此，如果連接使用`SQL_COPT_SS_APPLICATION_INTENT`設為唯讀，該連線會取得自己的連接集區。
-   設定`SQL_COPT_SS_ACCESS_TOKEN`屬性會導致個別的集區的連線 
  
如果在您的連接字串與共用的連接字串之間，有下列其中一個連接屬性識別碼或連接字串關鍵字不相同，驅動程式將會使用共用連接。 不過，如果所有的連接屬性識別碼或連接字串關鍵字皆相符，效能會更好。 (為了符合集區中的連接，驅動程式會重設屬性。) 由於重設下列參數需要額外的網路呼叫，效能因而降低。  
  
-    如果下列連接屬性或連接關鍵字有其中兩個或更多不相同，則不會使用共用連接。  
  
  - `Language`  
  - `QuoteId`  
  - `SQL_ATTR_TXN_ISOLATION` 
  - `SQL_COPT_SS_QUOTED_IDENT`  
  
-   如果在您的連接字串與共用的連接字串之間，有下列任一連接關鍵字不相同，則不會使用共用連接。  
  
    |關鍵字|ODBC Driver 13|ODBC Driver 11|
    |-|-|-|
    |`Address`|是|是|
    |`AnsiNPW`|是|是|
    |`App`|是|是|
    |`ApplicationIntent`|是|是|  
    |`Authentication`|是|否|
    |`ColumnEncryption`|是|否|
    |`Database`|是|是|
    |`Encrypt`|是|是|  
    |`Failover_Partner`|是|是|
    |`FailoverPartnerSPN`|是|是|
    |`MARS_Connection`|是|是|
    |`Network`|是|是|
    |`PWD`|是|是|
    |`Server`|是|是|
    |`ServerSPN`|是|是|
    |`TransparentNetworkIPResolution`|是|是|
    |`Trusted_Connection`|是|是|
    |`TrustServerCertificate`|是|是|
    |`UID`|是|是|
    |`WSID`|是|是|
    
- 如果在您的連接字串與共用的連接字串之間，有下列任一連接屬性不相同，則不會使用共用連接。  
  
    |attribute|ODBC Driver 13|ODBC Driver 11|  
    |-|-|-|  
    |`SQL_ATTR_CURRENT_CATALOG`|是|是|
    |`SQL_ATTR_PACKET_SIZE`|是|是|
    |`SQL_COPT_SS_ANSI_NPW`|是|是|
    |`SQL_COPT_SS_ACCESS_TOKEN`|是|否|
    |`SQL_COPT_SS_AUTHENTICATION`|是|否|
    |`SQL_COPT_SS_ATTACHDBFILENAME`|是|是|
    |`SQL_COPT_SS_BCP`|是|是|
    |`SQL_COPT_SS_COLUMN_ENCRYPTION`|是|否|
    |`SQL_COPT_SS_CONCAT_NULL`|是|是|
    |`SQL_COPT_SS_ENCRYPT`|是|是|
    |`SQL_COPT_SS_FAILOVER_PARTNER`|是|是|
    |`SQL_COPT_SS_FAILOVER_PARTNER_SPN`|是|是|
    |`SQL_COPT_SS_INTEGRATED_SECURITY`|是|是|
    |`SQL_COPT_SS_MARS_ENABLED`|是|是|
    |`SQL_COPT_SS_OLDPWD`|是|是|
    |`SQL_COPT_SS_SERVER_SPN`|是|是|
    |`SQL_COPT_SS_TRUST_SERVER_CERTIFICATE`|是|是|
    |`SSPROP_AUTH_REPL_SERVER_NAME`|是|是|
    |`SQL_COPT_SS_TNIR`|是|否|
 
-   驅動程式可以重設及調整下列連接關鍵字和屬性，而不需要進行額外的網路呼叫。 驅動程式會重設這些參數，以確保連接未包含不正確的資訊。  
  
     當驅動程式管理員在嘗試比對您的連接與集區中的連接時，並不會考量這些連接關鍵字。 (即使您變更其中一個參數，現有的連接仍可重複使用。 驅動程式會視需要重設選項。)這些屬性可以在用戶端重設，而不需要進行額外的網路呼叫。  
  
    |關鍵字|ODBC Driver 13|ODBC Driver 11|  
    |-|-|-|  
    |`AutoTranslate`|是|是|
    |`Description`|是|是|
    |`MultisubnetFailover`|是|是|  
    |`QueryLog_On`|是|是|
    |`QueryLogFile`|是|是|
    |`QueryLogTime`|是|是|
    |`Regional`|是|是|
    |`StatsLog_On`|是|是|
    |`StatsLogFile`|  是|是|
  
     如果您變更下列其中一個連接屬性，現有的連接仍可重複使用。  驅動程式會視需要重設此值。 驅動程式可在用戶端重設這些屬性，而不需要進行額外的網路呼叫。  
  
    |attribute|ODBC Driver 13|ODBC Driver 11|  
    |-|-|-|  
    |所有陳述式屬性|是|是|
    |`SQL_ATTR_AUTOCOMMIT`|是|是|
    |`SQL_ATTR_CONNECTION_TIMEOUT`|  是|是|
    |`SQL_ATTR_DISCONNECT_BEHAVIOR SQL_ATTR_CONNECTION_TIMEOUT`|是|是|
    |`SQL_ATTR_LOGIN_TIMEOUT`|是|是|
    |`SQL_ATTR_ODBC_CURSORS`|  是|是|
    |`SQL_COPT_SS_PERF_DATA`|是|是|
    |`SQL_COPT_SS_PERF_DATA_LOG`|是|是|
    |`SQL_COPT_SS_PERF_DATA_LOG_NOW`| 是|是| 
    |`SQL_COPT_SS_PERF_QUERY`|是|是|
    |`SQL_COPT_SS_PERF_QUERY_INTERVAL`|是|是|
    |`SQL_COPT_SS_PERF_QUERY_LOG`|  是|是|
    |`SQL_COPT_SS_PRESERVE_CURSORS`|是|是|
    |`SQL_COPT_SS_TRANSLATE`|是|是|
    |`SQL_COPT_SS_USER_DATA`|  是|是|
    |`SQL_COPT_SS_WARN_ON_CP_ERROR`|是|是|  
  
## <a name="see-also"></a>另請參閱  
 [Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
