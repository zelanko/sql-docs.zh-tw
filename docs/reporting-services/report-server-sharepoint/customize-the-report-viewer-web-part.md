---
title: "自訂報表檢視器 web 組件 |Microsoft 文件"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 38f23cf5d75c47be55e1820a4421a507a73df54e
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="customize-the-report-viewer-web-part"></a>自訂報表檢視器 web 組件

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

若要檢視設定為 SharePoint 整合報表伺服器執行的報表，您可以使用報表檢視器 web 組件。 可顯示的報表包括報表定義 (.rdl) 檔案和報表產生器報表。 報表在報表檢視器 web 組件，在新網頁中自動開啟，但您也可以加入報表檢視器 web 組件某現有網頁或網站如果您想要總是顯示在該頁面上的特定報表。

> [!NOTE]
> 雖然它們有相同名稱時，報表檢視器 web 組件透過安裝[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]增益集是包含在 RSWebParts.cab 檔案 報表檢視器網頁組件不同。 本主題中的指示是特別針對透過安裝報表檢視器 web 組件[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]增益集。

 您可以下列方式自訂報表檢視器 web 組件：  
  
-   設定屬性，以變更 web 組件的外觀。  
  
-   選擇報表工具列上可用哪些互動式報表功能。  
  
-   指定可用哪些檢視區域。 報表檢視器 web 組件有報表檢視區域、 參數區域和認證區域。  
  
 您無法擴充成支援不同的檔案類型，報表檢視器 web 組件，您無法自訂工具列取代報表工具列，或在現有工具列上加入新的功能。 如果您必須自訂標準功能，您應該建立自訂 web 組件。  

## <a name="setting-web-part-properties"></a>設定 web 組件屬性

 Web 組件有自訂屬性，用來設定特定的功能。 Web 組件也會有共通的標準，每個 web 組件的屬性。  
  
### <a name="change-default-properties"></a>變更預設屬性

 報表檢視器 web 組件有一些非常適合用於視開啟報表從程式庫或資料夾的預設屬性。 根據預設，所有可用控制項都會顯示的工具列上，而且高度和寬度都設定在網頁上使用所有可用的空間。 如果您想要修改預設屬性，您可以自訂 web 組件透過**站台設定**。  
  
1.  在 **[網站動作]** 功能表上，按一下 **[網站設定]**。  
  
2.  在組件庫，按一下  **web 組件**。  
  
3.  按一下 **[ReportViewer.dwp]**。  
  
4.  開啟工具窗格，並設定要使用的屬性。  
  
### <a name="customize-an-embedded-report-viewer-in-a-web-page"></a>自訂在網頁中內嵌的報表檢視器

 您可以設定屬性，使報表檢視器適合網頁。 報表檢視器可以與包含它的頁面使用相同的樣式和色彩。 您可以隱藏工具列、文件引導模式和參數區域的全部或一部分，使配置空間內的報表檢視區域放到最大。 報表所使用的樣式一定是在建立時為它所定義的樣式，您無法在報表發行至 SharePoint 文件庫後自訂其外觀。  
  
 如果您要在網頁中內嵌報表檢視器 web 組件，您應該設定**報表 URL**特定報表的屬性。 否則，報表檢視器將會顯示連結至報表的指示。 您無法自訂或移除這些指示。  
  
### <a name="custom-properties-of-the-report-viewer-web-part"></a>報表檢視器 web 組件自訂屬性

 設定自訂屬性時，請注意有些屬性可在網頁中內嵌報表檢視器 web 組件時，才。 例如，標題、高度、寬度、色彩類型和區域。 至於其他屬性 (例如工具列設定和參數設定)，則無論報表檢視器出現在頁面內或是以整頁模式開啟報表，都可以使用。  
  
 報表檢視器 web 組件的自訂屬性如下。  
  
