---
title: Microsoft ODBC Driver 的功能
description: 了解 Windows 版 Microsoft ODBC Driver for SQL Server 支援的各種功能。
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: v-makouz
ms.author: v-daenge
ms.openlocfilehash: 5fc07a171e42338ca76d51d66c04af187cb6beda
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005904"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server on Windows 的功能
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-174-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver 17.4 for SQL Server

ODBC 驅動程式 17.4 包括能夠調整 TCP Keep-Alive 設定。 您可以將值新增至驅動程式或 DSN 登錄機碼來進行修改。 這些機碼位於系統資料來源的 `HKEY_LOCAL_MACHINE\Software\ODBC\`，以及使用者資料來源的 `HKEY_CURRENT_USER\Software\ODBC\` 中。 若是 DSN，必須將值新增至 `...\Software\ODBC\ODBC.INI\<DSN Name>`；若是驅動程式，則新增至 `...\Software\ODBC\ODBCINST.INI\ODBC Driver 17 for SQL Server`。

如需詳細資訊，請參閱 [ODBC 元件的登錄項目](../../../odbc/reference/install/registry-entries-for-odbc-components.md)。

值為 `REG_SZ`，如下所示：

- `KeepAlive` 會藉由傳送 keep-alive 封包，控制 TCP 嘗試驗證閒置連線是否仍完整無缺的頻率。 預設值為 30 秒。

- `KeepAliveInterval` 可決定在收到回應之前，用以分隔 keep-alive 重新傳輸的間隔。 預設值為 1 秒。



## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver 13.1 for SQL Server

ODBC Driver 13.1 for SQL Server 包含舊版 (11) 的所有功能，並且增加對 Always Encrypted 和 Azure Active Directory 驗證的支援，這些是搭配 Microsoft SQL Server 2016 使用的新功能。  
  
一律加密可讓用戶端將用戶端應用程式內的機密資料進行加密，且永遠不會顯示 SQL Server 的加密金鑰。 安裝在用戶端電腦上且啟用一律加密的驅動程式，透過自動將 SQL Server 用戶端應用程式中的機密資料進行加密與解密，進而達成此目的。 驅動程式會先將敏感資料行中的資料進行加密，才會將資料傳遞至 SQL Server，並自動重寫查詢以保留應用程式的語意。 同樣地，驅動程式會以透明的方式，將查詢結果中加密資料庫資料行所儲存的資料進行解密。 如需詳細資訊，請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)。
 
Azure Active Directory 可讓使用者、DBA 和應用程式設計人員透過 Azure Active Directory (Azure AD) 中的身分識別，使用 Azure Active Directory 驗證作為連線到 Microsoft Azure SQL Database 與 Microsoft SQL Server 2016 的機制。 如需詳細資訊，請參閱[搭配 ODBC 驅動程式使用 Azure Active Directory](../using-azure-active-directory.md) 和[使用 Azure Active Directory 驗證連線到 SQL Database 或 Azure Synapse Analytics](/azure/sql-database/sql-database-aad-authentication)。   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver 11 for SQL Server  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含隨附於 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式的所有功能。 如需詳細資訊，請參閱 [SQL Server Native Client 程式設計](../../../relational-databases/native-client/sql-server-native-client-programming.md)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式以 Windows 作業系統中隨附的 ODBC 驅動程式作為基礎。 如需詳細資訊，請參閱 [Windows Data Access Components SDK](/previous-versions/windows/desktop/legacy/aa968814(v=vs.85))。  
  
此版本的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含下列新功能：  
  
### <a name="bcpexe--l-option-for-specifying-a-login-timeout"></a>bcp.exe -l 選項，用於指定登入逾時
 
-l 選項會指定在您嘗試連線到伺服器時，`bcp.exe` 登入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的逾時秒數。 預設登入逾時為 15 秒。 登入逾時必須是介於 0 與 65534 之間的數字。 如果所提供的值不是數值或不在該範圍內，`bcp.exe` 就會產生錯誤訊息。 值為 0 會指定無限逾時。 小於 (約) 10 秒的登入逾時不可靠。  
  
### <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]支援[可感知驅動程式的連線共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。 如需詳細資訊，請參閱 [ODBC Driver for SQL Server 中可感知驅動程式的連接共用](driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)。  
  
### <a name="asynchronous-execution-notification-method"></a>非同步執行 (通知方法)  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]支援[非同步執行 (通知方法)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。 如需使用範例，請參閱[非同步執行 &#40;通知方法&#41; 範例](asynchronous-execution-notification-method-sample.md)。  
  
### <a name="connection-resiliency"></a>連接恢復功能
若要確保應用程式仍然連接到 Microsoft Azure SQL Database，Windows 上的 ODBC 驅動程式可以還原閒置的連接。 如需詳細資訊，請參閱 [Windows ODBC 驅動程式中的連接恢復功能](connection-resiliency-in-the-windows-odbc-driver.md)。  
  
## <a name="behavior-changes"></a>行為變更

在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中，`sqlcmd.exe` 的 `-y0` 選項會在顯示寬度為 0 時，將輸出截斷為 1 MB。
  
從 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 開始，在已指定 `-y0` 的情況下，單一資料行中已沒有可擷取資料量的限制。 `sqlcmd.exe` 現在會串流多達 2 GB 的資料行 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 最大資料類型)。  
  
另一項差異是，同時指定 `-h` 和 `-y0` 現在會產生選項不相容的錯誤報告。 `-h` 會指定要在欄位標題間列印的資料列數目，且從不與 `-y0` 相容，該項目雖然不會列印標題，但是遭到忽略。
  
請注意，依照傳回的資料大小，`-y0` 可能導致伺服器和網路都發生效能問題。

## <a name="see-also"></a>另請參閱  
[Windows 上的 Microsoft ODBC Driver for SQL Server](microsoft-odbc-driver-for-sql-server-on-windows.md)  
