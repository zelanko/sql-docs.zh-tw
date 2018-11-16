---
title: 版本資訊：在 Linux 和 macOS 上安裝 Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 62270c3cce4b1a5f57874d6cd40c7c64ff409100
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600298"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Linux 和 macOS 上 Microsoft ODBC Driver for SQL Server 的版本資訊
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 和 macOS 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能

**新的散發套件支援**: Ubuntu 18.04

**新增功能**:

資料分類，Azure SQL Database 和 SQL Server，如需詳細資訊請參閱[資料分類](../data-classification.md)

支援 utf-8 伺服器版本編碼方式

SQLBrowseConnect

上的動態相依性`libcurl`:
- 此版本中，從開始`libcurl`套件並非明確相依性。 `libcurl`封裝 OpenSSL 或 NSS 時，必須使用 Azure 金鑰保存庫或 Azure Active Directory 驗證。 如果您遇到的錯誤有關`libcurl`，確定它已安裝。

ConnectRetryCount 和 ConnectRetryInterval 連接字串中的關鍵字與閒置連接恢復功能 (如需詳細資訊，請參閱 < [Connection Resiliency in the Windows ODBC Driver](../windows/connection-resiliency-in-the-windows-odbc-driver.md)):
- 使用`SQL_COPT_SS_CONNECT_RETRY_COUNT`（唯讀） 來擷取連接重試嘗試次數。
- 使用`SQL_COPT_SS_CONNECT_RETRY_INTERVAL`（唯讀） 來擷取連接重試間隔的長度。
- 連接將會重試一次的預設值。


[ug 修正](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 和 macOS 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能

**新增功能**:

支援`SQL_COPT_SS_CEKCACHETTL`並`SQL_COPT_SS_TRUSTEDCMKPATHS`連接屬性 (如需詳細資訊，請參閱[搭配 ODBC Driver for SQL Server 使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` 可讓控制本機快取的資料行加密金鑰存在的時間，以及排清它
- `SQL_COPT_SS_TRUSTEDCMKPATHS` 允許應用程式限制為只使用指定的清單的資料行主要金鑰的 AE 作業



支援載入`.rll`從預設位置 (如需詳細資訊，請參閱 <<c2> [ 安裝文件中的 '資源檔案載入' 區段](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading))

[ug 修正](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 和 macOS 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能

**新的散發套件支援**: macOS High Sierra 和 Ubuntu 17.10 

**效能改進**： 大於 10 倍的效能改進當驅動程式將轉換/8/utf-16。

**新增功能**:

Always Encrypted 支援適用於 BCP API

新的連接字串屬性 UseFMTOnly 會導致驅動程式需要暫存資料表的特殊案例中使用舊版的中繼資料。

Azure SQL 受控執行個體 （延伸私人預覽） 支援。 
> [!NOTE]
> 使用受控執行個體時，有一些差異：
> -   不支援檔案資料流 
> -   本機檔案系統存取不受支援，但所需的 tracefiles 等項目 
> -   建立 UDT，從本機路徑不支援 
> -   不支援 Windows 整合式驗證 
> -   不支援 DTC 
> -   'sa' 帳戶不存在 （預設帳戶稱為 'cloudSA'）
> -   TDS token 錯誤 (0xAA) 傳回不正確的伺服器名稱
> -   不支援資料庫名稱 中的特殊字元 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] 不支援
> -   錯誤訊息一律會顯示在英文中，不論語言為何 （與 Azure 相同） 的設定 

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 和 macOS 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能  

ODBC Driver 13.1 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]新增一律加密，並在搭配 Microsoft SQL Server 2016 中使用時，則 Azure Active Directory 的支援。

**新的散發套件支援**: ODBC 驅動程式，在 macOS 上的第一個版本支援 OS X 10.11 和 macOS 10.12。 Ubuntu 16.10 現在也支援，以及 Red Hat 6、 7 和 SUSE 12。 每個平台具有平台相關的封裝 （RPM 或 DEB） 簡化的安裝和設定。  請參閱[安裝驅動程式](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)如需安裝指示。

**unixODBC Driver Manager 2.3.1 支援變更**: ODBC 驅動程式不再依賴的 unixodbc 驅動程式的自訂封裝 （RedHat 6 上除外），並改為依賴發佈的套件管理員，若要解決 UnixODBC 相依性從散發存放庫。

**BCP API 支援**: Linux 和 macOS 的 ODBC 驅動程式現在支援使用[BCP API 函式 (**bcp_init**，依此類推。)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>什麼是新的 Microsoft ODBC Driver 13.0 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Linux 上  
使用 Microsoft ODBC Driver 13.0 for SQL Server，SQL Server 2014 和 SQL Server 2016 現在也支援。  

**新的散發套件支援**:

Ubuntu 現在已連同 Red Hat 和 SUSE 受到支援。 每個平台具有平台相關的封裝 （RPM 或 DEB） 簡化的安裝和設定。  請參閱[安裝驅動程式](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)如需安裝指示。

**unixODBC Driver Manager 2.3.1 支援**： 除了較新的驅動程式管理員，也沒有安裝簡化安裝和設定此相依性的套件。  

**透明網路 IP 解析**： 透明網路 IP 解析是現有的多重子網路容錯移轉功能會影響在第一個解析主機名稱的 IP 不的情況下的驅動程式的連接順序的修訂回應，並有多個主機名稱相關聯的 Ip。

**TLS 1.2 支援**: Linux 上的 SQL Server 的 Microsoft ODBC Driver 13.0 現在支援 TLS 1.2，使用與 SQL Server 的安全通訊時。

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>Linux 和 macOS 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能  
ODBC Driver on SUSE Linux (預覽) 支援 64 位元 SUSE Linux Enterprise 11 Service Pack 2。 如需詳細資訊，請參閱 [System Requirements](../../../connect/odbc/linux-mac/system-requirements.md)。  

ODBC Driver on Linux 支援 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]。 如需詳細資訊，請參閱 < [ODBC Driver on Linux 支援的高可用性、 災害復原](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  

ODBC Driver on Linux 支援對 Microsoft Azure SQL Database 的連接。 如需詳細資訊，請參閱 [如何：使用 ODBC 連接到 Windows Azure SQL Database](https://msdn.microsoft.com/library/hh974312.aspx)。  

`-l`選項 （登入逾時） 已新增至`bcp`。 如需詳細資訊，請參閱[使用 **bcp** 連線](../../../connect/odbc/linux-mac/connecting-with-bcp.md)。
