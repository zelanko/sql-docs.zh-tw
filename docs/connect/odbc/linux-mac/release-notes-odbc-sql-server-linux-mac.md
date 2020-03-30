---
title: Linux 和 macOS 上的 ODBC Driver for SQL Server 版本資訊
ms.custom: ''
ms.date: 03/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-jizho2
ms.technology: connectivity
ms.topic: conceptual
author: v-chojas
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: b2adbb0fca6c717a5864570cad40c65d7c332f90
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "79090502"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Linux 和 macOS 上 Microsoft ODBC Driver for SQL Server 的版本資訊

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文列出並描述 Linux 和 macOS 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行版本的新增功能。

<!--
Going forward, please use the new 2-column markdown table for each new H2 version section.
And we are keeping the H2 titles much shorter, partly by removing redundant or obvious info.
We want to track the Month YYYY each new version H2 section is added, at the end of the H2 title.
This is the new standard format for Release Notes article content.

OLD     FILE NAME:    linux-mac/release-notes.md
NOW NEW FILE NAME:    linux-mac/release-notes-odbc-sql-server-linux-mac.md

Thank you.
GeneMi.  2019/04/03.
-->

## <a name="1752-march-2020"></a>17.5.2，2020 年 3 月

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援使用 Azure Key Vault 受控識別進行驗證 | 請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md)。 |
| 支援其他的 Azure Key Vault 端點 | 請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md)。 |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="175-january-2020"></a>17.5，2020 年 1 月

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| SQL_COPT_SS_SPID 連線屬性，無需往返伺服器即可擷取 SPID | 請參閱 [DSN 和連接字串屬性和關鍵字](../dsn-connection-string-attribute.md)。 |
| 支援透過 Debian 和 Ubuntu 上的 `debconf` 來指示接受 EULA | 請參閱[安裝驅動程式](./installing-the-microsoft-odbc-driver-for-sql-server.md)。 |
| 支援新的散發套件。 | &bull; &nbsp; &nbsp; Alpine Linux (3.10、3.11)<br/>&bull; &nbsp; &nbsp; Oracle Linux 8<br/>&bull; &nbsp; &nbsp; Ubuntu 19.10<br/>&bull; &nbsp; &nbsp; macOS 10.15 |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="1742-october-2019"></a>17.4.2，2019 年 10 月

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援其他的 Azure Key Vault 端點 | 請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md)。 |
| 支援設定資料分類版本 | 請參閱[資料分類](../data-classification.md#bkmk-version)。 |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

**已知問題：**

使用具有安全記憶體保護區的 Always Encrypted 與 Azure Key Vault 時，奇數的金鑰路徑長度可能會導致 CMK 簽章驗證錯誤。 如果遇到此問題，請嘗試將 AKV 金鑰重新命名，以透過增加/刪除一個字元來變更金鑰路徑的長度。

## <a name="174-august-2019"></a>17.4，2019 年 8 月

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 具有安全記憶體保護區的 Always Encrypted。 | 請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md)。 |
| 動態載入 OpenSSL | 請參閱[程式設計指導方針](programming-guidelines.md#bkmk-openssl)。 |
| 可設定的 TCP 保持連線設定。 | 請參閱[連線到 SQL Server](connection-string-keywords-and-data-source-names-dsns.md)。 |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="173-february-2019"></a>17.3，2019 年 2 月

| 新項目 | 詳細資料 |
| :------- | :------ |
| 支援新的散發套件。 | &bull; &nbsp; &nbsp; SUSE 15<br/>&bull; &nbsp; &nbsp; Ubuntu 18.10<br/>&bull; &nbsp; &nbsp; macOS 10.14 |
| Azure Active Directory 受控服務識別 (系統和使用者指派) 驗證模式。 | 請參閱[搭配 ODBC 驅動程式使用 Azure Active Directory](../using-azure-active-directory.md)。 |
| 針對 Always Encrypted 資料行串流輸入參數的能力。 | 如需詳細資訊，請參閱[使用 Always Encrypted 時的 ODBC 驅動程式限制](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted)。 |
| XA 分散式交易。 | 請參閱[使用 XA 交易](../use-xa-with-dtc.md)。<br/><br/>XA 是 _eXtended Architecture_ (延伸架構) 的縮寫，這是針對存取多個伺服器端資料儲存系統的全域交易執行標準。 |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2，2018 年 7 月

| 新項目 | 詳細資料 |
| :------- | :------ |
| 支援新的散發套件。 | &bull; &nbsp; &nbsp; Ubuntu 18.04 |
| 適用於 Azure SQL Database 和 SQL Server 的資料分類。 | 請參閱[資料分類](../data-classification.md)。 |
| 支援 UTF-8 伺服器編碼。 | &nbsp; |
| `SQLBrowseConnect` | &nbsp; |
| 對 `libcurl` 具有動態相依性。 | 從此版本開始，`libcurl` 套件不是明確相依性。<br/>使用 Azure Key Vault 或 Azure Active Directory 驗證時，需要 OpenSSL 或 NSS 的 `libcurl` 套件。<br/>如果您遇到有關 `libcurl` 的錯誤，請確定它已安裝。 |
| 連接字串中 ConnectRetryCount 和 ConnectRetryInterval 關鍵字的閒置連接復原功能。 | &bull; &nbsp; &nbsp; 使用 `SQL_COPT_SS_CONNECT_RETRY_COUNT` (唯讀) 來擷取連線重試嘗試次數。<br/><br/>&bull; &nbsp; &nbsp; 使用 `SQL_COPT_SS_CONNECT_RETRY_INTERVAL` (唯讀) 來擷取連線重試間隔的長度。<br/><br/>請參閱 [Windows ODBC 驅動程式中的連接復原功能](../windows/connection-resiliency-in-the-windows-odbc-driver.md)。 |
| 錯誤修正。 | [錯誤修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>17.1，2018 年 3 月

| 新項目 | 詳細資料 |
| :------- | :------ |
| `SQL_COPT_SS_CEKCACHETTL` 和 `SQL_COPT_SS_TRUSTEDCMKPATHS` 連接屬性的支援。 | &bull; &nbsp; &nbsp; `SQL_COPT_SS_CEKCACHETTL` 允許控制資料行加密金鑰本機快取存在的時間，並加以排清。<br/><br/>&bull; &nbsp; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS` 允許應用程式限制 Always Encrypted 作業只能使用指定的資料行主要金鑰清單。<br/><br/>請參閱[搭配使用 Always Encrypted 與 ODBC Driver for SQL Server](../using-always-encrypted-with-the-odbc-driver.md)。 |
| 支援從預設位置載入 `.rll`。 | 請參閱[安裝文件中的＜資源檔案載入＞小節](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading)。 |
| 錯誤修正。 | [錯誤修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="17"></a>17

**支援新的散發套件**：macOS High Sierra 和 Ubuntu 17.10 

**效能改進**：當驅動程式在 UTF-8/16 之間轉換時大於 10 倍的效能改進。

**新增功能**：

BCP API 的 Always Encrypted 支援

新連接字串屬性 UseFMTOnly 會導致驅動程式在需要暫存資料表的特殊案例中使用舊版中繼資料。

Azure SQL 受控執行個體的支援。 
> [!NOTE]
> 使用受控執行個體時，有一些差異：
> -   不支援 FILESTREAM 
> -   不支援本機檔案系統存取，但 tracefiles 等項目需要本機檔案系統存取 
> -   不支援從本機路徑建立 UDT 
> -   不支援 Windows 整合式驗證 
> -   不支援 DTC 
> -   'sa' 帳戶不存在 (預設帳戶稱為 'cloudSA')
> -   TDS 權杖錯誤 (0xAA) 會傳回不正確的伺服器名稱
> -   不支援在資料庫名稱中使用特殊字元 
> -   不支援 ALTER DATABASE [dbname1] MODIFY NAME = [dbname2]
> -   錯誤訊息一律會以英文顯示，不論語言設定為何 (與 Azure 相同) 

## <a name="131-for-ssnoversion-on-linux-and-macos-may-2017"></a>Linux 和 macOS 上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 13.1，2017 年 5 月

ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 新增在與 Microsoft SQL Server 2016 一起使用時對 Always Encrypted 及 Azure Active Directory 的支援。

**支援新的散發套件**：在 macOS 上的 ODBC Driver 第一個版本支援 OS X 10.11 和 macOS 10.12。 Ubuntu 16.10 現在也已連同 Red Hat 6、7 和 SUSE 12 受到支援。 每個平台都有平台相關的套件 (RPM 或 DEB)，以便簡化安裝和設定。 如需詳細資訊，請參閱 [Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) 與 [macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md) 的 ODBC 驅動程式安裝指示。

**unixODBC Driver Manager 2.3.1 支援變更**：ODBC 驅動程式不再依賴 unixODBC 驅動程式管理員的自訂封裝 (RedHat 6 上除外)，並改為依賴散發套件管理員，從散發套件存放庫解析 UnixODBC 相依性。

**BCP API 支援**：Linux 和 macOS 的 ODBC 驅動程式現在支援使用 [BCP API 函式 (**bcp_init** 等等)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="130-for-ssnoversion-on-linux"></a>Linux 上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 13.0

透過 Microsoft ODBC Driver 13.0 for SQL Server，SQL Server 2014 和 SQL Server 2016 現在也已受到支援。  

**支援新的散發套件**：

Ubuntu 現在已連同 Red Hat 和 SUSE 受到支援。 每個平台都有平台相關的套件 (RPM 或 DEB)，以便簡化安裝和設定。  如需安裝指示，請參閱[安裝驅動程式](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

**unixODBC Driver Manager 2.3.1 支援**：除了較新的驅動程式管理員，也有一個套件用來安裝此相依性，以便簡化安裝和設定。  

**透明網路 IP 解析**：透明網路 IP 解析是現有多重子網路容錯移轉功能的修訂，它會影響當主機名稱的第一個解析 IP 無回應且有多個 IP 與主機名稱相關聯時，驅動程式的連接順序。

**TLS 1.2 支援**：Linux 上的 Microsoft ODBC Driver 13.0 for SQL Server 現在在使用與 SQL Server 之間的安全通訊時，支援 TLS1.2。

## <a name="11-for-ssnoversion-on-linux"></a>Linux 上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 11

ODBC Driver on SUSE Linux (預覽) 支援 64 位元 SUSE Linux Enterprise 11 Service Pack 2。 如需詳細資訊，請參閱[系統需求](../../../connect/odbc/linux-mac/system-requirements.md)。  

Linux 上的 ODBC 驅動程式支援 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]。 如需詳細資訊，請參閱 [Linux 上 ODBC Driver 對於高可用性、災害復原的支援](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  

ODBC Driver on Linux 支援對 Microsoft Azure SQL Database 的連接。 如需詳細資訊，請參閱 [如何：使用 ODBC 連接到 Azure SQL Database](https://msdn.microsoft.com/library/hh974312.aspx)。  

`-l` 選項 (登入逾時) 已新增至 `bcp`。 如需詳細資訊，請參閱[使用 **bcp** 連線](../../../connect/odbc/linux-mac/connecting-with-bcp.md)。
