---
title: 系統需求 (ODBC Driver for SQL Server)
description: 此清單會列出 Linux 和 macOS 作業系統上 ODBC Driver for SQL Server 的系統需求。
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 74b7bf1680dd956dfca85917939ad24a3559d7de
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934457"
---
# <a name="system-requirements-linux-and-macos"></a>系統需求 (Linux 和 macOS)

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本主題列出使用 Linux 和 macOS 版 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的需求。

## <a name="sql-version-compatibility"></a>SQL 的版本相容性

Linux 和 macOS 驅動程式的 SQL 版本相容性，與 [Windows 驅動程式 SQL 版本相容性](../windows/system-requirements-installation-and-driver-files.md#sql-version-compatibility)相同。

## <a name="operating-system-support"></a>作業系統支援

下列作業系統的 x64 結構上支援 Linux 和 macOS 驅動程式版本 17、13.1 和 13：

|驅動程式版本&nbsp;&#8594;<br />&#8595; 作業系統     |17.6|17.5|17.4|17.3|17.2|17.1|17.0|13.1|13|
|-------------------------------|----|----|----|----|----|----|----|----|---|
|Apple OS X 10.11 (El Capitan)  |    |    |是 |是 |是 |是 |是 |是 |是|
|Apple macOS 10.12 (Sierra)     |    |    |是 |是 |是 |是 |是 |是 |是|
|Apple macOS 10.13 (High Sierra)|是 |是 |是 |是 |是 |是 |是 |是 |是|
|Apple macOS 10.14 (Mojave)     |是 |是 |是 |是 |    |    |    |    |   |
|Apple macOS 10.15 (Catalina)   |是 |是 |    |    |    |    |    |    |   |
|Alpine Linux 3.11              |是 |是 |    |    |    |    |    |    |   |
|Debian Linux 8                 |是 |是 |是 |是 |是 |是 |是 |是 |是|
|Debian Linux 9                 |是 |是 |是 |是 |是 |是 |是 |是 |是|
|Debian Linux 10                |是 |是 |是 |    |    |    |    |    |   |
|Oracle Linux 8                 |是 |是 |    |    |    |    |    |    |   |
|RedHat Enterprise Linux 6      |是 |是 |是 |是 |是 |是 |是 |是 |是|
|RedHat Enterprise Linux 7      |是 |是 |是 |是 |是 |是 |是 |是 |是|
|RedHat Enterprise Linux 8      |是 |是 |是 |    |    |    |    |    |   |
|SUSE Linux Enterprise Server 11<sup>1</sup>|是 |是 |是 |是 |是 |是 |是 |是 |是|
|SUSE Linux Enterprise Server 12|是 |是 |是 |是 |是 |是 |是 |是 |是|
|SUSE Linux Enterprise Server 15|是 |是 |是 |是 |    |    |    |    |   |
|Ubuntu Linux 14.04             |    |    |是 |是 |是 |是 |是 |是 |是|
|Ubuntu Linux 16.04             |是 |是 |是 |是 |是 |是 |是 |是 |是|
|Ubuntu Linux 18.04             |是 |是 |是 |是 |是 |    |    |    |   |
|Ubuntu Linux 20.04             |是 |    |    |    |    |    |    |    |   |

<sup>1</sup> ODBC Driver 17 僅支援 SUSE Linux Enterprise Server 11 SP4

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Linux 和 macOS 的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13、13.1 及 17 版的安裝套件，在使用散發套件的套件管理系統安裝時，可自動解析驅動程式的相依性，如[安裝 ODBC Driver (Linux)](installing-the-microsoft-odbc-driver-for-sql-server.md) 和[安裝 ODBC Driver (macOS)](install-microsoft-odbc-driver-sql-server-macos.md) 中所述。

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
* 64 位元 UnixODBC 2.3.0 驅動程式管理員 (針對 64 位元 SQLLEN/SQLULEN 建置)。 Linux 上的 ODBC 驅動程式不支援較新版本的 64 位元 UnixODBC 驅動程式管理員。 如需相關資訊，請參閱 [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) 。  
  
* **Red Hat Enterprise Linux 5 (64 位元)** 的 ODBC 驅動程式需要下列套件，而且可以在這裡下載：[Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `e2fsprogs-libs`  
  * `krb5-libs`  
  * `openssl`  
  
* **Red Hat Enterprise Linux 6 (64 位元)** 的 ODBC 驅動程式需要下列套件，而且可以在這裡下載：[Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `libuuid`  
  * `krb5-libs`  
  * `openssl`  
  
* **SUSE Linux Enterprise 11 Service Pack 2 (64 位元)** 的 ODBC 驅動程式需要下列套件，而且可以在這裡下載：[Microsoft ODBC Driver 11 (預覽) for SQL Server - SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
  * `glibc`  
  * `libstdc++46`  
  * `libgcc46`  
  * `libuuid1`  
  * `krb5`  
  * `libopenssl0_9_8`  
  
## <a name="see-also"></a>另請參閱

[安裝驅動程式管理員](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)  
[此驅動程式版本的已知問題](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  
[版本資訊](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
