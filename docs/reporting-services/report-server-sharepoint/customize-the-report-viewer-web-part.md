---
title: 自訂報表檢視器 Web 組件 | Microsoft Docs
description: 您可以使用報表檢視器網頁組件，檢視在為 SharePoint 整合所設定的 SQL Server Reporting Services 伺服器上執行的報表。
ms.date: 11/26/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 50ff7c29e6718d8d38829d9cb23f5fafb6cf4dea
ms.sourcegitcommit: 66a0672e47415dbd5cfd8d19075102c8c3973e70
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83767045"
---
# <a name="customize-the-report-viewer-web-part"></a>自訂報表檢視器 Web 組件

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]  [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-and-later](../../includes/ssrs-appliesto-sharepoint-2013-and-later.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

您可以使用報表檢視器 Web 組件來檢視在設定為 SharePoint 整合之報表伺服器上執行的報表。 可顯示的報表包括報表定義 (.rdl) 檔案和報表產生器報表。 報表會自動在報表檢視器 Web 組件的新頁面中開啟。 如果您希望特定的報表能一律顯示在該頁面上，您也可以將報表檢視器 Web 組件新增至現有網頁或網站。

> [!NOTE]
> 雖然它們有相同的名稱，但是透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集安裝的報表檢視器 Web 組件，與包含在 RSWebParts.cab 檔案中的報表檢視器 Web 組件不同。 本主題中的指示是特別針對透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集安裝的報表檢視器 Web 組件。

 您可以用下列方式自訂報表檢視器 Web 組件：  
  
-   設定屬性以變更 Web 組件的外觀。  
  
-   選擇報表工具列上可用哪些互動式報表功能。  
  
-   指定可用哪些檢視區域。 報表檢視器 Web 組件有報表檢視區域、參數區域和認證區域。  
  
 您無法將報表檢視器 Web 組件擴充成支援不同檔案類型，也無法用自訂工具列取代報表工具列，或在現有工具列上新增新功能。 如果您必須自訂標準功能，就應該建立自訂的 Web 組件。  

## <a name="setting-web-part-properties"></a>設定 Web 組件屬性

 Web 組件有一些用來設定特定功能的自訂屬性， 也有一些每個 Web 組件共通的標準屬性。  
  
### <a name="change-default-properties"></a>變更預設屬性

 報表檢視器 Web 組件有一些預設屬性，非常適合用於視需要從文件庫或資料夾開啟報表。 根據預設，工具列會顯示所有可用的控制項。 高度和寬度設定為使用網頁上所有的可用空間。 如果您要修改預設屬性，可透過 [網站設定] 自訂 Web 組件。  
  
1.  在 **[網站動作]** 功能表上，按一下 **[網站設定]** 。  
  
2.  在組件庫下，按一下 [Web 組件]。  
  
3.  按一下 **[ReportViewer.dwp]** 。  
  
4.  開啟工具窗格，並設定要使用的屬性。  
  
### <a name="customize-an-embedded-report-viewer-in-a-web-page"></a>在網頁中自訂內嵌的報表檢視器

 您可以設定屬性，使報表檢視器適合網頁的大小。 報表檢視器可以與包含它的頁面使用相同的樣式和色彩。 您可以隱藏工具列、文件引導模式和參數區域的全部或一部分，使配置空間內的報表檢視區域放到最大。 報表一律使用您建立報表時所定義的樣式。 當您將報表發行至 SharePoint 文件庫之後，即無法自訂報表外觀。  
  
 如果要將報表檢視器 Web 組件內嵌在網頁中，就應該將 [報表 URL]**** 屬性設定為特定報表。 否則，報表檢視器將會顯示連結至報表的指示。 您無法自訂或移除這些指示。  
  
### <a name="custom-properties-of-the-report-viewer-web-part"></a>報表檢視器 Web 組件的自訂屬性

 設定自訂屬性時，須注意有些屬性只有當報表檢視器 Web 組件內嵌在頁面中時才適用， 例如，標題、高度、寬度、色彩類型和區域。 至於其他屬性 (例如工具列設定和參數設定)，則無論報表檢視器出現在頁面內或是以整頁模式開啟報表，都可以使用。  
  
 報表檢視器 Web 組件的自訂屬性如下所列。  
  
|屬性|說明|  
|--------------|-----------------|  
|Report|報表的完整路徑，此報表位於目前的 SharePoint 網站上，或是相同 Web 應用程式或伺服陣列內的網站上。 若要在設定其他屬性時獲得最佳結果，請在指定報表 URL 之後按一下 [套用]。|  
|超連結目標|標準 HTML，此 HTML 會指定在目前文件內顯示連結內容的目標框架。 如果是包含外部網站超連結的報表，您可以指定目標文件會取代目前視窗內現有的報表，或是在新的瀏覽器視窗中開啟。 有效值包括 **_Top**、 **_Blank**和 **_Self**。 **_Top** 會使用目前的視窗， **_Blank** 則會在新的瀏覽器視窗中載入文件，而 **_Self** 會在目前的框架內開啟文件。 雖然 **_Parent** 是 HTML 中目標屬性的有效值，但是請不要在報表檢視器 Web 組件內嵌於頁面中時使用。|  
|自動產生 Web 組件標題|所產生的標題，其中包括報表檢視器 Web 組件的名稱加上報表的名稱，兩者以破折號分隔。 如果報表沒有標題，則會使用報表的檔案名稱。 標題可在您將網頁組件新增至頁面時看見。 如果選取這個核取方塊，則標題會在每一次重新整理頁面時產生。|  
|自動產生 Web 組件標題詳細資料連結|產生的超連結，會出現在 Web 組件的上方。 您可以按一下連結，在新頁面中以整頁模式開啟報表。|  
|顯示報表產生器功能表項目|顯示或隱藏 **[動作]** 功能表選項以開啟報表產生器。|  
|顯示訂閱功能表項目|顯示或隱藏 **[動作]** 功能表選項以建立報表的訂閱。|  
|顯示列印功能表項目|顯示或隱藏 **[動作]** 功能表選項以列印報表。|  
|顯示匯出功能表項目|顯示或隱藏 **[動作]** 功能表選項以匯出報表。|  
|顯示重新整理按鈕|顯示或隱藏工具列上的重新整理按鈕。|  
|顯示頁面導覽控制項|顯示或隱藏工具列上的報表導覽按鈕。 此選項會變更所有導覽控制項的可見性。|  
|顯示上一步按鈕|顯示或隱藏工具列上的上一步按鈕。|  
|顯示尋找控制項|顯示或隱藏工具列上的尋找控制項。 尋找控制項可讓使用者在轉譯的報表內搜尋文字。 此選項會變更所有尋找控制項的可見性。|  
|顯示縮放控制項|顯示或隱藏工具列上的縮放控制項。|  
|顯示 ATOM 摘要按鈕|顯示或隱藏工具列上的 ATOM 摘要按鈕。<br /><br /> ![htmlviewer_datafeed](../../reporting-services/media/htmlviewer-datafeed.gif "htmlviewer_datafeed")|  
|工具列位置|判斷工具列在報表檢視器中的位置。 有效值包括 **Top** 和 **Bottom**。|  
|提示區域|有效的值包括 **Displayed**、 **Collapsed**和 **Hidden**。 **Displayed** 會針對包括參數化值的報表，以及需要使用者輸入才能執行的報表顯示參數區域。 如果已指定所有報表參數，而您不想讓使用者看見參數區域，請使用 **Hidden** 。|  
|參數區域寬度|您可以選擇度量單位和值。 預設值是 200 像素。 此屬性的唯一需求為大於零。|  
|文件引導模式|在報表中定義的報表導覽控制項，用來提供報表特定區段的單鍵存取。 此模式於 HTML 報表中提供。 文件引導模式會在報表檢視區域旁的可摺疊區域中顯示。 有效的值包括 **Displayed**、 **Collapsed**和 **Hidden**。 如果已定義報表的文件引導模式，除非在 Web 組件屬性中標記為隱藏或摺疊，否則此區域會根據預設展開。 如果文件引導模式為摺疊，則可以按一下箭號將它展開。|  
|文件引導模式區域寬度|您可以選擇度量單位和值。 預設值是 200 像素。 此屬性的唯一需求為大於零。|  
|載入參數|擷取報表的參數屬性。 並非所有報表都有參數。 如果報表沒有參數，則不會傳回任何值。 如果您要為剛剛上傳的報表設定屬性，則可能會收到錯誤，指出資料來源連接已刪除。 如果發生此錯誤，請重設連接，然後在指定連接之後完成設定參數屬性。 如需如何設定連線的詳細資訊，請參閱[建立和管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)。<br /><br /> 為了獲得最佳結果，在按一下 [載入參數] 之前，請先按一下 **[套用]** 。<br /><br /> 載入參數屬性之後，就可利用您在報表的參數屬性頁面中使用的方式設定屬性。 如需如何設定參數的詳細資訊，請參閱[在已發行的報表上設定參數 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)。|  

## <a name="customizing-the-toolbar"></a>自訂工具列

 工具列會出現在標題下方，並且橫跨報表頂端。 工具列提供 **[動作]** 功能表、已編頁報表的頁面導覽、重新整理和顯示比例。 其中包含文件引導模式控制項，用於擁有文件引導模式的報表。 **[動作]** 功能表所包含的命令可用於匯出報表、搜尋報表中的文字或數字、列印報表，以及在報表產生器中開啟報表。  
  
 您無法將新的命令加入至  **[動作]** 功能表，但是您可以變更使用者看得到的選項來加以自訂。 若要變更工具列按鈕與控制項的可見性，您可以變更 Web 組件之 [工具列項目可見性] 區段中的選項。 您也可以在報表伺服器上停用 **[列印]** 命令或特定匯出格式，藉此移除這些功能。 頁面導覽控制項適用於擁有分頁符號的報表；否則，報表為可改變長度的單一頁面。 [重新整理] 會使用報表的最新參數重新處理報表。 若要在同一行顯示所有控制項，請將 Web 組件的整體寬度設定為至少 400 像素。  

## <a name="customizing-the-viewing-area"></a>自訂檢視區域

 檢視區域可用來顯示報表。 報表檢視區域會與參數區域和認證區域共用 (如果使用的話)。 如果需要認證，認證區域就會出現在空的報表檢視區域旁邊。 等使用者提供認證並執行報表之後，認證區域就會關閉。 若要自訂提示使用者設定認證的文字，請修改資料來源連接屬性。 如需詳細資訊，請參閱[建立及管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)。  
  
 參數區域提供執行報表之前輸入值的欄位。 只有在報表定義包括參數時才會使用此區域。 當顯示參數或認證區域時，報表檢視會調整成使用 Web 組件的剩餘寬度。 您可以設定 Web 組件上的屬性，以自訂參數的寬度。 您也可以定義頁面上個別參數旁出現的標籤。 如需如何修改參數標籤的詳細資訊，請參閱[在已發行的報表上設定參數 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)。  
  
## <a name="see-also"></a>另請參閱

 [SharePoint 網站上的報表檢視器 Web 組件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [將報表檢視器 Web 組件新增至網頁](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
