---
title: 下載並安裝 Microsoft SQL Operations Studio (preview) |Microsoft 文件
description: 下載和安裝 Microsoft SQL Operations Studio (preview) for Windows、 macOS 或 Linux
ms.custom: tools|sos
ms.date: 08/30/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30eea457bdba7ac671829bb02f01152235babaf3
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348649"
---
# <a name="download-and-install-sql-operations-studio-preview"></a>下載並安裝 SQL Operations Studio (preview)

[!INCLUDE[name-sos](../includes/name-sos.md)] 在 Windows、 macOS 和 Linux 上執行。

下載並安裝最新版本中，*年 8 月公開預覽*:

|平台|下載|發行日期| 版本 |
|:---|:---|:---|:---|
|Windows|[安裝程式](https://go.microsoft.com/fwlink/?linkid=2013365)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2013712)|2018 年 8 月 30日日 |0.32.8|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2013715)|2018 年 8 月 30日日 |0.32.8|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2013833)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2013830)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2013718)|2018 年 8 月 30日日 |0.32.8|

如需最新版本的詳細資訊，請參閱[版本資訊](release-notes.md)。

## <a name="get-sql-operations-studio-preview-for-windows"></a>在 Windows 上取得 SQL Operations Studio (preview)

這一版的[!INCLUDE[name-sos](../includes/name-sos-short.md)]包括標準的 Windows 安裝程式體驗，以及用.zip 格式： 

**安裝程式**

1. 下載並執行[[!INCLUDE[name-sos](../includes/name-sos-short.md)]適用於 Windows 安裝程式](https://go.microsoft.com/fwlink/?linkid=2013365)。
1. 啟動[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]應用程式。


**.zip 檔案**

1. 下載[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows 的.zip](https://go.microsoft.com/fwlink/?linkid=2013712)。
2. 瀏覽至下載的檔案，並將它解壓縮。
3. 執行 `\sqlops-windows\sqlops.exe`


## <a name="get-sql-operations-studio-preview-for-macos"></a>在 macOS 上取得 SQL Operations Studio (preview)

1. 下載[[!INCLUDE[name-sos](../includes/name-sos-short.md)]適用於 macOS](https://go.microsoft.com/fwlink/?linkid=2013715)。
2. 若要展開的 zip 的內容，請按兩下它。
3. 若要讓[!INCLUDE[name-sos](../includes/name-sos-short.md)]中可用*Launchpad*，拖曳*sqlops.app*來*應用程式*資料夾。


## <a name="get-sql-operations-studio-preview-for-linux"></a>在 Linux 上取得 SQL Operations Studio (preview)

1. 下載[!INCLUDE[name-sos](../includes/name-sos-short.md)]適用於 Linux 使用其中一種安裝程式或.tar.gz 下載封存：
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2013833)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2013830)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2013718)
1. 擷取檔案，並啟動[!INCLUDE[name-sos](../includes/name-sos-short.md)]，開啟新的終端機視窗，並輸入下列命令：

   **Debian 安裝：**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/sqlops-linux-<version string>.deb

   sqlops
   ```

   **rpm 安裝：**
   ```bash
   cd ~
   yum install ./Downloads/sqlops-linux-<version string>.rpm

   sqlops
   ```

   **.tar.gz 下載安裝：**
   ```bash 
   cd ~ 
   cp ~/Downloads/sqlops-linux-<version string>.tar.gz ~ 
   tar -xvf ~/sqlops-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/sqlops-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   sqlops 
   ``` 

   > [!NOTE]
   > 在 Debian、 Redhat 和 Ubuntu 上，您可能有遺失相依性。 若要安裝這些相依性，視您的 Linux 版本而定，使用下列命令：
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **Redhat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```


## <a name="uninstall-sql-operations-studio-preview"></a>解除安裝 SQL Operations Studio (preview)

如果您已使用 Windows installer 安裝[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，解除安裝方式與所有 Windows 應用程式移除方式相同。

如果您使用.zip 或其他封存安裝[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，只要刪除檔案即可。

## <a name="supported-operating-systems"></a>支援的作業系統

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 在 Windows、 macOS 和 Linux 上執行，而且支援下列平台：

### <a name="windows"></a>視窗
- Windows 10 (64 位元)
- Windows 8.1 (64 位元)
- Windows 8 (64 位元)
- Windows 7 (SP1) （64 位元）： 需要[KB2533623](https://www.microsoft.com/en-us/download/details.aspx?id=26767)
- Windows Server 2016
- Windows Server 2012 R2 (64 位元)
- Windows Server 2012 (64 位元)
- Windows Server 2008 R2 (64 位元)

### <a name="macos"></a>macOS
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="check-for-updates"></a>檢查更新
若要檢查最新的更新，請按一下 的視窗，然後按一下左下方的齒輪圖示**檢查更新**

## <a name="next-steps"></a>後續步驟

請參閱下列快速入門，以開始使用其中一項：
- [連線與查詢 SQL Server](quickstart-sql-server.md)
- [連線與查詢 Azure SQL Database](quickstart-sql-database.md)
- [連線與查詢 Azure 資料倉儲](quickstart-sql-dw.md)

參與[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio) 

[Microsoft 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=521839)並[使用量資料收集](usage-data-collection.md)。
