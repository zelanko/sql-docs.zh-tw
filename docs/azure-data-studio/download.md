---
title: 下載並安裝
titleSuffix: Azure Data Studio
description: 下載並安裝適用於 Windows、macOS 或 Linux 的 Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.custom: seodec18
ms.date: 10/11/2019
ms.reviewer: alayu; sstein
ms.openlocfilehash: b7a9e9a13b5b19e2450ab1d4b12aea7a97cdc206
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313663"
---
# <a name="download-and-install-azure-data-studio"></a>下載並安裝 Azure Data Studio

[!INCLUDE[name-sos](../includes/name-sos.md)] 在 Windows、macOS 和 Linux 上執行。


請下載並安裝最新版的「十月版本」  ：

> [!NOTE]
> 如果您是從 SQL Operations Studio 更新，並想要保留您的設定、鍵盤快速鍵或程式碼片段，請參閱[移動使用者設定](#move-user-settings)。

|平台|下載|發行日期| 版本 |
|:---|:---|:---|:---|
|Windows|[使用者安裝程式 (建議)](https://go.microsoft.com/fwlink/?linkid=2105135)<br>[系統安裝程式](https://go.microsoft.com/fwlink/?linkid=2105134)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2104938)|2019 年 10 月 11 日 |1.12.2|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2105133)|2019 年 10 月 11 日 |1.12.2|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2105131)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2104937)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2105132)|2019 年 10 月 11 日 |1.12.2|

如需最新版本的詳細資訊，請參閱[版本資訊](release-notes.md)。

## <a name="get-azure-data-studio-for-windows"></a>取得適用於 Windows 的 Azure Data Studio

此版本的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 包含標準的 Windows 安裝程式體驗，以及 .zip 檔案。

建議使用「使用者安裝程式」  ，因為不需要系統管理員權限，從而簡化安裝和升級。 使用者安裝程式位於使用者的 Local AppData (LOCALAPPDATA) 資料夾底下，因此不需要系統管理員權限。 使用者安裝程式也提供更流暢的背景更新體驗。 如需詳細資訊，請參閱 [User setup for Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows) (適用於 Windows 的使用者安裝程式)。

**使用者安裝程式** (建議)

1. 下載並執行[適用於Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]「使用者」  安裝程式](https://go.microsoft.com/fwlink/?linkid=2105135)。
2. 啟動 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 應用程式。

**系統安裝程式**

1. 下載並執行[適用於Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]「系統」  安裝程式](https://go.microsoft.com/fwlink/?linkid=2105134)。
2. 啟動 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 應用程式。

**壓縮檔**

1. 下載[適用於 Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip](https://go.microsoft.com/fwlink/?linkid=2104938)。
2. 瀏覽至下載的檔案並解壓縮。
3. `\azuredatastudio-windows\azuredatastudio.exe`執行


## <a name="get-azure-data-studio-for-macos"></a>取得適用於 macOS 的 Azure Data Studio

1. 下載[適用於 macOS 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](https://go.microsoft.com/fwlink/?linkid=2105133)。
2. 若要展開壓縮檔的內容，請按兩下檔案。
3. 若要在「啟動控制板」  中提供 [!INCLUDE[name-sos](../includes/name-sos-short.md)]，請將 *Azure Data Studio.app* 拖曳至 [應用程式]  資料夾。


## <a name="get-azure-data-studio-for-linux"></a>取得適用於 Linux 的 Azure Data Studio

1. 使用其中一種安裝程式或 tar.gz 封存，下載適用於 Linux 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]：
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2105131)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2104937)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2105131)
1. 若要將檔案解壓縮並啟動 [!INCLUDE[name-sos](../includes/name-sos-short.md)]，請開啟新的終端視窗並鍵入下列命令：

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

   **tar.gz 安裝：**
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
## <a name="download-insiders-build-of-azure-data-studio"></a>下載 Azure Data Studio 的測試人員組建
一般而言，使用者應該下載上述穩定的 Azure Data Studio 版本。 不過，如果您想要試用搶鮮版 (Beta) 功能並提供意見反應，您可以下載 [Azure Data Studio 的測試人員組建](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)。

