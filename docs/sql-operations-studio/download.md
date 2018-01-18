---
title: "下載並安裝 Microsoft SQL 作業 Studio （預覽） |Microsoft 文件"
description: "下載和安裝 Microsoft SQL 作業 Studio （預覽） for Windows、 macOS 或 Linux"
ms.custom: tools|sos
ms.date: 01/17/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0621d5af62b5f5b8b694d47cf16d766215a0c819
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="download-and-install-sql-operations-studio-preview"></a>下載並安裝 SQL 作業 Studio （預覽）

[!INCLUDE[name-sos](../includes/name-sos.md)]在 Windows、 macOS 和 Linux 上執行。

下載並安裝最新版本中，*年 1 月公用預覽*:

|平台|下載|發行日期|
|:---|:---|:---|
|視窗|[安裝程式](https://go.microsoft.com/fwlink/?linkid=866480)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=866479)|2018 年 1 月 17 日 |
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=866481)|2018 年 1 月 17 日 |
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=866484)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=866483)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=866482)|2018 年 1 月 17 日|

如需最新版本的詳細資訊，請參閱[版本資訊](release-notes.md)。

## <a name="get-sql-operations-studio-preview-for-windows"></a>取得 SQL 作業 Studio （預覽） for Windows

這一版的[!INCLUDE[name-sos](../includes/name-sos-short.md)]包括標準的 Windows 安裝程式經驗，以及.zip: 

**安裝程式**

1. 下載並執行[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows 安裝程式](https://go.microsoft.com/fwlink/?linkid=866480)。
1. 啟動[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]應用程式。


**.zip 檔案**

1. 下載[[!INCLUDE[name-sos](../includes/name-sos-short.md)]適用於 Windows 的.zip](https://go.microsoft.com/fwlink/?linkid=866479)。
2. 瀏覽至下載的檔案，並將它解壓縮。
3. 執行 `\sqlops-windows\sqlops.exe`


## <a name="get-sql-operations-studio-preview-for-macos"></a>取得 macOS SQL 作業 Studio （預覽）

1. 下載[[!INCLUDE[name-sos](../includes/name-sos-short.md)]如 macOS](https://go.microsoft.com/fwlink/?linkid=866481)。
2. 若要展開的 zip 內容，請按兩下它。
3. 讓[!INCLUDE[name-sos](../includes/name-sos-short.md)]用於*啟動控制板*，拖曳*sqlops.app*至*應用程式*資料夾。


## <a name="get-sql-operations-studio-preview-for-linux"></a>取得 SQL 作業 Studio （預覽） for Linux

1. 下載[[!INCLUDE[name-sos](../includes/name-sos-short.md)]適用於 Linux](https://go.microsoft.com/fwlink/?linkid=866482)。
1. 擷取檔案和啟動[!INCLUDE[name-sos](../includes/name-sos-short.md)]，開啟新的終端機視窗，然後輸入下列命令：

   ```bash
   cd ~
   cp ~/Downloads/sqlops-linux-<version string>.tar.gz ~
   tar -xvf ~/sqlops-linux-<version string>.tar.gz
   echo 'export PATH="$PATH:~/sqlops-linux-x64"' >> ~/.bashrc
   source ~/.bashrc
   sqlops
   ```

   > [!NOTE]
   > 在 Ubuntu 及 Redhat，您可能遺失相依性。 若要安裝這些相依性，根據您的 Linux 版本中使用下列命令：
   
   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

   **Redhat:** 
   ```bash
   yum install libXScrnSaver
   ```

## <a name="uninstall-sql-operations-studio-preview"></a>解除安裝 SQL 作業 Studio （預覽）

如果您已安裝[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]使用 Windows installer，然後解除安裝移除所有 Windows 應用程式的方式相同。

如果您已安裝[!INCLUDE[name-sos-short](../includes/name-sos-short.md)].zip 或其他封存，然後只要刪除檔案。

## <a name="supported-operating-systems"></a>支援的作業系統

[!INCLUDE[name-sos](../includes/name-sos-short.md)]在 Windows、 macOS 和 Linux 上執行，並支援下列平台：

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
- macOS 10.13 高利也
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04



## <a name="next-steps"></a>後續步驟

請參閱下列快速入門，若要開始使用其中一項：
- [連接及查詢 SQL Server](quickstart-sql-server.md)
- [連接及查詢 Azure SQL Database](quickstart-sql-database.md)
- [連接及查詢 Azure 資料倉儲](quickstart-sql-dw.md)

參與[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio) 

[Microsoft 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=521839)和[使用量資料收集](usage-data-collection.md)。
