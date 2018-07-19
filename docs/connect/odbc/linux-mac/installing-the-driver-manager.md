---
title: Installing the Driver Manager (ODBC Driver for SQL Server) |Microsoft 文件
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
caps.latest.revision: 59
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18827f8e2e001700319d47516ba1694c384b26b7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853193"
---
# <a name="installing-the-driver-manager"></a>安裝驅動程式管理員
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文章包含隨所有版本的 Microsoft ODBC Driver for SQL Server on Linux 及 macOS 安裝 unixODBC 驅動程式管理員使用的指示。  

> [!IMPORTANT]  
> 在安裝 unixODBC 驅動程式管理員之前，請先刪除您的電腦上安裝的任何驅動程式管理員封裝。 安裝 unixodbc 驅動程式管理員可能會導致現有的驅動程式管理員失敗。  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>安裝 Microsoft ODBC Driver 13、 13.1，/ 17 的驅動程式管理員
驅動程式管理員相依性便會自動解除封裝管理系統中的指示安裝 Microsoft ODBC Driver 13、 13.1 或如 SQL Server on Linux 或 macOS 17 時[安裝 Microsoft ODBC 驅動程式針對 SQL Server on Linux 或 macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>安裝 Microsoft ODBC Driver 11 for SQL Server 的驅動程式管理員  

（SUSE 和 Red Hat Linux 只）。

**使用安裝指令碼**  
  
> [!IMPORTANT]  
> 這些指示是指`msodbcsql-11.0.2270.0.tar.gz`，這是 Red Hat Linux 的安裝檔案。 如果您要安裝 SUSE Linux 的預覽，則檔案名稱是`msodbcsql-11.0.2260.0.tar.gz`。  

若要安裝驅動程式管理員：  
  
1.  請確定您擁有根權限。  
  
2.  移至的目錄位置[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ODBC Driver 下載放置檔案稱為`msodbcsql-11.0.2270.0.tar.gz`。 請確定您有與您的 Linux 版本相符的 \*.tar.gz 檔案。 要擷取檔案，請執行下列命令： **tar 檔案解壓縮 xvzf msodbcsql-11.0.2270.0.tar.gz**。  

3.  若要變更`msodbcsql-11.0.2270.0`目錄該處您應會見名為的檔案和`build_dm.sh`。 您可以執行`build_dm.sh`安裝 unixODBC 驅動程式管理員。

4.  若要查看可用的選項清單，請執行下列命令： **./build_dm.sh-說明**。  
  
5.  當您準備好要安裝，而且您的電腦可以存取透過 FTP 外部網站，請執行下列命令： **./build_dm.sh**。

如果您的電腦無法存取外部透過 FTP 網站，取得`unixODBC-2.3.0.tar.gz`。 您可以取得`unixODBC-2.3.0.tar.gz`從[ http://www.unixodbc.org ](http://www.unixodbc.org/)。按一下**下載**来移至下載頁面的頁面左側的連結。 然後，按一下適當的連結，以下載 unixODBC-2.3.0 (不是 unixODBC-2.3.1)。 此版本不支援 unixodbc-2.3.1 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 執行下列命令，以便開始進行 unixODBC 驅動程式管理員安裝： **./build_dm.sh-下載 url = file://unixODBC-2.3.0.tar.gz**。  

6.  型別**是**繼續將檔案解壓縮。 這部分的程序可能需要五分鐘的時間才能完成。  

7.  指令碼停止執行之後，請依照畫面上的指示安裝 unixODBC 驅動程式管理員。

您現在已可開始安裝驅動程式。 如需詳細資訊，請參閱[安裝的 Microsoft ODBC Driver for SQL Server on Linux 及 macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。  

**手動安裝**

如果安裝指令碼無法完成，請自行設定並建置適當的驅動程式管理員。

1.  移除任何已安裝的舊版 unixODBC (例如 unixODBC 2.2.11)。 在 Red Hat Enterprise Linux 5 或 6 上，執行下列命令： **yum 移除 unixODBC**。 SUSE Linux Enterprise 上**zypper 移除 unixODBC**。  
  
2.  移至[ http://www.unixodbc.org ](http://www.unixodbc.org/)。按一下**下載**来移至下載頁面的頁面左側的連結。 然後按一下適當的連結，以將檔案 unixODBC-2.3.0.tar.gz 儲存至您的電腦。 此版本不支援 unixodbc-2.3.1 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
3.  在您的 Linux 電腦上執行命令： **tar 檔案解壓縮 xvzf unixodbc-2.3.0.tar.gz**。  
  
4.  切換至 unixODBC-2.3.0 目錄。  
  
5.  在命令提示字元中，執行下列命令： **CPPFLAGS ="-DSIZEOF_LONG_INT = 8"**。  
  
6.  在命令提示字元中，執行下列命令：**匯出 CPPFLAGS**。  
  
7.  在命令提示字元中，執行下列命令： **"。 / 設定-前置詞 = usr-libdir = / usr/lib64-sysconfdir = / 等等-啟用 gui = 否-啟用驅動程式 = 否-啟用 iconv-與-iconv-char-enc = UTF8-與-iconv-ucode-enc = UTF16LE"**.  
  
8.  在命令提示字元 （登入為根），執行下列命令：**進行**。  
  
9. 在命令提示字元 （登入為根），執行下列命令：**做安裝**。  

您現在已可開始安裝驅動程式。 如需詳細資訊，請參閱[安裝的 Microsoft ODBC Driver for SQL Server on Linux 及 macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱
[安裝的 Microsoft ODBC Driver for SQL Server on Linux 及 macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[此驅動程式版本的已知問題](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[版本資訊](../../../connect/odbc/linux-mac/release-notes.md)
