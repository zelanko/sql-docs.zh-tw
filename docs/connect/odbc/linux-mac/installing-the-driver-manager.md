---
title: Installing the Driver Manager (ODBC Driver for SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cd45cc3b0db61e87c8d9ce506e141cc9ad8c97c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798784"
---
# <a name="installing-the-driver-manager"></a>安裝驅動程式管理員
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文包含 Microsoft ODBC 驅動程式的所有版本一起安裝 unixODBC 驅動程式管理員使用，在 Linux 和 macOS 上的 SQL server 的指示。  

> [!IMPORTANT]  
> 在安裝 unixODBC 驅動程式管理員之前，請先刪除您的電腦上安裝的任何驅動程式管理員封裝。 安裝 unixodbc 驅動程式管理員可能會導致現有的驅動程式管理員失敗。  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>安裝 Microsoft ODBC Driver 13、13.1 和 17 的驅動程式管理員
驅動程式管理員相依性會自動解決套件管理系統中的指示安裝 Microsoft ODBC Driver 13、 13.1 或在 Linux 或 macOS 上的 SQL Server 的 17 時[安裝 Microsoft ODBC 驅動程式在 Linux 或 macOS 上的 SQL server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>安裝 Microsoft ODBC Driver 11 for SQL Server 的驅動程式管理員  

（SUSE 和僅限 Red Hat Linux）。

**使用安裝指令碼**  
  
> [!IMPORTANT]  
> 這些指令參考 `msodbcsql-11.0.2270.0.tar.gz`，這是 Red Hat Linux 的安裝檔案。 如果您要安裝 SUSE Linux (預覽)，檔案名稱為 `msodbcsql-11.0.2260.0.tar.gz`。  

若要安裝驅動程式管理員：  
  
1.  請確定您擁有根權限。  
  
2.  移至 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC 驅動程式下載放置檔案 `msodbcsql-11.0.2270.0.tar.gz` 的所在目錄。 請確定您有與您的 Linux 版本相符的 \*.tar.gz 檔案。 若要擷取檔案，請執行下列命令：**tar xvzf msodbcsql-11.0.2270.0.tar.gz**。  

3.  變更為 `msodbcsql-11.0.2270.0` 目錄，在該處您應會看到稱為 `build_dm.sh` 的檔案。 您可以執行`build_dm.sh`以安裝 unixODBC 驅動程式管理員。

4.  若要查看可用的選項清單，請執行下列命令： **./build_dm.sh --help**。  
  
5.  當您準備好要安裝，而且您的電腦可透過 FTP 存取外部網站時，請執行下列命令： **./build_dm.sh**。

如果您的電腦無法透過 FTP 存取外部網站，請取得 `unixODBC-2.3.0.tar.gz`。 您可以從 [http://www.unixodbc.org](http://www.unixodbc.org/) 取得 `unixODBC-2.3.0.tar.gz` 。按一下頁面左側的 [下載]  連結，以移至下載頁面。 然後，按一下適當的連結，以下載 unixODBC-2.3.0 (不是 unixODBC-2.3.1)。 此版本的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不支援 UnixODBC-2.3.1。 執行下列命令以開始進行 unixODBC 驅動程式管理員安裝： **./build_dm.sh --download-url=file://unixODBC-2.3.0.tar.gz**。  

6.  鍵入 **YES**，繼續將檔案解壓縮。 這部分的處理序最多需要 5 分鐘才能完成。  

7.  指令碼停止執行之後，請依照畫面上的指示安裝 unixODBC 驅動程式管理員。

您現在已可開始安裝驅動程式。 如需詳細資訊，請參閱 <<c0> [ 安裝 Microsoft ODBC Driver for Linux 和 macOS 上的 SQL Server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。  

**手動安裝**

如果安裝指令碼無法完成，請自行設定並建置適當的驅動程式管理員。

1.  移除任何已安裝的舊版 unixODBC (例如 unixODBC 2.2.11)。 在 Red Hat Enterprise Linux 5 或 6 上，執行下列命令：**yum remove unixODBC**。 在 SUSE Linux Enterprise、 **zypper 移除 unixODBC**。  
  
2.  移至 [http://www.unixodbc.org](http://www.unixodbc.org/)。按一下頁面左側的 [下載]  連結，以移至下載頁面。 然後按一下適當的連結，以將檔案 unixODBC-2.3.0.tar.gz 儲存至您的電腦。 此版本的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不支援 UnixODBC-2.3.1。  
  
3.  在您的 Linux 電腦上執行命令： **tar xvzf unixODBC-2.3.0.tar.gz**。  
  
4.  切換至 unixODBC-2.3.0 目錄。  
  
5.  在命令提示字元，執行下列命令： **CPPFLAGS ="-DSIZEOF_LONG_INT = 8"** 。  
  
6.  在命令提示字元，執行下列命令：**export CPPFLAGS**。  
  
7.  在命令提示字元，執行下列命令： **"./configure --prefix=/usr --libdir=/usr/lib64 --sysconfdir=/etc --enable-gui=no --enable-drivers=no --enable-iconv --with-iconv-char-enc=UTF8 --with-iconv-ucode-enc=UTF16LE"** .  
  
8.  在命令提示字元中 (以根使用者身分登入)，執行下列命令：**make**。  
  
9. 在命令提示字元中 (以根使用者身分登入)，執行下列命令：**make install**。  

您現在已可開始安裝驅動程式。 如需詳細資訊，請參閱 <<c0> [ 安裝 Microsoft ODBC Driver for Linux 和 macOS 上的 SQL Server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱
[在 Linux 和 macOS 上安裝 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[此驅動程式版本的已知問題](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[版本資訊](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
