---
title: 第 6 課：新增群組和總計 (Reporting Services) | Microsoft Docs
ms.date: 04/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b5b9846a20615cf613dd50752ac63f2669b1e399
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089670"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lesson 6: Adding Grouping and Totals (Reporting Services)

在最終的教學課程中，您會將群組和總計新增至 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表以組織和摘要資料。  

## <a name="to-group-data-in-a-report"></a>將報表中的資料分組

1. 選取 [設計] 索引標籤。
2. 如果您看不到 [資料列群組] 窗格，請以滑鼠右鍵按一下設計介面，然後選取 [檢視] >[群組]。
3. 將 `[Date]` 欄位從 [報表資料] 窗格拖曳到 [資料列群組] 窗格。 將其放置在顯示為 **= (詳細資料)** 的資料列上方。

    > [!NOTE]
    > 請注意，資料列控制代碼中現在具有一個用來表示群組的方括號。 資料表現在也具有兩個 `[Date]` 運算式資料行，垂直虛線兩側各有一個。
    >
    >![新增的日期群組](media/rs-basictablegroups1design.png "新增的日期群組")
4. 將 `[Order]` 欄位從 [報表資料] 窗格拖曳到 [資料列群組] 窗格。 將其放置在 [日期] 下方和 **= (詳細資料))** 上方。

    ![ssrs_ssdt_addorderfield](media/ssrs-ssdt-addorderfield.png)

    > [!NOTE]
    > 請注意，資料列控制代碼中現在具有兩個方括號 ![ssrs_ssdt_rowgroupdoublehandles](media/ssrs-ssdt-rowgroupdoublehandles.png)，用以表示兩個群組。 資料表現在也有兩個 `[Order]` 運算式資料行。

5. 刪除雙線右側的原始 `[Date]` 和 `[Order]` 運算式資料行。 選取這兩個資料行的資料行控制代碼，並按一下滑鼠右鍵，然後選取 [刪除資料行]。 報表設計師會移除個別資料列的運算式，因此只會顯示群組運算式。

    ![選取要刪除的資料行](media/rs-basictablegroupsdeletecols.gif "選取要刪除的資料行")

6. 若要設定 `[Date]` 資料行的格式，以滑鼠右鍵按一下包含 `[Date]` 運算式的資料區資料格，然後選取 [文字方塊屬性]。
7. 在最左邊的資料行清單方塊中選取 [數字]，然後從 [類別] 清單方塊中選取 [日期]。
8. 在 [類型] 清單方塊中，選取 [January 31, 2000]。
9. 選取 [確定] 來套用格式。
10. 再次預覽報表。 它看起來應該如下：

    ![rs_BasicTableGroupsPreview](media/rs-basictablegroupspreview.png)

## <a name="adding-totals-to-a-report"></a>在報表中加入總計

1. 切換至 [設計] 檢視。
2. 以滑鼠右鍵按一下含有 `[LineTotal]` 運算式的資料區資料格，然後選取 [加入總計]。 報表設計師會加入含有每筆訂單總金額的資料列。
3. 以滑鼠右鍵按一下含有 `[Qty]` 欄位的資料格，然後選取 [加入總計]。 報表設計師會在總計資料列中加入每筆訂單的總數量。
4. 在 `Sum[Qty]` 資料格左側的空白資料格中，輸入「訂單總額」字串。
5. 您也可以在總計資料列中加入背景色彩。 選取兩個總和資料格以及標籤資料格。  
6. 從 [格式] 功能表上，選取[背景色彩] > [淺灰] 正方形。
7. 選取 [確定] 來套用格式。

   ![設計檢視：具有訂單總計的基本資料表](media/rs-basictablesumlinetotaldesign.gif "設計檢視：具有訂單總計的基本資料表")

## <a name="add-the-daily-total-to-the-report"></a>在報表中加入每日總計

