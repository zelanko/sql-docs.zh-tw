---
title: Windows 上 Microsoft ODBC Driver for SQL Server 的功能 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: v-makouz
ms.author: genemi
ms.openlocfilehash: 6e3f7929c17b161d3534474d3d9ad99e559714d2
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653800"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server on Windows 的功能
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-174-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver 17.4 for SQL Server

ODBC 驅動程式17.4 包括調整 TCP Keep-alive 設定的能力。 您可以藉由將值新增至驅動程式或 DSN 登錄機碼來進行修改。 金鑰位於中`HKEY_LOCAL_MACHINE\Software\ODBC\` , 適用于系統資料來源, 而在`HKEY_CURRENT_USER\Software\ODBC\`中則用於使用者資料來源。 對於 DSN, 必須將值新增至`...\Software\ODBC\ODBC.INI\<DSN Name>` , 並將驅動程式加入至。 `...\Software\ODBC\ODBCINST.INI\ODBC Driver 17 for SQL Server`

如需詳細資訊, 請參閱[ODBC 元件](../../../odbc/reference/install/registry-entries-for-odbc-components.md)的登錄專案。

值為 `REG_SZ`，如下所示：

- `KeepAlive`藉由傳送 keep-alive 封包, 控制 TCP 嘗試驗證閒置連線是否仍保持不變的頻率。 預設值是 30 秒。

- `KeepAliveInterval`決定在收到回應之前, 用來分隔 keep-alive 重新傳輸的間隔。 預設值為 1 秒。



## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver 13.1 for SQL Server

ODBC Driver 13.1 for SQL Server 包含舊版 (11) 的所有功能, 並在與 Microsoft SQL Server 2016 搭配使用時, 新增 Always Encrypted 和 Azure Active Directory 驗證的支援。  
  
一律加密可讓用戶端將用戶端應用程式內的機密資料進行加密，且永遠不會顯示 SQL Server 的加密金鑰。 安裝在用戶端電腦上且啟用一律加密的驅動程式，透過自動將 SQL Server 用戶端應用程式中的機密資料進行加密與解密，進而達成此目的。 驅動程式會先將敏感資料行中的資料進行加密，才會將資料傳遞至 SQL Server，並自動重寫查詢以保留應用程式的語意。 同樣地，驅動程式會以透明的方式，將查詢結果中加密資料庫資料行所儲存的資料進行解密。 如需詳細資訊，請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)。
 
Azure Active Directory 可讓使用者、DBA 和應用程式設計人員使用 Azure Active Directory 驗證, 做為使用 Azure Active Directory (Azure AD 中的身分識別連接到 Microsoft Azure SQL Database 和 Microsoft SQL Server 2016 的機制). 如需詳細資訊, 請參閱搭配[使用 Azure Active Directory 與 ODBC 驅動程式](../../../connect/odbc/using-azure-active-directory.md), 以及[使用 Azure Active Directory 驗證連接到 SQL Database 或 SQL 資料倉儲](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver 11 for SQL Server  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含隨附於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]Native Client ODBC 驅動程式的所有功能。 如需詳細資訊，請參閱 [SQL Server Native Client 程式設計](../../../relational-databases/native-client/sql-server-native-client-programming.md)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式以 Windows 作業系統中隨附的 ODBC 驅動程式作為基礎。 如需詳細資訊，請參閱 [Windows Data Access Components SDK](https://msdn.microsoft.com/library/aa968814(VS.85).aspx)。  
  
此版本的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含下列新功能：  
  
### <a name="bcpexe--l-option-for-specifying-a-login-timeout"></a>指定登入超時的 bcp-l 選項
 
-l 選項會指定在您嘗試連線到伺服器時，`bcp.exe` 登入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的逾時秒數。 預設登入超時時間為15秒。 登入逾時必須是介於 0 與 65534 之間的數字。 如果所提供的值不是數值或不在該範圍內，`bcp.exe` 就會產生錯誤訊息。 值為0會指定無限的超時時間。 小於 (約) 10 秒的登入逾時不可靠。  
  
### <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]支援[可感知驅動程式的連線共用](https://msdn.microsoft.com/library/hh405031(VS.85).aspx)。 如需詳細資訊，請參閱 [ODBC Driver for SQL Server 中可感知驅動程式的連接共用](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)。  
  
### <a name="asynchronous-execution-notification-method"></a>非同步執行 (通知方法)  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]支援[非同步執行 (通知方法)](https://msdn.microsoft.com/library/hh405038(VS.85).aspx)。 如需使用範例，請參閱[非同步執行 &#40;通知方法&#41; 範例](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)。  
  
### <a name="connection-resiliency"></a>連接恢復功能
若要確保應用程式仍然連接到 Microsoft Azure SQL Database，Windows 上的 ODBC 驅動程式可以還原閒置的連接。 如需詳細資訊，請參閱 [Windows ODBC 驅動程式中的連接恢復功能](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)。  
  
## <a name="behavior-changes"></a>行為變更

在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中, `-y0`如果顯示`sqlcmd.exe`寬度為 0, 則的選項會導致在 1 MB 時截斷輸出。
  
從 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 開始，在已指定 `-y0` 的情況下，單一資料行中已沒有可擷取資料量的限制。 `sqlcmd.exe` 現在會串流多達 2 GB ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型上限) 的資料行。  
  
另一個差異是, 同時`-h`指定`-y0`和現在會產生錯誤報表, 指出選項不相容。 `-h` 會指定要在欄位標題間列印的資料列數目，且從不與 `-y0` 相容，該項目雖然不會列印標題，但是遭到忽略。
  
請注意，依照傳回的資料大小，`-y0` 可能導致伺服器和網路都發生效能問題。

## <a name="see-also"></a>另請參閱  
[Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
