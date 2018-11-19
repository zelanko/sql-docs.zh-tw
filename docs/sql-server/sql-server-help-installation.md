---
title: SQL Server 說明內容和說明檢視器 | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2017
ms.prod: sql
ms.technology: ''
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9a1ae0aac049fef58d8007c26dce6ce355344a6
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51700526"
---
# <a name="sql-server-offline-help-and-help-viewer"></a>SQL Server 離線說明和說明檢視器

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

您可以使用 SQL Server Management Studio (SSMS) 或 Visual Studio (VS) 中的說明檢視器，從線上來源或磁碟下載並安裝 SQL Server 說明套件，以及進行離線檢視。 本文描述可安裝說明檢視器的工具、如何安裝離線說明內容，以及如何檢視 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]、SQL Server 2016 和 SQL Server 2017 的說明。

> [!NOTE]
> 結合 SQL Server 2016 和 SQL Server 2017 說明，雖然有些主題適用於特別註記的個別版本。 大部分主題都適用於兩者。

## <a name="install-the-help-viewer"></a>安裝說明檢視器

說明檢視器有兩個版本：v2.x 支援 SQL Server 2016/SQL Server 2017 說明，而 v1.x 支援 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 說明。 說明檢視器不支援 Proxy 設定，且不支援 ISO 格式。 

下列工具會安裝說明檢視器： 

|**安裝說明檢視器的工具**|**安裝的說明檢視器版本**|
|---------|---------|
|[SQL Server Management Studio 17.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)| v2.2|
|[SQL Server Data Tools for Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)| v2.2|
|Visual Studio 2017* | v2.3|
|Visual Studio 2015 | v2.2|
|SQL Server 2014 Management Studio | v1.x|
|舊版 Visual Studio | v1.x|
|SQL Server 2016 | v1.x|

\* 若要使用 Visual Studio 2017 安裝說明檢視器，請在 Visual Studio 安裝程式的 [個別元件] 索引標籤上選取 [程式碼工具] 下方的 [說明檢視器]，然後按一下 [安裝]。 

>[!NOTE]
> - SQL Server 2016 安裝說明檢視器 1.1，其不支援 SQL Server 2016 說明。 
> - 安裝 SQL Server 2017 時不會安裝任何說明檢視器。
> - 如果您從磁碟安裝內容，則說明檢視器 v2.x 也可以支援 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 說明。

## <a name="use-help-viewer-v2x"></a>使用說明檢視器 v2.x

SSMS 17.x 以及 VS 2015 和 2017 使用說明檢視器 2.x，其支援 SQL Server 2016/2017 說明。 

**使用說明檢視器 v2.x 下載並安裝離線說明內容**

1. 在 SSMS 或 VS 中，按一下 [說明] 功能表上的 [新增和移除說明內容]。 

   ![HelpViewer2 新增移除內容](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

   說明檢視器會開啟至 [管理內容] 索引標籤。  
   
2. 若要安裝最新說明內容套件，請選擇 [安裝來源] 下方的 [線上]。
   
   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)  
   
   >[!NOTE]
   > 若要從磁碟進行安裝 (SQL Server 2014 說明)，請選擇 [安裝來源] 下的 [磁碟]，並指定磁碟位置。
   
   [管理內容] 索引標籤上的 [本機存放區路徑] 會顯示本機電腦上安裝內容的位置。 如果您想要變更位置，請按一下 [移動]，並在 [到] 欄位中輸入不同資料夾路徑，然後按一下 [確定]。
   如果說明安裝在變更本機存放區路徑後失敗，請關閉並重新開啟說明檢視器，並確保新的位置出現在本機存放區路徑中，然後重試安裝。

3. 按一下您想要安裝的每個內容套件 (書籍) 旁邊的 [新增]。 
   若要安裝所有 SQL Server 說明內容，請新增 SQL Server 下的全部 13 本書籍。 
   
4. 按一下右下方的 [更新]。 
   會使用新增的書籍自動更新左側的說明目錄。 
   
   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)     
   
