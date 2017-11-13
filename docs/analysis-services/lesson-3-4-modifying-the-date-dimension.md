---
title: "修改 Date 維度 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 4689d780-4bf6-4cf8-8fde-eb3f15dd668a
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c514356aeabd59525fdab80e6e1c03f93d9ae34f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-3-4---modifying-the-date-dimension"></a>課程 3-4-修改日期 維度
在這個主題的工作中，您會建立一個使用者定義階層，以及變更針對 [日期]、[月]、[日曆季] 和 [日曆半年] 屬性所顯示的成員名稱。 您也會定義屬性的複合索引鍵、控制維度成員的排序次序，以及定義屬性關聯性。  
  
## <a name="adding-a-named-calculation"></a>加入具名計算  
具名計算是以導出資料行表示的 SQL 運算式，您可以將它加入資料來源檢視的資料表中。 這個運算式以資料表的資料行呈現及運作。 具名計算可讓您延伸資料來源檢視中現有資料表的關聯式結構描述，而不必修改基礎資料來源中的資料表。 如需詳細資訊，請參閱[在資料來源檢視中定義具名計算 &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
#### <a name="to-add-a-named-calculation"></a>加入具名計算  
  
1.  若要開啟 [Adventure Works DW 2012] 資料來源檢視，請在方案總管的 [資料來源檢視] 資料夾中按兩下該檢視。  
  
2.  在靠近 [資料表] 窗格底部的地方，以滑鼠右鍵按一下 [日期]，然後按一下 [新增具名計算]。  
  
3.  在 [建立具名計算] 對話方塊中，於 [資料行名稱] 方塊中輸入 **SimpleDate**，然後在 [運算式] 方塊中輸入或複製和貼上下列 **DATENAME** 陳述式：  
  
    ```  
    DATENAME(mm, FullDateAlternateKey) + ' ' +  
    DATENAME(dd, FullDateAlternateKey) + ', ' +  
    DATENAME(yy, FullDateAlternateKey)  
    ```  
  
    這個 **DATENAME** 陳述式會從 FullDateAlternateKey 資料行中擷取年份、月份和日期等值。 您將使用這個新的資料行當做 FullDateAlternateKey 屬性的顯示名稱。  
  
4.  按一下 [確定]，然後展開 [資料表] 窗格中的 [日期]。  
  
    [SimpleDate] 具名計算會出現在 [日期] 資料表的資料行清單中，並以圖示表示它是具名計算。  
  
5.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
6.  在 [資料表] 窗格中，以滑鼠右鍵按一下 [日期]，然後按一下 [瀏覽資料]。  
  
7.  向右捲動以檢閱 [Explore Date Table (瀏覽日期資料表)] 檢視中的最後一個資料行。  
  
    請注意，[SimpleDate] 資料行出現在資料來源檢視中時，可正確串連基礎資料來源中幾個資料行的資料，而不會修改原始資料來源。  
  
8.  關閉 [Explore Date Table (瀏覽日期資料表)] 檢視。  
  
## <a name="using-the-named-calculation-for-member-names"></a>針對成員名稱使用具名計算  
在資料來源檢視中建立具名計算之後，您就可以使用此具名計算當做屬性 (Attribute) 的屬性 (Property)。  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>針對成員名稱使用具名計算  
  
1.  針對 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [日期] 維度，開啟 [維度設計師]。 若要這樣做，請在**方案總管**的 [維度] 節點中，按兩下 [日期] 維度。  
  
2.  在 [維度結構] 索引標籤的 [屬性] 窗格中，按一下 [日期索引鍵] 屬性。  
  
3.  如果 [屬性] 視窗未開啟，請開啟 [屬性] 視窗，然後按一下標題列上的 [自動隱藏] 按鈕，如此它就會保持開啟狀態。  
  
4.  在靠近視窗底部的地方按一下 [NameColumn] 屬性欄位，然後按一下省略符號瀏覽 (**…**) 按鈕，即可開啟 [名稱資料行] 對話方塊。  
  
5.  選取 [來源資料行] 清單底部的 [SimpleDate]，然後按一下 [確定]。  
  
6.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="creating-a-hierarchy"></a>建立階層  
您可以將屬性從 [屬性] 窗格拖曳到 [階層] 窗格，藉以建立新的階層。  
  
#### <a name="to-create-a-hierarchy"></a>若要建立階層  
  
1.  在 [日期] 維度的 [維度設計師] 中，將 [維度結構] 索引標籤中的 [日曆年度] 屬性從 [屬性] 窗格拖曳到 [階層] 窗格中。  
  
2.  將 [日曆半年度] 屬性從 [屬性] 窗格拖曳到 [階層] 窗格的 [<new level>] 資料格中 (位於 [日曆年度] 層級底下)。  
  
3.  將 [日曆季] 屬性從 [屬性] 窗格拖曳到 [階層] 窗格的 [<new level>] 資料格中 (位於 [日曆半年度] 層級底下)。  
  
4.  將 [英文月份] 屬性從 [屬性] 窗格拖曳到 [階層] 窗格的 [<new level>] 資料格中 (位於 [日曆季] 層級底下)。  
  
5.  將 [日期索引鍵] 屬性從 [屬性] 窗格拖曳到 [階層] 窗格的 [<new level>] 資料格中 (位於 [英文月份] 層級底下)。  
  
6.  在 [階層] 窗格中，以滑鼠右鍵按一下 [階層] 階層的標題列，按一下 [重新命名]，然後輸入**日曆日期**。  
  
7.  藉由使用滑鼠右鍵操作功能表，在 [日曆日期] 階層中，將 [英文月份] 層級重新命名為**日曆月份**，並將 [日期索引鍵] 層級重新命名為**日期**。  
  
8.  從 [屬性] 窗格中刪除 [完整日期替代索引鍵] 屬性，因為您將不會再使用它。 在 [刪除物件] 確認視窗中按一下 [確定]。  
  
9. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="defining-attribute-relationships"></a>定義屬性關聯性  
如果基礎資料支援屬性關聯性，您就應該定義屬性之間的屬性關聯性。 定義屬性關聯性可加快維度、資料分割和查詢處理的速度。  
  
#### <a name="to-define-attribute-relationships"></a>定義屬性關聯性  
  
1.  在 [日期] 維度的 [維度設計師] 中，按一下 [屬性關聯性] 索引標籤。  
  
2.  在圖表中，以滑鼠右鍵按一下 [英文月份] 屬性，然後按一下 [新增屬性關聯性]。  
  
3.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [英文月份]。 將 [相關屬性] 設定為 [日曆季]。  
  
4.  在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
    此關聯性類型是 [固定]，因為成員之間的關聯性不會隨著時間而變更。  
  
5.  按一下 **[確定]**。  
  
6.  在圖表中，以滑鼠右鍵按一下 [日曆季] 屬性，然後按一下 [新增屬性關聯性]。  
  
7.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [日曆季]。 將 [相關屬性] 設定為 [日曆半年度]。  
  
8.  在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
9. 按一下 **[確定]**。  
  
10. 在圖表中，以滑鼠右鍵按一下 [日曆半年度] 屬性，然後按一下 [新增屬性關聯性]。  
  
11. 在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [日曆半年度]。 將 [相關屬性] 設定為 [日曆年度]。  
  
12. 在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
13. 按一下 **[確定]**。  
  
14. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="providing-unique-dimension-member-names"></a>提供唯一的維度成員名稱  
在這項工作中，您將建立 [EnglishMonthName]、[CalendarQuarter] 和 [CalendarSemester] 屬性所使用的使用者易記名稱資料行。  
  
#### <a name="to-provide-unique-dimension-member-names"></a>提供唯一的維度成員名稱  
  
1.  若要切換至 [[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012] 資料來源檢視，請在方案總管的 [資料來源檢視] 資料夾中按兩下該檢視。  
  
2.  在 [資料表] 窗格中，以滑鼠右鍵按一下 [日期]，然後按一下 [新增具名計算]。  
  
3.  在 [建立具名計算] 對話方塊的 [資料行名稱] 方塊中輸入 **MonthName**，然後在 [運算式] 方塊中輸入或複製並貼上下列陳述式：  
  
    ```  
    EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)  
    ```  
  
    這個陳述式會將資料表中的每一個月的月份和年份串連成新的資料行。  
  
4.  按一下 **[確定]**。  
  
5.  在 [資料表] 窗格中，以滑鼠右鍵按一下 [日期]，然後按一下 [新增具名計算]。  
  
6.  在 [建立具名計算] 對話方塊的 [資料行名稱] 方塊中輸入 **CalendarQuarterDesc**，然後在 [運算式] 方塊中輸入或複製並貼上下列 SQL 指令碼：  
  
    ```  
    'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY ' +  
    CONVERT(CHAR (4), CalendarYear)  
    ```  
  
    這個 SQL 指令碼會將資料表中每一季的日曆季和年份串連成新的資料行。  
  
7.  按一下 **[確定]**。  
  
8.  在 [資料表] 窗格中，以滑鼠右鍵按一下 [日期]，然後按一下 [新增具名計算]。  
  
9. 在 [建立具名計算] 對話方塊的[資料行名稱] 方塊中輸入 **CalendarSemesterDesc**，然後在 [運算式] 方塊中輸入或複製並貼上下列 SQL 指令碼：  
  
    ```  
    CASE  
    WHEN CalendarSemester = 1 THEN 'H1' + ' ' + 'CY' + ' '   
           + CONVERT(CHAR(4), CalendarYear)  
    ELSE  
    'H2' + ' ' + 'CY' + ' ' + CONVERT(CHAR(4), CalendarYear)  
    END  
    ```  
  
    這個 SQL 指令碼會將資料表中每半年度的日曆半年度和年份串連成新的資料行。  
  
10. 按一下 **[確定].**  
  
11. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="defining-composite-keycolumns-and-setting-the-name-column"></a>定義複合 KeyColumns 並設定名稱資料行  
[KeyColumns] 屬性 (property) 包含代表屬性 (attribute) 之索引鍵的一或多個資料行。 在這項工作中，您將會定義複合 [KeyColumns]。  
  
#### <a name="to-define-composite-keycolumns-for-the-english-month-name-attribute"></a>針對 [英文月份] 屬性定義複合 KeyColumns  
  
1.  針對 [日期] 維度開啟 [維度結構] 索引標籤。  
  
2.  在 [屬性] 窗格中，按一下 [英文月份] 屬性。  
  
3.  在 [屬性] 視窗的 [KeyColumns] 欄位中按一下，然後按一下瀏覽 (**...**) 按鈕。  
  
4.  在 [索引鍵資料行] 對話方塊的 [可用的資料行] 清單中，選取 [CalendarYear] 資料行，然後按一下 [>] 按鈕。  
  
5.  [EnglishMonthName] 和 [CalendarYear] 資料行現在會顯示在 [索引鍵資料行] 清單中。  
  
6.  按一下 **[確定]**。  
  
7.  若要設定 [EnglishMonthName] 屬性 (attribute) 的 [NameColumn] 屬性 (property)，請按一下 [屬性] 視窗中的 [NameColumn] 欄位，然後按一下瀏覽 (**...**) 按鈕。  
  
8.  在 [名稱資料行] 對話方塊的 [來源資料行] 清單中，選取 [MonthName]，然後按一下 [確定]。  
  
9. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-quarter-attribute"></a>若要針對 [日曆季] 屬性定義複合 KeyColumns  
  
1.  在 [屬性] 窗格中，按一下 [日曆季] 屬性。  
  
2.  在 [屬性] 視窗的 [KeyColumns] 欄位中按一下，然後按一下瀏覽 (**...**) 按鈕。  
  
3.  在 [索引鍵資料行] 對話方塊的 [可用的資料行] 清單中，選取 [CalendarYear] 資料行，然後按一下 [>] 按鈕。  
  
    [CalendarQuarter] 和 [CalendarYear] 資料行現在會顯示在 [索引鍵資料行] 清單中。  
  
4.  按一下 **[確定]**。  
  
5.  若要設定 [日曆季] 屬性 (attribute) 的 [NameColumn] 屬性 (property)，請按一下 [屬性] 視窗中的 [NameColumn] 欄位，然後按一下瀏覽 (**...**) 按鈕。  
  
6.  在 [名稱資料行] 對話方塊的 [來源資料行] 清單中，選取 [CalendarQuarterDesc]，然後按一下 [確定]。  
  
7.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-semester-attribute"></a>若要針對 [日曆半年] 屬性定義複合 KeyColumns  
  
1.  在 [屬性] 窗格中，按一下 [日曆半年度] 屬性。  
  
2.  在 [屬性] 視窗的 [KeyColumns] 欄位中按一下，然後按一下瀏覽 (**...**) 按鈕。  
  
3.  在 [索引鍵資料行] 對話方塊的 [可用的資料行] 清單中，選取 [CalendarYear] 資料行，然後按一下 [>] 按鈕。  
  
    [CalendarSemester] 和 [CalendarYear] 資料行現在會顯示在 [索引鍵資料行] 清單中。  
  
4.  按一下 **[確定]**。  
  
5.  若要設定 [日曆半年度] 屬性 (attribute) 的 [NameColumn] 屬性 (property)，請按一下 [屬性] 視窗中的 [NameColumn] 欄位，然後按一下瀏覽 (**...**) 按鈕。  
  
6.  在 [名稱資料行] 對話方塊的 [來源資料行] 清單中，選取 [CalendarSemesterDesc]，然後按一下 [確定]。  
  
7.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="deploying-and-viewing-the-changes"></a>部署和檢視變更  
在變更屬性和階層之後，您必須部署變更及重新處理相關物件，然後才可以檢視變更。  
  
#### <a name="to-deploy-and-view-the-changes"></a>部署和檢視變更  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
2.  當您收到 [已成功地完成部署] 訊息之後，請針對 [日期] 維度按一下 [維度設計師] 的 [瀏覽器] 索引標籤，然後按一下設計師工具列上的 [重新連接] 按鈕。  
  
3.  從 [階層] 清單中，選取 [日曆季]。 檢閱 [日曆季] 屬性階層中的成員。  
  
    請注意，[日曆季] 屬性階層的成員名稱會更清楚且更容易使用，因為您建立了要當作名稱使用的具名計算。 現在成員位於每個年度中每個季度的 [日曆季] 屬性階層中。 成員不是依時間順序排序。 而是先按季再按年排序。 在這個主題的下一項工作中，您會修改先按季再按年排序這個屬性階層成員的行為。  
  
4.  檢閱 [英文月份] 和 [日曆半年度] 屬性階層的成員。  
  
    請注意，這些階層的成員也未按照時間順序排列， 而是分別按月或按半年度再按年來排序。 在這個主題的下一項工作中，您會修改這個行為來變更這種排序順序。  
  
## <a name="changing-the-sort-order-by-modifying-composite-key-member-order"></a>修改複合索引鍵成員順序來變更排序順序  
在這項工作中，您將會透過變更組成複合索引鍵之索引鍵的順序，變更排序次序。  
  
#### <a name="to-modify-the-composite-key-member-order"></a>若要修改複合索引鍵成員順序  
  
1.  在 [日期] 維度的 [維度設計師] 中開啟 [維度結構] 索引標籤，然後在 [屬性] 窗格中選取 [日曆半年度]。  
  
2.  在 [屬性] 視窗中，檢閱 [OrderBy] 屬性的值。 它會設定為 [索引鍵]。  
  
    [日曆半年度] 屬性階層的成員會按照其索引鍵值進行排序。 利用複合索引鍵，成員索引鍵的排序是先依據第一個成員索引鍵的值，再依據第二個成員索引鍵的值。 換言之，[日曆半年度] 屬性階層的成員是先按半年度再按年度進行排序。  
  
3.  在 [屬性] 視窗中，按一下省略符號瀏覽按鈕 (**...**) 變更 [KeyColumns] 屬性值。  
  
4.  在 [索引鍵資料行] 對話方塊的 [索引鍵資料行] 清單中，確認已選取 [CalendarSemester]，然後按一下向下箭號，讓這個複合索引鍵之成員的順序相反。 按一下 **[確定]**。  
  
    屬性階層的成員現在變成先按年再按半年度排序。  
  
5.  在 [屬性] \(attribute) 窗格中選取 [日曆季]，然後在 [屬性] \(property) 視窗中按一下 [KeyColumns] 屬性 (property) 的省略符號瀏覽按鈕 (**...**)。  
  
6.  在 [索引鍵資料行] 對話方塊的 [索引鍵資料行] 清單中，確認已選取 [CalendarQuarter]，然後按一下向下箭號，讓這個複合索引鍵之成員的順序相反。 按一下 **[確定]**。  
  
    屬性階層的成員現在變成先按年再按季排序。  
  
7.  在 [屬性]\ (attribute) 窗格中選取 [英文月份]，然後在 [屬性] \(property) 視窗中按一下 [KeyColumns] 屬性 (property) 的省略符號按鈕 (**...**)。  
  
8.  在 [索引鍵資料行] 對話方塊的 [索引鍵資料行] 清單中，確認已選取 [EnglishMonthName]，然後按一下向下箭號，讓這個複合索引鍵之成員的順序相反。 按一下 **[確定]**。  
  
    屬性階層的成員現在變成先按年再按月排序。  
  
9. 在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。 順利完成部署之後，在 [日期] 維度的 [維度設計師] 中按一下 [瀏覽器] 索引標籤。  
  
10. 在 [瀏覽器] 索引標籤的工具列上，按一下 [重新連接] 按鈕。  
  
11. 檢閱 [日曆季] 和 [日曆半年度] 屬性階層的成員。  
  
    請注意，這些階層的成員現在已按照時間順序排列了，它們是先按年再按季或半年度來排序。  
  
12. 檢閱 [英文月份] 屬性階層的成員。  
  
    請注意，現在階層的成員會先依年排序，然後依月按字母順序排序。 這是因為依據關聯式資料庫中的 nvarchar 資料類型，在資料來源檢視中 EnglishCalendarMonth 資料行的資料類型為字串資料行。 如需如何讓每年的月份按時間順序排序的資訊，請參閱 [依次要屬性來排序屬性成員](../analysis-services/lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md)。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[瀏覽已部署的 Cube](../analysis-services/lesson-3-5-browsing-the-deployed-cube.md)  
  
## <a name="see-also"></a>另請參閱  
[多維度模型中的維度](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
  