1. 以滑鼠右鍵按一下 `[Order]` 運算式資料格，然後選取 [加入總計] > [之後]。 報表設計師會針對每一天加入含有 `[Qty]` 和 `[Linetotal]` 值加總的新資料列，並在 `[Order]` 運算式資料行底部加入「總計」字串。
2. 在同一資料格的「總計」一詞之前，輸入「每日」一詞，使其讀為「每日總計」。
3. 選取該儲存格和右側的兩個相鄰資料格，以及兩者之間的空白資料格。
4. 從 [格式] 功能表上，選取[背景色彩] > [橙色] 正方形。
5. 選取 [確定] 來套用格式。

   ![將背景色彩設定為橙色](media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")

## <a name="add-the-grand-total-to-the-report"></a>在報表中加入總計

1. 以滑鼠右鍵按一下 `[Date]` 運算式資料格，然後選取 [加入總計] > [之後]。 報表設計師會針對整份報表，加入含有 `[Qty]` 和 `[LineTotal]` 值加總的新資料列，並在 `[Date]` 運算式資料行底部加入「總計」字串。
2. 在同一資料格的「總計」一詞之前，輸入「全部」字串，使其讀為「全部總計」。
3. 選取「全部總計」資料格、兩個 `Sum()` 運算式資料格，以及兩者之間的空白資料格。
4. 從 [格式] 功能表上，選取[背景色彩] > [淺藍] 正方形。
5. 選取 [確定] 來套用格式。

    ![設計檢視：基本資料表中的總計](media/rs-basictablesumgrandtotaldesign.gif "設計檢視：基本資料表中的總計")

## <a name="preview-the-report"></a>預覽報表

若要預覽格式變更，請選取 [預覽] 索引標籤。在 [預覽] 工具列中，選取 [最後一頁] 按鈕，如下所示 ![ssrs_ssdt_viewertoolbar_lastpage](media/ssrs-ssdt-viewertoolbar-lastpage.png)。 結果應該會顯示如下：

   ![預覽：具有總計的基本資料表](media/rs-basictablesumgrandtotalpreview.gif "預覽：具有總計的基本資料表")

## <a name="publishing-the-report-to-the-report-server-optional"></a>將報表發佈至*報表伺服器* (選擇性)

選擇性步驟是將已完成的報表發佈至報表伺服器，讓您能夠在入口網站中檢視報表。

1. 選取 [專案] 功能表 > [教學課程屬性...]
2. 在 **TargetServerURL** 中，輸入報表伺服器的名稱，例如：
    - `http:/<servername>/reportserver` 或
    - 在報表伺服器上設計報表時可用 `https://localhost/reportserver`。

3. **TargetReportFolder** 是從專案名稱命名的教學課程。 報表設計師會將報表部署到此資料夾。
4. 選取 [確定]。
5. 選取 [建置]功能表 > [部署教學課程]。

    如果您在 [輸出] 視窗中看見類似如下的訊息，就表示部署成功。

    > ------ 已經開始建立: 專案: tutorial，組態: 偵錯 ------  
    > 正在略過 'Sales Orders.rdl'。 項目已是最新版本。  
    > 建立已完成 -- 0 個錯誤，0 個警告  
    > ------ 已經開始部署: 專案: tutorial，組態: 偵錯 ------  
    > 正在部署至 `https://[server name]/reportserver`  
    > 正在部署報表 '/tutorial/Sales Orders'。  
    > 部署已完成 -- 0 個錯誤，0 個警告  
    > ========== 建置: 1 個成功或最新狀態，0 個失敗，0 個略過 ==========  
    > ========== 部署: 1 個成功，0 個失敗，0 個略過 ==========  

    如果您看見類似如下的錯誤訊息，請確認您擁有報表伺服器的適當權限，而且已經以系統管理員權限啟動 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]。
    >
    > 「授與使用者 'XXXXXXXX\\[您的使用者名稱]' 的權限不足，無法執行此作業」

6. 以系統管理員權限開啟瀏覽器。 例如，以滑鼠右鍵按一下 Internet Explorer 的圖示，然後選取 [以系統管理員身分執行]。
7. 瀏覽至入口網站 URL。
   - 第 1 課：建立 Windows Azure 儲存體物件`https://<server name>/reports`。
   - 在報表伺服器上設計報表時可用 `https://localhost/reports`。

8. 選取 [教學課程] 資料夾，然後選取「銷售訂單」報表，以檢視該報表。

    ![ssrs_tutorial_tutorialfolder](media/ssrs-tutorial-tutorialfolder.png)  

您已成功完成**建立基本資料表報表教學課程**。

## <a name="see-also"></a>另請參閱

[篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)