> [!NOTE]
> 並非 SQL Server 目錄中的所有頂端節點標題都完全符合對應可下載說明書籍的名稱。 TOC 標題對應至書籍名稱，如下所示：

| 內容窗格 | SQL Server 書籍 |
|-----|-----|
|Analysis Services 語言參考 | Analysis Services (MDX) 語言參考|
|Data Analysis Expressions (DAX) 參考 | Data Analysis Expressions (DAX) 參考|
|資料採礦延伸模組 (DMX) 參考 | 資料採礦延伸模組 (DMX) 參考|
|適用於 SQL Server 的開發人員指南 | SQL Server 開發人員參考資料|
|下載 SQL Server Management Studio | SQL Server Management Studio|
|開始使用 SQL Server 中的機器學習 | Microsoft Machine Learning 服務|
|Power Query M 參考 | Power Query M 參考|
|SQL Server 驅動程式 | SQL Server 連線驅動程式|
|Linux 上的 SQL Server | Linux 上的 SQL Server|
|SQL Server 技術文件 | SQL Server 技術文件 (SSIS、SSRS、資料庫引擎、設定)|
|Azure SQL Database 的工具和公用程式 | SQL Server 工具|
|Transact-SQL 參考 (資料庫引擎) | Transact-SQL 參考|
|Xquery 語言參考 (SQL Server) | Xquery 語言參考 (SQL Server)|

> [!NOTE]
> 如果說明檢視器在新增內容時凍結 (擱置)，請將 %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings 或 HlpViewer_VisualStudiox_en-US.settings 檔案中的 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 行變更為未來的某個日期。 如需此問題的詳細資訊，請參閱 [Visual Studio 說明檢視器凍結在啟動顯示畫面上](/visualstudio/welcome-to-visual-studio)。

**使用說明檢視器 v2.x 在 SSMS 中檢視離線說明內容**

若要在 SSMS 中檢視已安裝的說明，請按 CTRL + ALT + F1，或選擇 [說明] 功能表中的 [新增或移除內容]，以啟動說明檢視器。 

   ![HelpViewer2 新增移除內容](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

說明檢視器會開啟到 [管理內容] 索引標籤，並在左窗格中顯示已安裝的說明目錄。 按一下目錄中的主題，以將它們顯示在右窗格中。 
> [!TIP]
> 如果看不到內容窗格，請按一下左邊界的 [內容]。 按一下圖釘圖示，以保持開啟的內容窗格。  

   ![含內容的說明檢視器 v2.x](../sql-server/media/sql-server-help-installation/helpviewer2-withcontentinstalled.png)

**使用說明檢視器 v2.x 在 VS 中檢視離線說明內容**

在 Visual Studio 中檢視已安裝的說明：
1. 指向 [說明] 功能表上的 [設定說明喜好設定]，然後選擇 [在說明檢視器中啟動]。 

   ![VS 說明檢視設定喜好設定說明檢視器](../sql-server/media/sql-server-help-installation/launchviewer.png)

2. 按一下 [說明] 功能表中的 [檢視說明]，以在說明檢視器中顯示內容。 

   ![檢視說明](../sql-server/media/sql-server-help-installation/viewhelp.png)

   說明目錄會顯示在左側，並在右側顯示選取的說明主題。 
   
## <a name="use-help-viewer-v1x"></a>使用說明檢視器 v1.x

舊版 SSMS 和 VS 使用說明檢視器 1.x，其支援 SQL Server 2014 說明。 

**使用說明檢視器 v1.x 下載並安裝離線說明內容**

此程序使用說明檢視器 1.x 從 Microsoft 下載中心下載 SQL Server 2014 說明，並將它安裝在電腦上。

1. 巡覽至 [Microsoft SQL Server 2014 的產品文件](https://www.microsoft.com/download/details.aspx?id=42557)下載網站，然後按一下 [下載]。  
2. 按一下訊息方塊中的 [儲存]，將 *SQLServer2014Documentation\_\*.exe* 檔案儲存至電腦。  
   
   >[!NOTE]
   >針對防火牆或 Proxy 受限的環境，將下載儲存到可攜至環境中的 USB 磁碟機或其他可攜式媒體。   
   
3. 按兩下 .exe 以解壓縮說明內容檔案，並將檔案儲存至本機或共用資料夾。  
4. 啟動 SSMS 或 VS，並按一下 [說明] 功能表上的 [管理說明設定]，來開啟 [Help Library 管理員]。  
5. 按一下 [從磁碟安裝內容]，然後瀏覽至要解壓縮說明內容檔的資料夾。  
   
   ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-installfromdisk.png)
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog1.png)
   
   > [!IMPORTANT]
   > 若要避免安裝只有部分目錄的本機說明內容，您必須使用 [Help Library 管理員] 中的 [從磁碟安裝內容] 選項。  如果您已使用 [從線上安裝內容]，而說明檢視器顯示部分目錄，請參閱這篇[部落格文章](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/)以取得疑難排解步驟。 
   
