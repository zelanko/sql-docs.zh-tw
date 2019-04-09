---
title: 第 6 課：新增群組和總計 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 945cde51f7529dc31fd7018f1194de600ea1acf5
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241736"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>第 6 課：加入群組和總計 (Reporting Services)
  將群組和總計加入至報表以組織和摘要資料。  
  
 如需中加入報表的資訊，請參閱：[將總計加入到 Reporting Services (SSRS) 報表](https://www.tutorialgateway.org/add-total-and-subtotal-to-ssrs-report/)。  
  
 **本主題內容：**  
  
-   [將報表中的資料分組](#bkmk_groupdata)  
  
-   [在報表中加入總計](#bkmk_addtotals)  
  
-   [在報表中加入每日總計](#bkmk_adddailytotal)  
  
-   [在報表中加入總計](#bkmk_addgrandtotal)  
  
-   [若要將報表發行至報表伺服器 (選擇性)](#bkmk_publishreport)  
  
##  <a name="bkmk_groupdata"></a> 在報表中的群組資料  
  
1.  按一下 **[設計]** 索引標籤。  
  
2.  如果您看不見**資料列群組**窗格中以滑鼠右鍵按一下設計介面，然後按一下**檢視**，然後按一下 **分組**。  
  
3.  從**報表資料**窗格拖曳到`Date`欄位設為**資料列群組**窗格。 將它放在稱為 [(詳細資料)] 之資料列的上方。  
  
     請注意，資料列控制代碼中現在具有一個用來顯示群組的方括號。 資料表現在也具有兩個 [日期] 資料行 – 垂直虛線兩側各有一個。  
  
     ![](../../2014/tutorials/media/rs-basictablegroups1design.gif "rs_BasicTableGroups1Design")  
  
4.  從**報表資料**窗格拖曳到`Order`欄位設為**資料列群組**窗格。 將它放在 [日期] 下方和 [(詳細資料)] 上方。  
  
     請注意，資料列控制代碼中現在具有兩個方括號，用來顯示兩個群組。 資料表現在有兩個`Order`資料行太。  
  
5.  刪除原始的日期和訂單資料行，以**右**雙線。 這樣會移除這個個別記錄值，所以只有群組值會顯示。 選取這兩個資料行的資料行控制代碼，並按一下滑鼠右鍵，然後按一下 [刪除資料行]。  
  
     ![選取要刪除的資料行](../../2014/tutorials/media/rs-basictablegroupsdeletecols.gif "選取要刪除的資料行")  
  
     您可以再次設定資料行標頭和日期的格式。  
  
6.  切換到 **[預覽]** 索引標籤預覽報表。 報表應看起來類似下圖：  
  
     ![依日期和訂單分組的資料表](../../2014/tutorials/media/rs-basictablegroupspreview.gif "依日期和訂單分組的資料表")  
  
##  <a name="bkmk_addtotals"></a> 若要在報表中加入總計  
  
1.  切換至 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下含有 `[LineTotal]` 欄位的資料區資料格，然後按一下 [新增總計]。  
  
     這樣會加入每筆訂單的總金額資料列。  
  
3.  以滑鼠右鍵按一下含有 `[Qty]` 欄位的資料格，然後按一下 [新增總計]。  
  
     這樣會在總計資料列中加入每筆訂單的總數量。  
  
4.  在 `Sum[Qty]`左側的空白資料格中，輸入**訂單總額**標籤。  
  
5.  您也可以在總計資料列中加入背景色彩。 選取兩個總和資料格以及標籤資料格。  
  
6.  在 **[格式]** 功能表上，依序按一下 **[背景色彩]**、 **[淺灰]** 和 **[確定]**。  
  
     ![設計檢視：包含訂單總計的基本資料表](../../2014/tutorials/media/rs-basictablesumlinetotaldesign.gif "設計檢視：包含訂單總計的基本資料表")  
  
##  <a name="bkmk_adddailytotal"></a> 若要加入報表中的每日總計  
  
1.  以滑鼠右鍵按一下 [訂單] 資料格，指向**加入總計**，然後按一下**之後**。  
  
     這會將新增新的資料列包含的數量和金額總和的每一天，而標籤 」**總**」 中排序資料行。  
  
2.  在同一資料格的 **總計** 一詞之前，輸入 **每日** 一詞，使其讀為 **[每日總計]**。  
  
3.  選取 **[每日總計]** 資料格、兩個 **[總和]** 資料格以及它們之間的空白資料格。  
  
4.  在 **[格式]** 功能表上，依序按一下 **[背景色彩]**、 **[橙色]** 和 **[確定]**。  
  
     ![](../../2014/tutorials/media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")  
  
##  <a name="bkmk_addgrandtotal"></a> 將總計加入到報表  
  
1.  以滑鼠右鍵按一下 [日期] 資料格，並指向 [加入總計]，然後按一下 [之後]。  
  
     這會將新增新的資料列包含總和的數量和金額的整份報表，而**總**標記中`Date`資料行。  
  
2.  在同一資料格的 **總計** 一詞之前，輸入 **全部** 一詞，使其讀為 **[全部總計]**。  
  
3.  選取 **[全部總計]** 資料格、兩個 **[總和]** 資料格以及它們之間的空白資料格。  
  
4.  在 **[格式]** 功能表上，依序按一下 **[背景色彩]**、 **[淺藍]** 和 **[確定]**。  
  
     ![設計檢視：基本資料表中的總計](../../2014/tutorials/media/rs-basictablesumgrandtotaldesign.gif "設計檢視：基本資料表中的總計")  
  
5.  按一下 [預覽]。  
  
     最後一頁碼看起來可能如下：  
  
     ![預覽：包含總計的基本資料表](../../2014/tutorials/media/rs-basictablesumgrandtotalpreview.gif "預覽：包含總計的基本資料表")  
  
##  <a name="bkmk_publishreport"></a> 將報表發行至報表伺服器 （選擇性）  
  
1.  選擇性步驟是將已完成的報表發行至原生模式報表伺服器，讓您能夠從報表管理員檢視報表。  
  
2.  在工具列上，按一下 **[專案]** ，然後按一下 **[Tutorial 屬性]**。  
  
3.  在  **TargetServerURL**輸入您的報表伺服器的名稱，例如**http://\<伺服器名稱 > / reportserver**  
  
4.  按一下 **[確定]**。  
  
5.  在工具列上，按一下 **[建置]** ，然後按一下 **[部署教學課程]**。  
  
     如果您在輸出視窗中看見類似下面的訊息，就表示部署成功。  
  
    > ------ 已經開始建立:專案：教學課程，設定：偵錯 ------ 正在略過 'Sales Orders.rdl'。 項目為最新狀態。建立完成 -- 0 個錯誤，0 個警告 ------ 已經開始部署:專案：教學課程，設定：偵錯---部署至 http://\<伺服器名稱 > / 正在回報 ' / 教學課程/Sales Orders'。部署完成--0 個錯誤，0 個警告 === 建置：1 個成功或為最新狀態，0 個失敗，0 個略過 ==================== 部署:1 個成功，0 個失敗，0 個略過 ==========  
  
     如果您看見類似下面的錯誤訊息，請確認自己擁有報表伺服器的權限，而且已經以系統管理員權限啟動 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 。  
  
    > 」 的權限授與使用者 'XXXXXXXX\\< 您的使用者名稱\>' 不足，無法執行此作業 」  
  
6.  比方說，系統管理員權限，啟動報表管理員，以滑鼠右鍵按一下 Internet explorer 的圖示，按一下 **系統管理員身分執行**。  
  
     瀏覽至報表管理員 URL，例如： `http://<server name>/reports`。  
  
7.  瀏覽至包含報表的資料夾，然後按一下 `Sales Orders` 報表的名稱，即可在瀏覽器中檢視轉譯的報表。  
  
## <a name="next-steps"></a>後續步驟  
 您已成功完成「建立基本資料表報表」教學課程。  
  
## <a name="see-also"></a>另請參閱  
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
