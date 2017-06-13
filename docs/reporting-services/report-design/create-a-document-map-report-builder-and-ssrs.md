---
title: "建立文件引導模式 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c200a97b-67f2-499f-8374-3ed1ebe3f33c
caps.latest.revision: 13
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3abd0b8ce2b463cf793b6b75c908a69308cb68a8
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---

# <a name="create-a-document-map-report-builder-and-ssrs"></a>建立文件引導模式 (報表產生器及 SSRS)

文件引導模式提供了與轉譯報表中之報表項目連結的一組導覽連結。 您檢視包含文件引導模式的報表時，報表旁邊會出現另一個側窗格。 使用者按一下文件引導模式中的連結，即可跳到顯示該項目的報表頁面。 報表區段與群組會以連結的階層排列。 按一下文件引導模式中的項目，會重新整理報表並顯示文件引導模式中之項目所對應的報表區域。  
  
 若要在文件引導模式中加入連結，您可將報表項目的 **DocumentMapLabel** 屬性設定為您所建立的文字，或是將它設定為某個運算式，該運算式會評估為您希望顯示於文件引導模式中的文字。 您也可以將資料表或矩陣群組的唯一值加入到文件引導模式。 例如，如果是以色彩為根據的群組，每一個唯一色彩就是報表頁面的連結，可顯示該色彩的群組執行個體。  
  
 您也可以建立報表的 URL 來覆寫文件引導模式的顯示，讓您可以執行報表而不顯示文件引導模式，然後按一下報表檢視器工具列上的 **[顯示/隱藏文件引導模式]** 按鈕來切換顯示。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DocMapRenderExtensions"></a> 文件引導模式及轉譯延伸模組  
 文件引導模式旨在供 HTML 轉譯延伸模組使用，例如，在預覽和報表檢視器中。 其他轉譯延伸模組有不同的方式來表達文件引導模式：  
  
-   PDF 會將文件引導模式轉譯成 [書籤] 窗格。  
  
-   Excel 會將文件引導模式轉譯成具名工作表，其中包含連結的階層。 報表區段會在個別工作表中轉譯，這些工作表和文件引導模式包含在同一個活頁簿中。  
  
-   Word 會將文件引導模式加入為目錄。  
  
-   Atom、TIFF、XML 與 CSV 則會忽略文件引導模式。  
  
 如需詳細資訊，請參閱[不同報表轉譯延伸模組的互動式功能 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)。  
  
##  <a name="AddRptItemToMap"></a>   
#### <a name="to-add-a-report-item-to-a-document-map"></a>將報表項目加入至文件引導模式中  
  
1.  在 [設計] 檢視中，選取要加入至文件引導模式的報表項目，例如資料表、矩陣或量測計。 該報表項目的屬性會出現在 [屬性] 窗格中。  
  
    > [!NOTE]  
    >  若要選取 Tablix 資料區，請在任何資料格中按一下來顯示資料列和資料行控點，然後按一下角控點。  
  
2.  在 [屬性] 窗格中，輸入您希望在文件引導模式中出現在 **[DocumentMapLabel]** 屬性內的文字，或是輸入評估為某個標籤的運算式。 例如，輸入 **Sales Chart**。  
  
    > [!NOTE]  
    >  如果看不到 [屬性] 窗格，請在 **[檢視]** 索引標籤的 **[顯示/隱藏]** 群組中，選取 **[屬性]**。  
  
3.  針對您希望出現在文件引導模式中的每個報表項目重複步驟 1 和 2。  
  
4.  按一下 **[執行]**。 報表便會執行，而且文件引導模式會顯示您所建立的標籤。 按一下任何連結，即可跳至包含該項目的報表頁面。  

  
##  <a name="AddUniqueValuesToMap"></a>   
#### <a name="to-add-unique-group-values-to-a-document-map"></a>將唯一的群組值加入至文件引導模式中  
  
1.  在 [設計] 檢視中，選取包含您希望顯示在文件引導模式中之群組的資料表、矩陣或清單。 [群組] 窗格會顯示資料列和資料行群組。  
  
2.  在 [資料列群組] 窗格中，以滑鼠右鍵按一下群組，然後按一下 **[編輯群組]**。 **[Tablix 群組屬性]** 對話方塊的 **[一般]** 頁面隨即開啟。  
  
3.  按一下 **[進階]**。  
  
4.  在 **[文件引導模式]** 清單方塊中，輸入或選取符合群組運算式的某個運算式。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  針對您希望出現在文件引導模式中的每一個群組重複步驟 1 到 4。  
  
7.  按一下 **[執行]**。 報表便會執行，而且文件引導模式會顯示群組值。 按一下任何連結，即可跳至包含該項目的報表頁面。  
  
##  <a name="HideMapWhenViewRpt"></a>   
#### <a name="to-hide-the-document-map-when-you-view-a-report"></a>在檢視報表時隱藏文件引導模式  
  
1.  在報表管理員中，瀏覽至具有文件引導模式的報表。  
  
     例如，以 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 範例報表為例，下列 URL 會指定名為 Product Catalog 的報表。  
  
    ```  
    http://localhost/Reports/Pages/Report.aspx?ItemPath=%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    ```  
  
2.  複製伺服器上的報表路徑。 在此範例中，報表路徑為 `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`。  
  
3.  建立具有下列三個元件的新 URL：  
  
    -   報表伺服器上的報表檢視器： `http://localhost/ReportServer/Pages/ReportViewer.aspx?`  
  
    -   您在步驟 1 中複製的報表名稱，例如： `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`  
  
    -   指定隱藏文件引導模式的裝置資訊參數： `&rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False`  
  
     下列 URL 是由附加的三個元件所組成 (依據其列出的順序)。  
  
    ```  
    http://localhost/ReportServer/Pages/ReportViewer.aspx?  
    %2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    &rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False  
    ```  
  
     若要使用這個 URL，請複製它，並移除所有分行符號。  
  
4.  在報表管理員中貼上此 URL，然後按 ENTER 鍵。 報表便會執行，而且文件引導模式會隱藏起來。  
  
> [!NOTE]  
>  如需有關下載範例報表的詳細資訊，請參閱[報表產生器和報表設計師範例報表](http://go.microsoft.com/fwlink/?LinkId=198283)。  
>   
>  如需詳細資訊，請參閱《SQL Server 線上叢書》中 [Reporting Services 文件集](http://go.microsoft.com/fwlink/?linkid=121312) 的＜URL 存取＞。  


更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
