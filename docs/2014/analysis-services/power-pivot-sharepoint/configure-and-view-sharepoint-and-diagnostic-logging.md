---
title: 設定及檢視 SharePoint 記錄檔與診斷記錄 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 85f62d29-cdc6-45b3-be1f-ff1182939858
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7099282f8fef9d8d029249ba5637eba6fa6bf1f2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188348"
---
# <a name="configure-and-view-sharepoint-log-files--and-diagnostic-logging-powerpivot-for-sharepoint"></a>設定及檢視 SharePoint 記錄檔與診斷記錄 (PowerPivot for SharePoint)
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器作業、 事件和訊息記錄在 SharePoint 記錄檔中。 使用本主題的資訊來設定記錄層級及檢視記錄檔資訊。 您可以控制要記錄到檔案中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器事件。 您也可以控制所記錄之訊息的嚴重性。 如需詳細資訊，請參閱 <<c0> [ 設定使用量資料收集的&#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)。</c0>  
  
 本主題內容：  
  
-   [記錄檔位置](#bkmk_filelocation)  
  
-   [為個別的事件類別目錄修改診斷記錄層次](#bkmk_modifyloglevels)  
  
-   [如何檢視 SharePoint 記錄檔](#bkmk_how2viewlogfiles)  
  
##  <a name="bkmk_filelocation"></a> 記錄檔位置  
 根據預設，SharePoint 記錄檔會儲存到下列位置：  
  
 `C:\Program files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS`  
  
 LOGS 資料夾中包含記錄檔 (`.log`)、資料檔 (`.txt`) 與使用方式檔案 (`.usage`)。 SharePoint 追蹤記錄的檔案命名慣例為伺服器名稱後面緊接著日期和時間戳記。 SharePoint 追蹤記錄會定期以及有 IISRESET 時建立。 通常在 24 小時的週期內會有許多追蹤記錄。  
  
##  <a name="bkmk_modifyloglevels"></a> 為個別的事件類別目錄修改診斷記錄層次  
 根據預設，PowerPivot 事件的 ULS 記錄是設為 *「中」*。 這是 SQL Server 2012 的新設定。 如果您從舊版升級伺服器，記錄層次可能仍然設為 *「詳細資訊」*(SQL Server 2008 R2 的預設層次)。 如果您習慣檢閱 ULS 記錄檔中的 PowerPivot 伺服器使用資訊，會注意到因為此變更，PowerPivot 伺服器作業相關資訊變少了。  
  
 除了例外狀況 (類型為 *「高」*) 以外，所有的 PowerPivot 訊息都會歸類為「詳細資訊」類別目錄。 如果您想要例行伺服器作業 (例如連接、要求或查詢報告) 的記錄項目，必須將記錄層次變更為「詳細資訊」。  
  
 若要為個別的事件類別修改診斷記錄層次：  
  
1.  在 SharePoint 管理中心，按一下 **[監視]**。  
  
2.  按一下 **[設定診斷記錄]**。  
  
3.  捲動到 **[PowerPivot 服務]**。  
  
4.  展開類別目錄，然後選取個別的類別目錄。  
  
     **應用程式頁面要求**指定尋找時，服務應用程式所觸發的事件[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]載入 PowerPivot 資料來源，以及伺服器陣列中的其他伺服器通訊。  
  
     **[要求處理]** 會指定針對位於伺服器陣列中伺服器上所載入的 PowerPivot 資料庫，由查詢要求所觸發的事件。  
  
     **[使用量]** 指定與 PowerPivot 使用量資料收集相關的事件。  
  
5.  在 [回報至事件記錄的最低緊急事件] 中，選取 **[無]** 以停用類別目錄的事件記錄，或是選取 **[錯誤]** 以限制僅針對錯誤進行記錄。  
  
6.  選取 **[詳細資訊]** ，將所有事件記錄到事件記錄檔。  
  
7.  在 [回報至追蹤記錄的最低緊急事件] 中，選取 **[無]** 以停用類別目錄的追蹤，或是選取 **[錯誤]** 以限制僅為錯誤進行追蹤。  
  
8.  選取 **[詳細資訊]** ，將所有事件記錄到追蹤記錄檔。  
  
9. 按一下 [確定] 。  
  
##  <a name="bkmk_how2viewlogfiles"></a> 如何檢視 SharePoint 記錄檔  
 記錄檔是文字檔。 您可以使用任何文字編輯器來開啟它們。 您也可以使用協力廠商的記錄檢視器應用程式。  
  
#### <a name="use-a-text-editor"></a>使用文字編輯器  
 如果您要使用文字編輯器疑難排解 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器錯誤，下列秘訣可以協助您找出檔案中相關的資訊：  
  
-   若是與發行、檢視或重新整理 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿相關的錯誤，請搜尋記錄檔中的活頁簿名稱。  
  
-   若是提供相互關聯識別碼的錯誤，請複製該識別碼，並將其當做記錄檔中的搜尋詞彙使用。  
  
-   搜尋錯誤狀態「高」或「例外狀況」。 搜尋「PowerPivot 服務」。  
  
-   如果您知道錯誤發生的時間，請使用日期和時間資訊縮小您必須捲動之項目的範圍。  
  
#### <a name="use-a-log-viewer-application"></a>使用記錄檢視器應用程式  
 您可以使用文字編輯器個別檢視追蹤記錄，但是可讓您同時檢視數個記錄檔的記錄檢視器應用程式可能更實用。 慶幸的是，有一些協力廠商記錄檢視器應用程式可以從 Codeplex 網站下載，協助您在單一工作空間檢視多個追蹤記錄。  
  
 下列指示包含可從 Codeplex 下載的常用 SharePoint ULS 記錄檢視器的連結。  
  
1.  移至 Codeplex 網站上的 [SharePoint 記錄檢視器](http://sharepointlogviewer.codeplex.com) 或 [SharePoint ULS 記錄檢視器](http://go.microsoft.com/fwlink/?LinkId=150052) 。  
  
2.  按一下 **[Downloads]** 索引標籤。  
  
3.  按一下可執行檔。 此可執行檔是 **SharePointLogViewer.exe** 或 **ULS Viewer 2.0 Binary**。  
  
4.  閱讀並接受授權條款。  
  
5.  按一下 **[Save]** ，將軟體下載到您的本機系統。  
  
     如果您正在下載 SharePoint ULS 記錄檢視器，請將 ULSViewer.zip 儲存至 Downloads 資料夾。  
  
6.  在 [Downloads] 資料夾中，以滑鼠右鍵按一下 ULSViewer.zip，然後選取 **[解壓縮全部]**。  
  
7.  指定目的地資料夾，然後按一下 **[解壓縮]**。  
  
8.  在包含已解壓縮之程式檔的資料夾中，按兩下 **[ULSViewer]** 並執行應用程式。  
  
9. 按一下應用程式視窗左上角的資料夾圖示。  
  
10. 瀏覽至 \Program files\Common Files\Microsoft Shared\Web Server Extensions\14\Logs。  
  
11. 選取一個或多個追蹤記錄。 根據預設，記錄檔名稱由電腦名稱加上日期和時間資訊所組成。 檔案類型為 [純文字文件]。  
  
12. 按一下 **[開啟]** ，然後等待檔案載入。  
  
13. 根據嚴重性、處理序、類別目錄或使用者定義的文字檔，使用內建的篩選選取記錄。 您也可以按一下欄標題來變更排序次序。  
  
#### <a name="entries-for-powerpivot-services"></a>PowerPivot 服務的項目  
 下表描述很可能在 SharePoint 記錄檔中找到之 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器作業的項目。  
  
|處理|區域|類別目錄|層級|訊息|詳細資料|  
|-------------|----------|--------------|-----------|-------------|-------------|  
|w3wp.exe|[PowerPivot 服務]|[使用量]|「詳細資訊」|目前沒有要求統計資料，沒有要記錄的項目。|服務報表會在預先定義的間隔查詢回應統計資料，做為使用量資料集合系統的使用量事件。 此訊息表示沒有要報告的查詢統計資料。|  
|w3wp.exe|PowerPivot 服務|Web 前端|「詳細資訊」|開始尋找資料來源的應用程式伺服器 =\<*路徑*>|當它收到連接要求時， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務會識別可用的 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 來處理要求。 如果伺服陣列中只有一個伺服器，在所有情況下本機伺服器都會接受要求。|  
|w3wp.exe|PowerPivot 服務|Web 前端|「詳細資訊」|尋找應用程式伺服器成功。|此要求會配置到 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。|  
|w3wp.exe|PowerPivot 服務|Web 前端|「詳細資訊」|要求重新導向\< *PowerPivotdata 來源*> 至[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]。|此要求會轉送至 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]。|  
|w3wp.exe|[PowerPivot 服務]|[要求處理]|「詳細資訊」|使用者名稱的要求重新導向\<*SharePoint 使用者*> 資料庫|系統會代表 SharePoint 使用者建立模擬的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料來源連接。|  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot 使用量資料收集](power-pivot-usage-data-collection.md)   
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [設定使用量資料收集的&#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
