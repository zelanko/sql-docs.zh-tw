---
title: "SQL Server 說明檢視器與離線內容 | Microsoft Docs"
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
ms.translationtype: HT
ms.sourcegitcommit: aad94f116c1a8b668c9a218b32372424897a8b4a
ms.openlocfilehash: ca52d53cf25fa0ead6abd9b870f4d8dab424d11a
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="help-viewer-and-offline-content-for-sql-server"></a>SQL Server 說明檢視器與離線內容
  
  
  
本文示範如何安裝說明檢視器，以及離線檢視 SQL Server 文件。 本文涵蓋 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]、SQL Server 2016 和 SQL Server 2017 的文件。 

## <a name="install-help-viewer"></a>安裝說明檢視器
下表列出安裝說明檢視器的工具，視所用 SQL Server 版本而定。 請安裝所列工具之一以安裝說明檢視器。


|**SQL Server 版本**|**安裝說明檢視器的工具**|**安裝的說明檢視器版本**|
|---------|---------|---------|
|SQL Server 2017<br>SQL Server 2016     |   [最新版的 SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)<br><br>[最新版的 SQL Server Data Tools for Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)<br><br>Visual Studio 2017 (*僅支援 SQL Server 2016*)  |  v2.x       |
|SQL Server 2014    | SQL Server 2014 Management Studio<br><br>Visual Studio 2012 以前的 Visual Studio 版本        |  v1.x       |


> [!IMPORTANT]
> SQL Server 2016 安裝的說明檢視器 1.1，無法用來檢視 SQL Server 2016 和 2017 的文件。
> <br>
> <br>
> SQL Server 2017 不安裝說明檢視器。
> <br>
> <br>
> 若要使用 Visual Studio 2017 安裝說明檢視器，請按一下 **Visual Studio 安裝程式**程式的 [個別元件] 索引標籤，按一下 [程式碼工具] 類別目錄的 [說明檢視器]，然後按一下 [安裝]。 
> <br>
> <br>
> 只有當您**從磁碟安裝內容**時，才能使用說明檢視器 2.x 檢視 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 的本機說明。 


## <a name="sql-server-2016-sql-server-2017-offline-content"></a>SQL Server 2016、SQL Server 2017 離線內容  
 
