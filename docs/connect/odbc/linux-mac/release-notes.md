---
title: "版本資訊-Microsoft ODBC Driver for SQL Server on Linux 及 macOS |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 84bb78e184f1bca9e683aeebf46b178e3a7dd61f
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Microsoft ODBC Driver for SQL Server on Linux 及 macOS 的版本資訊
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-linux-and-macos"></a>新功能[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux 及 macOS  

ODBC Driver 13.1 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]新增一律加密與 Azure Active Directory 時用於搭配 Microsoft SQL Server 2016 的支援。

**支援的新發佈**: OS X 10.11 及 macOS 10.12 macOS 上的 ODBC 驅動程式的第一個版本中支援。 Ubuntu 16.10 現在也支援，連同 Red Hat 6、 7 和 SUSE 12。 每個平台都有平台相關的封裝 （RPM 或 DEB） 可簡化安裝和設定。  請參閱[安裝驅動程式](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)如需安裝指示。

**unixODBC Driver Manager 2.3.1 支援變更**: ODBC 驅動程式不再依賴的 unixodbc 驅動程式的自訂封裝 （除了 RedHat 6），並改為依賴發佈的封裝管理員，來解決 UnixODBC 相依性從分佈的儲存機制。

**BCP API 支援**： 的 Linux 及 macOS ODBC 驅動程式現在支援使用[BCP API 函數 (**bcp_init**等。)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>新功能的 Microsoft ODBC 驅動程式 13.0 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] on Linux  
Microsoft ODBC Driver for SQL Server 13.0，與 SQL Server 2014 和 SQL Server 2016 現在也支援。  

**支援的新發佈**:

Ubuntu 現在已連同 Red Hat 和 SUSE 受到支援。 每個平台都有平台相關的封裝 （RPM 或 DEB） 可簡化安裝和設定。  請參閱[安裝驅動程式](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)如需安裝指示。

**unixODBC Driver Manager 2.3.1 支援**： 除了較新的驅動程式管理員，此外還有安裝簡化安裝和設定此相依性的套件。  

**透明網路 IP 解析**： 透明網路 IP 解析為現有的多重子網路容錯移轉功能會影響連接的序列中第一個解析主機名稱的 IP 並不會的看到的驅動程式的修訂回應，有多個主機名稱相關聯的 Ip。

**TLS 1.2 支援**: SQL Server on Linux 的 Microsoft ODBC 驅動程式 13.0 時現在還支援 TLS 1.2 與 SQL Server 的安全通訊所使用。

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>新功能的[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] on Linux  
ODBC Driver on SUSE Linux (預覽) 支援 64 位元 SUSE Linux Enterprise 11 Service Pack 2。 如需詳細資訊，請參閱[系統需求](../../../connect/odbc/linux-mac/system-requirements.md)。  

ODBC driver on Linux 支援[!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]。 如需詳細資訊，請參閱[ODBC Driver on Linux 支援高可用性、 災害復原](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  

ODBC Driver on Linux 支援對 Microsoft Azure SQL Database 的連接。 如需詳細資訊，請參閱 [如何：使用 ODBC 連接到 Windows Azure SQL Database](http://msdn.microsoft.com/library/hh974312.aspx)。  

`-l`選項 （登入逾時） 已新增到`bcp`。 如需詳細資訊，請參閱[連接**bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)。