8. 按一下 HelpContentSetup.msha 檔案、按一下 [開啟]，然後按 [下一步]。  
9. 按一下要安裝之文件旁邊的 [加入]，然後按一下 [更新]。  
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog2.png)  
   
10. 按一下 [完成]，然後按一下 [結束]。

**使用說明檢視器 v1.x 檢視離線說明內容**

11. 若要檢視已安裝的說明，請開啟 [Help Library 管理員]，並按一下 [選擇線上或本機說明]，然後按一下 [I want to use local help] (我要使用本機說明)。
12. 按一下 [說明] 功能表上的 [檢視說明]，開啟說明檢視器查看內容。 您已安裝的內容會列在左窗格中。  
   
   ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/sql-server-help-installation/helpviewer1-withcontentinstalled-zoomedin.png)  
   
## <a name="view-online-help"></a>檢視線上說明

線上說明一律會顯示最新內容。 

**在 SSMS 17.x 中檢視 SQL Server 線上說明**

- 在 [說明] 功能表中，按一下 [檢視說明]。 來自 [https://docs.microsoft.com/sql/ https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation) 的最新 SQL Server 2016/2017 文件即會在瀏覽器中顯示。 

   ![檢視說明](../sql-server/media/sql-server-help-installation/viewhelp.png)

**在 Visual Studio 中檢視 Visual Studio 線上說明**

1. 指向 [說明] 功能表上的 [設定說明喜好設定]，然後選擇 [在瀏覽器中啟動] 或 [在說明檢視器中啟動]。 
2. 在 [說明] 功能表中，按一下 [檢視說明]。 最新的 Visual Studio 說明會顯示在選擇的環境中。 

**使用說明檢視器 v1.x 檢視線上說明**

1. 按一下 [說明] 功能表上的 [管理說明設定]，來開啟 [Help Library 管理員]。  
2. 在 [Help Library 管理員] 對話方塊中，按一下 [選擇線上或本機說明]。  
   
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
   
3. 依序按一下 [I want to use online help] (我要使用線上說明)、[確定] 和 [結束]。  
   
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/sql-server-help-installation/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)
   
4. 按一下 [說明] 功能表上的 [檢視說明]，開啟說明檢視器查看內容。 

## <a name="view-f1-help"></a>檢視 F1 說明

如果按 F1 或按一下 [說明] 或 **?** 圖示 (位在 SSMS 或 VS 的對話方塊中)，即時線上說明主題會出現在瀏覽器或說明檢視器中。 

**檢視 F1 說明**

1. 指向 [說明] 功能表上的 [設定說明喜好設定]，然後選擇 [在瀏覽器中啟動] 或 [在說明檢視器中啟動]。 
2. 按 F1 或按一下 [說明] 或 **?** (位在它們可用的對話方塊中)，以查看所選擇環境中的即時線上主題。

>  [!NOTE]
>  只有在您於線上時，才能使用 F1 說明。 F1 說明沒有離線來源。 
   

## <a name="next-steps"></a>後續步驟
[Microsoft 說明檢視器 - Visual Studio](/visualstudio/ide/microsoft-help-viewer)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
