---
title: 下載 ODBC Driver for SQL Server
ms.date: 04/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53b09784-bb9d-4fd4-99d3-0492b3308ac4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ce99312dac0fa05af904f1c6a8c5e78c398d70fe
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924575"
---
# <a name="download-odbc-driver-for-sql-server"></a>下載 ODBC Driver for SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Microsoft ODBC Driver for SQL Server 是單一動態連結程式庫 (DLL)，包含使用機器碼 API 連線至 SQL Server 的應用程式執行階段支援。 使用 Microsoft ODBC Driver 17 for SQL Server 建立新應用程式，或加強需要利用較新 SQL Server 功能的現有應用程式。

## <a name="download-for-windows"></a>下載 Windows 版

Microsoft ODBC Driver 17 for SQL Server 的可轉散發安裝程式會安裝必要的用戶端元件，以在執行階段期間使用較新的 SQL Server 功能。 安裝程式會選擇性地安裝必要的標頭檔，以供開發使用 ODBC API 的應用程式。 從 17.4.2 版開始，該安裝程式也會包含並安裝 Microsoft Active Directory 驗證程式庫 (ADAL.dll)。

17.5.2 版是最新的正式運作 (GA) 版本。 如果已安裝舊版的 Microsoft ODBC Driver 17 for SQL Server，則安裝 17.5.2 便會將其升級至 17.5.2。

**[![下載](../../ssms/media/download-icon.png) 下載 Microsoft ODBC Driver 17 for SQL Server (x64)](https://go.microsoft.com/fwlink/?linkid=2120137)**  
**[![下載](../../ssms/media/download-icon.png) 下載 Microsoft ODBC Driver 17 for SQL Server (x86)](https://go.microsoft.com/fwlink/?linkid=2120140)**  

### <a name="version-information"></a>版本資訊

- 版本號碼：17.5.2.1
- 發行日期：2020 年 3 月 6 日

> [!Note]
> 如果您在非英文語言版本存取此頁面，且想要查看最新內容，請參閱[本頁面的英文 (美國) 版](https://aka.ms/downloadmsodbcsqlenglish)。 您可以選取[可用的語言](#available-languages)，從英文 (美國) 版網站下載不同語言版本。

## <a name="available-languages"></a>可用的語言

此 Microsoft ODBC Driver for SQL Server 版本可以用下列語言安裝：

Microsoft ODBC Driver 17.5.2 for SQL Server (x64)：  
[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x40a)

Microsoft ODBC Driver 17.5.2 for SQL Server (x86)：  
[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x40a)

### <a name="release-notes-for-windows"></a>Windows 版本資訊

如需此 Windows 版本的詳細資料，請參閱 [Windows 版本資訊](windows\release-notes-odbc-sql-server-windows.md)。

### <a name="previous-releases-for-windows"></a>Windows 先前版本

若要下載舊版 Windows，請參閱[舊版 Microsoft ODBC Driver for SQL Server](windows\release-notes-odbc-sql-server-windows.md#previous-releases)。

## <a name="download-for-linux-and-macos"></a>適用於 Linux 與 macOS 的下載

可使用相關的安裝指示以適用於 Linux 與 macOS 的套件管理員來下載並安裝 Microsoft ODBC Driver for SQL Server：  
[安裝 ODBC for SQL Server (Linux)](linux-mac\installing-the-microsoft-odbc-driver-for-sql-server.md)  
[安裝 ODBC for SQL Server (macOS)](linux-mac\install-microsoft-odbc-driver-sql-server-macos.md)  

如果需要下載可離線安裝的套件，可透過下列連結取得所有版本。

> [!Note]
> 名為 `msodbcsql17-*` 的套件為最新版本。 名為 `msodbcsql-*` 的套件為驅動程式其 13 版。

### <a name="alpine"></a>Alpine

- [Alpine 套件](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.apk) ([PGP 簽章](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.sig))

### <a name="debian"></a>Debian

- [Debian 10 .deb 套件](https://packages.microsoft.com/debian/10/prod/pool/main/m/msodbcsql17/) \(英文\)
- [Debian 9 .deb 套件](https://packages.microsoft.com/debian/9/prod/pool/main/m/msodbcsql17/) \(英文\)
- [Debian 8 .deb 套件](https://packages.microsoft.com/debian/8/prod/pool/main/m/msodbcsql17/) \(英文\)
- [Debian 8 .deb 套件 (msodbcsql 13.x)](https://packages.microsoft.com/debian/8/prod/pool/main/m/msodbcsql/)

### <a name="redhat"></a>RedHat

- [RedHat 8 .rpm 套件](https://packages.microsoft.com/rhel/8/prod/)
- [RedHat 7 .rpm 套件](https://packages.microsoft.com/rhel/7/prod/)
- [RedHat 6 .rpm 套件](https://packages.microsoft.com/rhel/6/prod/)

### <a name="suse"></a>Suse

- [SuSE 15 .rpm 套件](https://packages.microsoft.com/sles/15/prod/)
- [SuSE 12 .rpm 套件](https://packages.microsoft.com/sles/12/prod/)
- [SuSE 11 .rpm 套件](https://packages.microsoft.com/sles/11/prod/)

### <a name="ubuntu"></a>Ubuntu

- [Ubuntu 19.10 .deb 套件](https://packages.microsoft.com/ubuntu/19.10/prod/pool/main/m/msodbcsql17/)
- [Ubuntu 18.04 .deb 套件](https://packages.microsoft.com/ubuntu/18.04/prod/pool/main/m/msodbcsql17/) \(英文\)
- [Ubuntu 16.04 .deb 套件](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql17/) \(英文\)
- [Ubuntu 14.04 .deb 套件](https://packages.microsoft.com/ubuntu/14.04/prod/pool/main/m/msodbcsql17/) \(英文\)
- [Ubuntu 16.04 .deb 套件 (msodbcsql 13.x)](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/)
- [Ubuntu 14.04 .deb 套件 (msodbcsql 13.x)](https://packages.microsoft.com/ubuntu/14.04/prod/pool/main/m/msodbcsql/)

另請參閱[安裝 Linux 驅動程式](linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

### <a name="macos"></a>macOS

- 如需詳細資訊，請參閱 [Homebrew 公式](https://github.com/Microsoft/homebrew-mssql-release)。

另請參閱[安裝 macOS 驅動程式](linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)。

### <a name="older-linux-releases"></a>舊版 Linux

- **Red Hat Enterprise Linux 5 和 6 (64 位元)**  - [下載 Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
- **SUSE Linux Enterprise 11 Service Pack 2 (64 位元)**  - [下載 Microsoft ODBC Driver 11 Preview for SQL Server - SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)

### <a name="release-notes-for-linux-and-macos"></a>Linux 與 macOS 版本資訊

如需 Linux 與 macOS 版本的詳細資料，請參閱 [Linux 與 macOS 版本資訊](linux-mac\release-notes-odbc-sql-server-linux-mac.md)。
