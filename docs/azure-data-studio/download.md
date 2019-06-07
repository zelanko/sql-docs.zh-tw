---
title: 下載並安裝
titleSuffix: Azure Data Studio
description: 下載並為 Windows 安裝 Azure 資料 Studio、 macOS 或 Linux
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: craigg
ms.custom: seodec18
ms.date: 06/06/2019
ms.reviewer: alayu; sstein
ms.openlocfilehash: 39985ea8a13b4102393434dd2ef0981fe022798f
ms.sourcegitcommit: 32dce314bb66c03043a93ccf6e972af455349377
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2019
ms.locfileid: "66744145"
---
# <a name="download-and-install-azure-data-studio"></a>下載並安裝 Azure Data Studio

[!INCLUDE[name-sos](../includes/name-sos.md)] 在 Windows、 macOS 和 Linux 上執行。


下載並安裝最新版本中， *6 月版次*:

> [!NOTE]
> 如果您正在從 SQL Operations Studio 更新，且想要保留您的設定、 鍵盤快速鍵或程式碼片段，請參閱[移動使用者設定](#move-user-settings)。

|平台|下載|發行日期| 版本 |
|:---|:---|:---|:---|
|視窗|[使用者安裝程式 （建議選項）](https://go.microsoft.com/fwlink/?linkid=2094100)<br>[系統安裝程式](https://go.microsoft.com/fwlink/?linkid=2094200)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2094201)|2019 年 6 月 6日日 |1.8.0|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2094202)|2019 年 6 月 6日日 |1.8.0|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2094203)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2094102)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2094101)|2019 年 6 月 6日日 |1.8.0|

如需最新版本的詳細資訊，請參閱[版本資訊](release-notes.md)。

## <a name="get-azure-data-studio-for-windows"></a>取得適用於 Windows 的 Azure Data Studio

這一版的[!INCLUDE[name-sos](../includes/name-sos-short.md)]包括標準的 Windows 安裝程式體驗，以及一個.zip 檔案。

*使用者安裝程式*建議，因為它不需要系統管理員權限，可簡化安裝和升級。 使用者安裝程式不需要系統管理員權限，因為這個位置是 [使用者] 本機 AppData (LOCALAPPDATA) 資料夾下。 使用者安裝程式也提供順暢的背景更新體驗。 如需詳細資訊，請參閱 <<c0> [ 的 Windows 使用者設定](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows)。


**使用者安裝程式**（建議選項）

1. 下載並執行[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *使用者*針對 Windows installer](https://go.microsoft.com/fwlink/?linkid=2094100)。
2. 啟動[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]應用程式。

**系統安裝程式**

1. 下載並執行[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *系統*針對 Windows installer](https://go.microsoft.com/fwlink/?linkid=2094200)。
2. 啟動[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]應用程式。


**壓縮檔**

1. 下載[ [!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows 的.zip](https://go.microsoft.com/fwlink/?linkid=2094201)。
2. 瀏覽至下載的檔案，並將它解壓縮。
3. 執行 `\azuredatastudio-windows\azuredatastudio.exe`


## <a name="get-azure-data-studio-for-macos"></a>取得適用於 macOS 的 Azure Data Studio

1. 下載[[!INCLUDE[name-sos](../includes/name-sos-short.md)]適用於 macOS](https://go.microsoft.com/fwlink/?linkid=2094202)。
2. 若要展開的 zip 的內容，請按兩下它。
3. 若要讓[!INCLUDE[name-sos](../includes/name-sos-short.md)]中可用*Launchpad*，拖曳*Azure 資料 Studio.app*來*應用程式*資料夾。


## <a name="get-azure-data-studio-for-linux"></a>取得適用於 Linux 的 Azure 資料 Studio

1. 下載[!INCLUDE[name-sos](../includes/name-sos-short.md)]適用於 Linux 使用其中一種安裝程式或.tar.gz 下載封存：
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2094203)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2094102)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2094101)
1. 擷取檔案，並啟動[!INCLUDE[name-sos](../includes/name-sos-short.md)]，開啟新的終端機視窗，並輸入下列命令：

   **Debian 安裝：**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **rpm 安裝：**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **.tar.gz 下載安裝：**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > 在 Debian、Redhat 和 Ubuntu 上，您可能遺失相依性。 使用下列命令，根據您的 Linux 版本安裝這些相依性：
   

   **Debian：** 
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


## <a name="uninstall-azure-data-studio"></a>Azure Data Studio 解除安裝

如果您已使用 Windows installer 安裝[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，解除安裝方式與所有 Windows 應用程式移除方式相同。

如果您使用.zip 或其他封存安裝[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，只要刪除檔案即可。

## <a name="supported-operating-systems"></a>支援的作業系統

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 在 Windows、 macOS 和 Linux 上執行，而且支援下列平台：

### <a name="windows"></a>視窗
- Windows 10 (64 位元)
- Windows 8.1 (64 位元)
- Windows 8 (64 位元)
- Windows 7 (SP1) （64 位元）： 需要[KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
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

## <a name="recommended-system-requirements"></a>建議的系統需求
以獲得最佳的體驗，請使用建議的系統需求。
[量化記憶體需要以下的更新]

|             | CPU 核心 | 記憶體/RAM |
|:-----------|:---------|:----------|
| 建議 |     4     |      8 GB    |
|   最小值   |     2     |      4 GB     |
|             |           |            |

## <a name="check-for-updates"></a>檢查更新
若要檢查最新的更新，請按一下 的視窗，然後按一下左下方的齒輪圖示**檢查更新**

## <a name="supported-sql-offerings"></a>支援的 SQL 供應項目

* 這個版本的 Azure Data Studio 適用於所有[支援的 SQL Server 2014-版本[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)並提供支援使用 Azure SQL Database 和 Azure SQL 資料倉儲中最新的雲端功能。 Azure Data Studio 也提供 Azure SQL 受控執行個體的預覽支援。

## <a name="upgrade-from-sql-operations-studio"></a>從 SQL Operations Studio 升級

如果您仍在使用 SQL Operations Studio，您需要升級至 Azure Data Studio。 SQL Operations Studio 是預覽名稱和 Azure Data Studio 預覽版本。 在 2018 年 9 月中，我們[將名稱變更為 Azure Data Studio](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/)和發行的公開上市 (GA) 版本。 因為 SQL Operations Studio 是不會再更新或支援，我們要求所有的 SQL Operations Studio 使用者下載最新版的 Azure Data Studio，以取得最新功能，也就是安全性更新和修正。
 
當從舊的預覽版本升級到最新的 Azure Data Studio，您將會遺失您目前的設定和延伸模組。 若要移動您的設定，請依照下列中的指示*移動使用者設定*區段：


## <a name="move-user-settings"></a>移動使用者設定

如果您想要移動您的自訂設定、 鍵盤快速鍵或程式碼片段，請遵循下列步驟。 這很重要，如果您從 SQL Operations Studio 版本升級至 Azure Data Studio。

*如果您已經有 Azure Data Studio，或您永遠不會安裝或自訂 SQL Operations Studio，您可以忽略這一節。*


1. 開啟 [設定]，請按一下左下方的齒輪，然後按一下**設定。**

   ![開啟設定](./media/download/open-settings.png)

2. 以滑鼠右鍵按一下**使用者設定**索引標籤上，按一下**總管中顯示**

   ![reveal-in-explorer](./media/download/reveal-in-explorer.png)

3. 複製此資料夾中的所有檔案，並儲存成容易尋找相似的文件 資料夾的本機磁碟機上的位置。

   ![複製設定](./media/download/copy-settings.png)

4. 新版本的 Azure Data Studio，請遵循的步驟 1-2，然後針對步驟 3 將您儲存的內容貼到資料夾。 您可以手動複製設定、 按鍵繫結關係或在其各自的位置中的程式碼片段。

5. 如果覆寫現有的安裝，請刪除舊的安裝目錄，才能進行安裝，以避免資源總管 連接到您的 Azure 帳戶時發生錯誤。

## <a name="next-steps"></a>後續步驟

請參閱下列快速入門，以開始使用其中一項：
- [連線與查詢 SQL Server](quickstart-sql-server.md)
- [連線與查詢 Azure SQL Database](quickstart-sql-database.md)
- [連線與查詢 Azure 資料倉儲](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Microsoft 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=521839)並[使用量資料收集](usage-data-collection.md)。