**安裝離線內容**  
1. 藉由啟動 SQL Server Management Studio 或 Visual Studio，然後按一下 [說明] 功能表上的 [新增和移除說明內容]，來開啟說明檢視器。  
2. 按一下 [管理內容] 索引標籤。  
3. 若要從線上來源安裝說明，按一下 [安裝來源] 區域中的 [線上]。  
![HelpViewer2_ManageContent_OnlineSource](../release-notes/media/helpviewer2-managecontent-onlinesource.png)  
7. 按一下要安裝之文件旁邊的 [加入]，然後按一下 [更新]。  
![HelpViewer2_ManageContent_AddContent](../release-notes/media/helpviewer2-managecontent-addcontent.png)     
  
   >[!IMPORTANT] 
   >在 SQL Server Management Studio 和 Visual Studio 中，加入文件程序期間可能會凍結 (擱置) 說明檢視器應用程式。 若要解決此問題，請執行下列作業。 如需此問題的詳細資訊，請參閱 [Visual Studio 說明檢視器凍結在啟動顯示畫面上](https://msdn.microsoft.com/library/mt654096.aspx)。  
   >>以 [記事本] 開啟 %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings 檔案，將下列程式碼中的日期變更為未來的日期。 只有當您已安裝 Visual Studio 時，才能在您的本機電腦上使用這個檔案。 
   >>>Cache LastRefreshed="12/31/2017 00:00:00"  
  
    左窗格中的目錄會自動更新以包含您已加入的文件。  
![HelpViewer2_withContentInstalled](../release-notes/media/helpviewer2-withcontentinstalled.png)

1. (選擇性) [管理內容] 索引標籤上的 [本機存放區路徑] 索引標籤會顯示本機電腦上安裝文件的位置。 若要將文件移至不同的位置，按一下 [移動]、在 [移動內容] 對話方塊的 [至] 欄位中輸入資料夾路徑，然後按一下 [確定]。

   ![HelpViewer2_Move Content Dialog](../release-notes/media/helpviewer2-move-content-dialog.png)

   移動內容之後，新的位置就會顯示在 [本機存放區路徑] 中。
      
   >[!IMPORTANT]
   > 如果出現訊息指出移動操作失敗，請關閉訊息方塊、關閉說明檢視器，然後重新開啟說明檢視器。 內容的新位置現在應該會出現在 [本機存放區路徑] 中。   
 
## <a name="includesssql14mdincludessssql14-mdmd-offline-content"></a>[!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 離線內容 
 
  
**安裝離線內容**  
1. 瀏覽至說明內容的[下載網站](https://www.microsoft.com/en-us/download/details.aspx?id=42557)，然後按一下 [下載]。  
2. 按一下訊息方塊中的 [儲存]，將 SQLServer2014Documentation_*.exe 檔案儲存到您的電腦中。  

 針對防火牆或 Proxy 受限的環境，將下載儲存到可攜至環境中的 USB 磁碟機或其他可攜式媒體。   

3. 按兩下 .exe 以解壓縮說明內容檔案，並將檔案儲存至本機或共用資料夾。  
4. 藉由啟動 SQL Server Management Studio 或 Visual Studio，然後按一下 [說明] 功能表上的 [管理說明設定]，來開啟 [Help Library 管理員]。  
5. 按一下 [從磁碟安裝內容]，然後瀏覽至要解壓縮說明內容檔案的資料夾。  
  
     選取 [從磁碟安裝內容]  |瀏覽至說明內容檔案   
     ---------|---------  
     ![HelpLibraryManager_MainPage_InstallFromDisk](../release-notes/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
     >[!IMPORTANT]
     > 若要避免安裝僅含部分目錄的本機說明內容，請使用 [Help Library 管理員] 中的 [從磁碟安裝內容] 選項。  
     >>如果您已使用 [從線上安裝內容] 選項，而說明檢視器顯示了部分目錄，請參閱這篇[部落格文章](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/)以取得疑難排解的步驟。 

8. 按一下 HelpContentSetup.msha 檔案、按一下 [開啟]，然後按 [下一步]。  
9. 按一下要安裝之文件旁邊的 [加入]，然後按一下 [更新]。  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. 按一下 [完成]，按一下 [結束]。
11. 再次開啟 [Help Library 管理員]，按一下 [選擇線上或本機說明]，然後按一下 [我要使用本機說明]。
12. 按一下 [說明] 功能表上的 [檢視說明]，開啟說明檢視器查看內容。 您應該會在左窗格中，看到您已安裝的內容列於目錄中。  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../release-notes/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
## <a name="view-online-content-in-help-viewer"></a>在說明檢視器中檢視線上內容

在說明檢視器 v2.x 中，您可以執行下列一項作業檢視線上內容。

- 在 SQL Server Management Studio 中，按一下 [說明] 功能表的 [檢視說明]。 文件會顯示於瀏覽器中。
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)

- 在 Visual Studio 中，按一下 [說明] 功能表的 [設定說明偏好]，然後按一下 [在瀏覽器中啟動]。 當您按一下 [說明] 功能表上的 [檢視說明] 時，文件即會顯示於瀏覽器中。

![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)   

在說明檢視器 v1.x 中，您可以執行下列作業檢視線上內容。
1. 按一下 [說明] 功能表上的 [管理說明設定]，來開啟 [Help Library 管理員]。  
2. 在 [Help Library 管理員] 對話方塊中，按一下 [選擇線上或本機說明]。  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../release-notes/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. 依序按一下 [I want to use online help] (我要使用線上說明)、[確定] 和 [結束]。  

   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../release-notes/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)

## <a name="f1-help-and-other-tips"></a>F1 說明和其他提示

當您按 F1 時，即會顯示線上的對應主題。 該主題無法顯示於本機說明中。

此外，說明檢視器不支援 Proxy 設定，也不支援 ISO 格式。 


## <a name="additional-information"></a>其他資訊
[Microsoft 說明檢視器 - Visual Studio 2015](https://msdn.microsoft.com/library/hh580782.aspx)

