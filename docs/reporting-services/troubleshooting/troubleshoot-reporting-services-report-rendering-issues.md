---
title: "Reporting Services 報表轉譯問題疑難排解 |Microsoft 文件"
ms.custom: 
ms.date: 02/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1e0fb399-4c16-438a-92cb-db3e877896d0
caps.latest.revision: 4
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 91629c6d86f1616b19026cbc0e670fff51553dda
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot-reporting-services-report-rendering-issues"></a>Reporting Services 報表轉譯問題疑難排解
結合報表資料與配置資訊之後，編譯完的報表會傳送到報表轉譯器。 例如，當您在本機預覽報表時，您會使用 HTML 轉譯器來檢視已編譯的報表。 您可以使用本主題來協助疑難排解有關報表轉譯的問題。   
  
## <a name="why-do-i-have-extra-white-space-including-blank-pages-in-my-report"></a>為什麼我的報表中有多餘的空白，包括空白頁？  
在報表處理期間，報表項目會自動調整以便保留定義為報表內容的空白。 報表 [設計] 檢視中的空白會獲得保留。 在報表設計介面上，白色背景代表檢視、匯出或列印報表時會保留的空白，端視目標媒體而定。  
  
### <a name="white-space-and-page-breaks-interact-during-rendering"></a>空白和分頁符號在轉譯期間互動  
當您檢視報表或將報表匯出為某檔案格式時，相關的轉譯延伸模組會處理報表，並將報表儲存為您指定的檔案格式。 每一個轉譯延伸模組，都會根據其特定規則來處理報表中的空白。 此外，空白還會受到下列因素的影響：頁面設定屬性、設定在報表項目上的分頁符號、放置在報表主體中的報表項目相對位置、特定報表項目的 KeepTogether 屬性，以及報表項目是否在父容器內。   
  
若要刪除由於報表寬度所產生的額外頁面，請拖曳報表設計介面的邊緣，以便與最外側的報表項目對齊。 若為由左至右的報表配置，請拖曳右邊緣，以便與最外側的報表項目對齊。 如需詳細資訊，請參閱 [轉譯行為](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
### <a name="white-space-is-not-preserved-at-the-end-of-a-report"></a>報表結尾處的空白未保留  
對於報表結尾處的空白，Reporting Services 提供可以讓您予以保留或刪除的選項。   
  
若要保留報表結尾處的空白，請選取報表並在 [屬性] 窗格中捲動至 ConsumeContainerWhitespace，然後輸入 False。   
  
## <a name="why-do-my-reports-look-different-when-exported-to-different-formats"></a>當我的報表匯出成不同格式時，為什麼看起來會不一樣？  
當您執行報表時，您可以將報表匯出成其他格式，例如 Excel、Word 或 PDF。 根據您匯出的格式而定，報表可能會有某些規則和限制。 當您建立報表時，可以考量許多限制來加以對付。 您可能需要在報表中使用稍微不同的配置、小心對齊報表內的項目、將報表頁尾限制為單行文字等等。 您也可以使用內建的全域 RenderFormat，在某些條件下針對不同的轉譯器使用不同的報表配置。 其他內建全域功能可以幫助您管理匯出之格式的分頁，並為 Excel 中的工作表索引標籤命名。 如需詳細資訊，請參閱 [匯出報表](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) 和 [使用內建的 Globals 和 Users 參考資料](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。  
  
## <a name="how-can-i-view-all-my-report-data-on-one-page"></a>如何在單一頁面上檢視所有報表資料？  
對於資料量不大的報表，您可能想要將所有資料顯示在單一頁面上，以便進行互動式檢視。   
  
就軟分頁轉譯器而言，若要在單一頁面上檢視所有資料，請在 [報表屬性] 中將 [InteractiveHeight] 設為 0。 軟分頁轉譯器會忽略現有的分頁符號。   
  
> [!NOTE]  
> 當報表沒有分頁符號時，必須先將整個報表處理完畢之後，您才能檢視第一頁。   
  
如需轉譯器類別目錄的詳細資訊，請參閱 [轉譯行為](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
## <a name="reports-do-not-run-when-your-browser-is-configured-to-prompt-for-credentials"></a>當瀏覽器設定為提示認證時，報表不會執行。  
當瀏覽器設定為提示認證，而且資料來源有設定整合式 Windows 驗證時，檢視您的報表可能會失敗並傳回錯誤訊息。 當資料來源所在的電腦與報表伺服器不同、資料來源設定為使用 Windows 驗證，而且瀏覽器設定為提示認證時，就會發生這個情況。 以下是您將會看到的訊息範例。  
  
當針對 Microsoft SQL Server 連接類型設定資料來源時：  
`An error has occurred during report processing.`  
`Cannot create a connection to data source 'localhost'.`  
`Login failed for user '(null)'. Reason: Not associated with a trusted SQL Server connection.`  
  
當針對 Microsoft SharePoint 清單連接類型設定資料來源時：  
`An error occurred during client rendering.`   
`An error has occurred during report processing.`   
`Query execution failed for dataset 'DataSet1'.`   
`The request failed with HTTP status 401: Unauthorized.`  
  
**若要解決此問題** ：修改資料來源以使用預存認證，而非 Windows 認證。  
  
**此問題適用於** ：瀏覽器設定為提示認證時。  
  
## <a name="see-also"></a>請參閱＜  
[錯誤和事件 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[搭配 Reporting Services 報表為資料擷取問題疑難排解](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[為 Reporting Services 訂閱與傳遞疑難排解](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