## <a name="uninstall-azure-data-studio"></a>解除安裝 Azure Data Studio

如果您使用 Windows 安裝程式安裝 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，請以移除其他 Windows 應用程式相同的方式解除安裝。

如果您使用 .zip 或其他封存安裝 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]，則只需刪除這些檔案即可。

## <a name="supported-operating-systems"></a>支援的作業系統

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 在 Windows、macOS 和 Linux 上執行，並支援下列平台：

### <a name="windows"></a>Windows
- Windows 10 (64 位元)
- Windows 8.1 (64 位元)
- Windows 8 (64 位元)
- Windows 7 (SP1) (64 位元) - 需要 [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2019
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

|             | CPU 核心 | 記憶體/RAM |
|:-----------|:---------|:----------|
| 建議 |     4     |      8 GB    |
|   最小值   |     2     |      4 GB     |
|             |           |            |

## <a name="check-for-updates"></a>檢查更新
若要檢查是否有最新的更新，請按一下視窗左下方的齒輪圖示，然後按一下 [檢查更新] 

## <a name="supported-sql-offerings"></a>支援的 SQL 供應項目

* 此版本的 Azure Data Studio 適用於所有 [SQL Server 2014 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的支援版本](https://support.microsoft.com/lifecycle?C2=1044)，並提供支援以使用 Azure SQL Database 和 Azure SQL 資料倉儲中的最新雲端功能。 Azure Data Studio 也提供 Azure SQL 受控執行個體的預覽支援。

## <a name="upgrade-from-sql-operations-studio"></a>從 SQL Operations Studio 升級

如果您仍在使用 SQL Operations Studio，您需要升級到 Azure Data Studio。 SQL Operations Studio 是 Azure Data Studio 的預覽名稱和預覽版本。 在 2018 年 9 月，我們[已將名稱變更為 Azure Data Studio](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/) 並發行正式運作 (GA) 版本。 因為 SQL Operations Studio 已不再更新或受支援，所以我們要求所有 SQL Operations Studio 使用者下載最新版的 Azure Data Studio，以便取得最新的功能、安全性更新和修正。
 
從舊版預覽升級到最新版的 Azure Data Studio 時，您將會遺失目前的設定和延伸模組。 若要移動您的設定，請遵循下一節＜移動使用者設定＞  中的指示：


## <a name="move-user-settings"></a>移動使用者設定

如果您想要移動自訂設定、鍵盤快速鍵或程式碼片段，請遵循下列步驟。 如果您要從 SQL Operations Studio 版升級到 Azure Data Studio，必須這麼做。

如果您已有 Azure Data Studio，或是從未安裝或自訂 SQL Operations Studio，則可以略過本節。 


1. 按一下左下方的齒輪，然後按一下 [設定]  ，開啟設定。

   ![開啟設定](./media/download/open-settings.png)

2. 以滑鼠右鍵按一下頂端的 [使用者設定]  索引標籤，然後按一下 [在總管中顯示] 

   ![在總管中顯示](./media/download/reveal-in-explorer.png)

3. 複製此資料夾中的所有檔案，然後儲存在本機磁碟上容易找到的位置 (例如 [文件] 資料夾)。

   ![複製設定](./media/download/copy-settings.png)

4. 在您的新版 Azure Data Studio 中，遵循步驟 1-2，然後在步驟 3 中，將您儲存的內容貼到資料夾。 您也可以將設定、按鍵繫結關係或程式碼片段手動複製到各自的位置。

5. 如果覆寫現有的安裝，請在安裝前先刪除舊的安裝目錄，以避免在連線到資源總管中的 Azure 帳戶時發生錯誤。

## <a name="next-steps"></a>Next Steps

若要開始使用，請參閱下列其中一個快速入門：
- [連線與查詢 SQL Server](quickstart-sql-server.md)
- [連線與查詢 Azure SQL Database](quickstart-sql-database.md)
- [連線與查詢 Azure 資料倉儲](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Microsoft 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=521839)和[使用方式資料收集](usage-data-collection.md)。
