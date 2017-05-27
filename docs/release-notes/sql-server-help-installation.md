---
title: "適用於 SQL Server 的說明檢視器 | Microsoft Docs"
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fc2435ccea3b01328c3c4623e62fbf12ee53e400
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="help-viewer-for-sql-server"></a>適用於 SQL Server 的說明檢視器
  
  
  
本文將逐步引導您安裝本機說明，以及顯示線上和本機說明。 本文涵蓋 Microsoft 說明檢視器 1.1 和 2.2，以及適用於 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 和 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 的文件。 

>[!IMPORTANT]
>說明檢視器不支援 Proxy 設定，且不支援 ISO 格式。  

>**F1 和說明**
>>當您按 F1 時，即會顯示線上的對應主題。 該主題無法顯示於本機說明中。

## <a name="includesscurrentmdincludessscurrent-mdmd-and-help-viewer-22"></a>[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 和說明檢視器 2.2  
您可以在 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Management Studio (從 2016 年 4 月的預覽版 (13.0.12500.29) 開始) 和 Visual Studio 2015 中取得說明檢視器 2.2。  

> [![下載 SSMS](../release-notes/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) **[下載最新版的 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**  

**安裝本機說明以與說明檢視器 2.2 搭配使用**  
1. 藉由啟動 SQL Server Management Studio 或 Visual Studio，然後按一下 [說明] 功能表上的 [加入和移除說明內容]，來開啟說明檢視器 2.2。  
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

1. (選擇性) [管理內容] 索引標籤上的 [本機存放區路徑] 方塊會顯示本機電腦上安裝文件的位置。 若要將文件移至不同的位置，按一下 [移動]、在 [移動內容] 對話方塊的 [至] 欄位中輸入資料夾路徑，然後按一下 [確定]。

   ![HelpViewer2_Move Content Dialog](../release-notes/media/helpviewer2-move-content-dialog.png)

   移動內容之後，新的位置就會顯示在 [本機存放區路徑] 中。
      
   >[!IMPORTANT]
   > 如果出現訊息指出移動操作失敗，請關閉訊息方塊、關閉說明檢視器，然後重新開啟說明檢視器。 內容的新位置現在應該會出現在 [本機存放區路徑] 中。   
  
**在 SQL Server Management Studio 中顯示本機說明或線上說明**  
* 若要檢視本機說明，按一下 [說明] 功能表上的 [加入和移除說明內容]，然後按一下[說明檢視器首頁] 索引標籤來查看文件。  
    >[!NOTE]
    >**說明檢視器首頁**的文字會根據您在目錄中按下的是哪一個主題來變更。   
* 若要檢視線上說明，按一下 [說明] 功能表上的 [檢視說明]。 文件會顯示於瀏覽器中。  
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)  
  
  
**在 Visual Studio 中顯示本機說明或線上說明**  
* 按一下 [說明] 功能表上的 [設定說明偏好]，然後執行下列其中一項。  
   * 按一下 [在瀏覽器中啟動] 來檢視線上說明。 當您按一下 [說明] 功能表上的 [檢視說明] 時，文件即會顯示於瀏覽器中。  
   * 按一下 [在說明檢視器中啟動] 來檢視本機說明。 當您按一下 [說明] 功能表上的 [檢視說明] 時，文件即會顯示於說明檢視器中。  
     
     ![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)  
  
  
## <a name="includesssql14mdincludessssql14-mdmd-and-help-viewer-11"></a>[!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 和說明檢視器 1.1  
 您可以從 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] Management Studio 和 Visual Studio 2012 之前的 Visual Studio 版本中取得說明檢視器 1.1 。   
 
>[!NOTE]
> 只有當您**從磁碟安裝內容**時，也能使用說明檢視器 2.2 來檢視 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 的本機說明。 您可以在 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Management Studio (從 2016 年 4 月的預覽版 (13.0.12500.29) 開始) 和 Visual Studio 2015 中取得說明檢視器 2.2。 
   
**安裝本機說明以與說明檢視器 1.1 搭配使用**  
1. 瀏覽至說明內容的[下載網站](https://www.microsoft.com/en-us/download/details.aspx?id=42557)，然後按一下 [下載]。  
2. 按一下訊息方塊中的 [儲存]，將 SQLServer2014Documentation_*.exe 檔案儲存到您的電腦中。  
   >[!NOTE]
   >針對防火牆或 Proxy 受限的環境，將下載儲存到可攜至環境中的 USB 磁碟機或其他可攜式媒體。   
3. 按兩下 .exe 以解壓縮說明內容檔案，並將檔案儲存至本機或共用資料夾。  
4. 藉由啟動 SQL Server Management Studio 或 Visual Studio，然後按一下 [說明] 功能表上的 [管理說明設定]，來開啟 [Help Library 管理員]。  
7. 按一下 [從磁碟安裝內容]，然後瀏覽至要解壓縮說明內容檔案的資料夾。  
  
選取 [從磁碟安裝內容]  |瀏覽至說明內容檔案   
---------|---------  
![HelpLibraryManager_MainPage_InstallFromDisk](../release-notes/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
>[!IMPORTANT]
> 若要避免安裝僅含部分目錄的本機說明內容，請使用 [Help Library 管理員] 中的 [從磁碟安裝內容] 選項。  
>>如果您已使用 [從線上安裝內容] 選項，而說明檢視器顯示了部分目錄，請參閱這篇[部落格文章](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/)以取得疑難排解的步驟。 

8. 按一下 HelpContentSetup.msha 檔案、按一下 [開啟]，然後按 [下一步]。  
9. 按一下要安裝之文件旁邊的 [加入]，然後按一下 [更新]。  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. 依序按一下 [完成] 和 [結束]，然後開啟說明檢視器，按一下 [說明] 功能表上的 [檢視說明] 來查看內容。 您應該會在左窗格中，看到您已安裝的內容列於目錄中。  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../release-notes/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
**顯示本機說明或線上說明**  
1. 按一下 [說明] 功能表上的 [管理說明設定]，來開啟 [Help Library 管理員]。  
2. 在 [Help Library 管理員] 對話方塊中，按一下 [選擇線上或本機說明]。  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../release-notes/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. 執行下列其中一項作業，然後依序按一下 [確定] 和 [結束]。  
   * 按一下 [我想要使用線上說明]。  
   * 按一下 [我想要使用本機說明]。  
  
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../release-notes/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)  
  
如果您選擇使用線上說明，當您按一下 [說明] 功能表上的 [檢視說明] 時，瀏覽器就會啟動並顯示 MSDN 上的[SQL Server 2014 的線上叢書](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx)文章。 如果您選取使用本機說明，當您按一下[檢視說明] 時，即會啟動說明檢視器。  

## <a name="additional-information"></a>其他資訊
[Microsoft 說明檢視器 - Visual Studio 2015](https://msdn.microsoft.com/library/hh580782.aspx)

