---
title: 下載並安裝 Microsoft SQL Operations Studio (preview) |Microsoft 文件
description: 下載和安裝 Microsoft SQL Operations Studio (preview) for Windows、 macOS 或 Linux
ms.custom: tools|sos
ms.date: 05/08/2018
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
ms.openlocfilehash: dcf6f9d14efd903c47d4e3b059503fb77606209b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="download-and-install-sql-operations-studio-preview"></a>下載並安裝 SQL Operations Studio (preview)

[!INCLUDE[name-sos](../includes/name-sos.md)] 在 Windows、 macOS 和 Linux 上執行。

下載並安裝最新版本中，*5 月公開預覽版*:

|平台|下載|發行日期| 版本 |
|:---|:---|:---|:---|
|Windows|[安裝程式](https://go.microsoft.com/fwlink/?linkid=873386)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=873387)|2018 年 5 月 7 日 |0.29.3|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=873388)|2018 年 5 月 7 日 |0.29.3|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=873391)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=873390)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=873389)|2018 年 5 月 7 日 |0.29.3|

如需最新版本的詳細資訊，請參閱[版本資訊](release-notes.md)。

## <a name="get-sql-operations-studio-preview-for-windows"></a>取得 SQL Operations Studio (preview) for Windows

這一版的[!INCLUDE[name-sos](../includes/name-sos-short.md)]包括標準的 Windows 安裝程式經驗，以及.zip: 

**安裝程式**

1. 下載並執行[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows 安裝程式](https://go.microsoft.com/fwlink/?linkid=873386)。
1. 啟動[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]應用程式。


**.zip 檔案**

1. 下載[[!INCLUDE[name-sos](../includes/name-sos-short.md)]適用於 Windows 的.zip](https://go.microsoft.com/fwlink/?linkid=873387)。
2. 瀏覽至下載的檔案，並將它解壓縮。
3. 執行 `\sqlops-windows\sqlops.exe`


## <a name="get-sql-operations-studio-preview-for-macos"></a>取得 macOS SQL Operations Studio (preview)

1. 下載[[!INCLUDE[name-sos](../includes/name-sos-short.md)]如 macOS](https://go.microsoft.com/fwlink/?linkid=873388)。
2. 若要展開的 zip 內容，請按兩下它。
3. 讓[!INCLUDE[name-sos](../includes/name-sos-short.md)]用於*啟動控制板*，拖曳*sqlops.app*至*應用程式*資料夾。


## <a name="get-sql-operations-studio-preview-for-linux"></a>取得 SQL Operations Studio (preview) for Linux

1. 下載[!INCLUDE[name-sos](../includes/name-sos-short.md)]適用於 Linux 使用其中一種安裝程式或.tar.gz 封存：
    - [.deb](https://go.microsoft.com/fwlink/?linkid=873391)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=873390)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=873389)
1. 擷取檔案和啟動[!INCLUDE[name-sos](../includes/name-sos-short.md)]，開啟新的終端機視窗，然後輸入下列命令：

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

   **.tar.gz 安裝：**
   ```bash 
   cd ~ 
   cp ~/Downloads/sqlops-linux-<version string>.tar.gz ~ 
   tar -xvf ~/sqlops-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/sqlops-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   sqlops 
   ``` 

   > [!NOTE]
   > 在 Debian、 Redhat 和 Ubuntu，您可能遺失相依性。 若要安裝這些相依性，根據您的 Linux 版本中使用下列命令：
   

   **Debian:** 
   ```bash
   sudo apt-get install libuwind8
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

如果您已安裝[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]使用 Windows installer，然後解除安裝移除所有 Windows 應用程式的方式相同。

如果您已安裝[!INCLUDE[name-sos-short](../includes/name-sos-short.md)].zip 或其他封存，然後只要刪除檔案。

## <a name="supported-operating-systems"></a>支援的作業系統

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 在 Windows、 macOS 和 Linux 上執行，並支援下列平台：

### <a name="windows"></a>視窗
- Windows 10 (64 位元)
- Windows 8.1 (64 位元)
- Windows 8 (64 位元)
- Windows 7 (SP1) （64 位元）-需要[KB2533623](https://www.microsoft.com/en-us/download/details.aspx?id=26767)
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
若要檢查最新的更新，請按一下 的視窗，然後按一下左下角的齒輪圖示**檢查更新**

## <a name="next-steps"></a>後續步驟

請參閱下列快速入門，若要開始使用其中一項：
- [連接及查詢 SQL Server](quickstart-sql-server.md)
- [連接及查詢 Azure SQL Database](quickstart-sql-database.md)
- [連接及查詢 Azure 資料倉儲](quickstart-sql-dw.md)

參與[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio) 

[Microsoft 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=521839)和[使用量資料收集](usage-data-collection.md)。