|屬性|說明|  
|--------------|-----------------|  
|報表|報表的完整路徑，此報表位於目前的 SharePoint 網站上，或是相同 Web 應用程式或伺服陣列內的網站上。 若要在設定其他屬性時獲得最佳結果，請在指定報表 URL 之後按一下 [套用]。|  
|超連結目標|標準 HTML，此 HTML 會指定在目前文件內顯示連結內容的目標框架。 如果是包含外部網站超連結的報表，您可以指定目標文件會取代目前視窗內現有的報表，或是在新的瀏覽器視窗中開啟。 有效值包括 **_Top**、 **_Blank**和 **_Self**。 **_Top** 會使用目前的視窗， **_Blank** 則會在新的瀏覽器視窗中載入文件，而 **_Self** 會在目前的框架內開啟文件。 雖然**_Parent** HTML 中的目標屬性，請勿使用內嵌於頁面報表檢視器 web 組件是有效的值。|  
|自動產生 web 組件標題|產生的標題，其中包含報表檢視器 web 組件名稱加上報表，並以破折號分隔的名稱。 如果報表沒有標題，則會使用報表的檔案名稱。 當您將 web 組件加入頁面時，標題就會顯示。 如果選取這個核取方塊，則標題會在每一次重新整理頁面時產生。|  
|自動產生 web 組件標題詳細資料連結|會出現在 web 組件上方產生超連結。 您可以按一下連結，在新頁面中以整頁模式開啟報表。|  
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
|文件引導模式|在報表中定義的報表導覽控制項，用來提供報表特定區段的單鍵存取。 此模式於 HTML 報表中提供。 文件引導模式會在報表檢視區域旁的可摺疊區域中顯示。 有效的值包括 **Displayed**、 **Collapsed**和 **Hidden**。 如果報表定義文件引導模式，此區域會展開預設情況下，除非標記為隱藏或摺疊 web 組件屬性中。 如果文件引導模式為摺疊，則可以按一下箭號將它展開。|  
|文件引導模式區域寬度|您可以選擇度量單位和值。 預設值是 200 像素。 此屬性的唯一需求為大於零。|  
|載入參數|擷取報表的參數屬性。 並非所有報表都有參數。 如果報表沒有參數，則不會傳回任何值。 如果您要為剛剛上傳的報表設定屬性，則可能會收到錯誤，指出資料來源連接已刪除。 如果發生此錯誤，請重設連接，然後在指定連接之後完成設定參數屬性。 如需如何設定連接的詳細資訊，請參閱[建立和管理共用資料來源 &#40;Reporting Services SharePoint 整合模式 &#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).<br /><br /> 為了獲得最佳結果，在按一下 [載入參數] 之前，請先按一下 **[套用]** 。<br /><br /> 載入參數屬性之後，就可利用您在報表的參數屬性頁面中使用的方式設定屬性。 如需如何設定參數的詳細資訊，請參閱[已發行的報表 &#40; 上的 設定參數Reporting Services SharePoint 整合模式 &#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).|  

## <a name="customizing-the-toolbar"></a>自訂工具列

 工具列會出現在標題下方，並且橫跨報表頂端。 工具列提供 **[動作]** 功能表、已編頁報表的頁面導覽、重新整理和顯示比例。 其中包含文件引導模式控制項，用於擁有文件引導模式的報表。 **[動作]** 功能表所包含的命令可用於匯出報表、搜尋報表中的文字或數字、列印報表，以及在報表產生器中開啟報表。  
  
 您無法將新的命令加入至  **[動作]** 功能表，但是您可以變更使用者看得到的選項來加以自訂。 若要變更工具列按鈕與控制項的可見性，您可以變更之選項的**工具列項目可見性**web 組件的區段。 您也可以在報表伺服器上停用 **[列印]** 命令或特定匯出格式，藉此移除這些功能。 頁面導覽控制項適用於擁有分頁符號的報表；否則，報表為可改變長度的單一頁面。 **重新整理**重新處理報表使用報表最新的參數。 若要顯示於同一行上的所有控制項，將 web 組件的整體寬度設定為至少 400 像素。  

## <a name="customizing-the-viewing-area"></a>自訂檢視區域

 檢視區域可用來顯示報表。 報表檢視區域會與參數區域和認證區域共用 (如果使用的話)。 如果需要認證，認證區域就會出現在空的報表檢視區域旁邊。 等使用者提供認證並執行報表之後，認證區域就會關閉。 若要自訂提示使用者設定認證的文字，請修改資料來源連接屬性。 如需詳細資訊，請參閱[建立和管理共用資料來源 &#40;Reporting Services SharePoint 整合模式 &#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
 參數區域提供執行報表之前輸入值的欄位。 只有在報表定義包括參數時才會使用此區域。 當顯示參數或認證區域時，報表檢視會調整成使用 web 組件的剩餘寬度。 您可以自訂參數的寬度 web 組件上設定屬性。 您也可以定義頁面上個別參數旁出現的標籤。 如需如何修改參數標籤的詳細資訊，請參閱[已發行的報表 &#40; 上的 設定參數Reporting Services SharePoint 整合模式 &#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>另請參閱

 [在 SharePoint 網站上的報表檢視器 web 組件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [將報表檢視器 web 組件加入至 web 網頁](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

