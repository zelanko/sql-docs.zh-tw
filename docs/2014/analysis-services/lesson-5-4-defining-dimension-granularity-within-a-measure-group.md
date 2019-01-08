---
title: 定義量值群組內的維度資料粒度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 4f079485-9eb4-405c-9a20-81258298b810
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1d7b619cb711938f07ae7902dc1b9544adc5890
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512295"
---
# <a name="defining-dimension-granularity-within-a-measure-group"></a>在量值群組內定義維度資料粒度
  使用者希望維度事實資料基於不同的用途有不同的資料粒度或具體性。 例如可能記錄每一天轉售商的銷售資料或網際網路銷售，但銷售配額資訊可能只有當月或當季才有。 在這些案例中，使用者希望時間維度對每一個不同的事實資料表有不同的資料粒度或詳細層級。 雖然您能夠以這種不同的資料粒度將新資料庫維度定義為時間維度，但有更容易的方法，就是使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
 根據預設，在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中，當維度使用於量值群組內，該維度內的資料粒度是以維度的索引鍵屬性為基礎。 例如，當 [時間] 維度是包括在量值群組內，且 [時間] 維度的預設資料粒度是每天，則量值群組內的該維度的預設資料粒度就是每天。 這適合許多情況，例如本教學課程中的 [網際網路銷售] 和 [轉售商銷售] 量值群組。 不過，當這種維度包含在其他類型的量值群組中，例如在銷售配額或預算量值群組中，則每月或每季資料粒度會更加適合。  
  
 若要對 Cube 維度指定預設資料粒度以外的資料粒度，您必須在 [Cube 設計師] 的 [維度使用方式] 索引標籤上，修改特定量值群組內使用的 Cube 維度的資料粒度屬性。 當您將特定量值群組內的維度資料粒度變更為該維度的索引鍵屬性以外的屬性時，必須保證該量值群組中的所有其他屬性均與新的資料粒度屬性直接或間接相關。 您可以在所有其他屬性與指定為量值群組中的資料粒度屬性的那個屬性之間指定屬性關聯性，來達到這個目的。 在本案例中，您會定義其他的屬性關聯性，而不是移動屬性關聯性。 實際上，對維度中的其餘屬性來說，指定為資料粒度屬性的屬性會成為量值群組內的索引鍵屬性。 如果您未適當地指定屬性關聯性， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 將無法正確彙總各值，您將在這個主題的工作中看到這種情況。  
  
 如需詳細資訊，請參閱 [維度關聯性](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)、 [定義一般關聯性及一般關聯性屬性](multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)。  
  
 在這個主題的工作中，您會加入 [銷售配額] 量值群組，以及在這個量值群組中將 [日期] 維度的資料粒度定義為每月。 然後您會在月份屬性和其他維度屬性之間定義屬性關聯性，以確定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 可正確彙總各值。  
  
## <a name="adding-tables-and-defining-the-sales-quotas-measure-group"></a>加入資料表及定義 [銷售配額] 量值群組  
  
1.  請切換到 [Adventure Works DW 2012] 資料來源檢視。  
  
2.  中的任何位置按一下滑鼠右鍵**圖表組合管理**窗格中，按一下**新圖表**，然後將圖表命名`Sales Quotas`。  
  
3.  拖曳**員工**， **Sales Territory**，並`Date`從資料表**資料表**窗格**圖表**窗格。  
  
4.  以滑鼠右鍵按一下 [圖表] 窗格中的任何位置，並選取 [加入/移除資料表] 即可將 [FactSalesQuota] 資料表加入 [圖表] 窗格中。  
  
     請注意，[SalesTerritory] 資料表是透過 [員工] 資料表而連結到 [FactSalesQuota] 資料表。  
  
5.  檢閱 [FactSalesQuota] 資料表中的資料行，然後瀏覽這個資料表中的資料。  
  
     請注意，這個資料表內的資料粒度是日曆季，這是 [FactSalesQuota] 資料表的最低層級詳細資料。  
  
6.  在 資料來源檢視設計師，變更**FriendlyName**屬性**FactSalesQuota**資料表`SalesQuotas`。  
  
7.  請切換到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程的 Cube，然後按一下 [Cube 結構] 索引標籤。  
  
8.  中的任何位置按一下滑鼠右鍵**量值**窗格中，按一下**新的量值群組**，按一下 `SalesQuotas`中**新的量值群組**對話方塊方塊，然後再按一下  **確定**。  
  
     `Sales Quotas`量值群組會出現在**量值**窗格。 在 **維度**窗格中，請注意，新`Date`也定義 cube 維度，根據`Date`資料庫維度。 會定義新的時間相關 Cube 維度，是因為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不知道 [FactSalesQuota] 事實資料表中的 [DateKey] 資料行是與哪一個現有的時間相關 Cube 維度有關，這個事實資料表就是 Sales Quotas 量值群組的基礎。 稍後您會在這個主題的另一項工作中加以變更。  
  
9. 展開`Sales Quotas`量值群組。  
  
10. 在 [量值] 窗格中，選取 [銷售量配額]，然後在 [屬性] 視窗中將 [FormatString] 屬性的值設為 [貨幣]。  
  
11. 選取 [**銷售配額計數**量值，並鍵入`#,#`做為值**FormatString**屬性] 視窗中的屬性。  
  
12. 刪除**日曆季**量值從`Sales Quotas`量值群組。  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 偵測到作為 [日曆季] 量值基礎的資料行是包含量值的資料行。 不過，這個資料行和 CalendarYear 資料行都包含您稍後在這個主題中用於連結 [銷售配額] 量值群組與 [日期] 維度的值。  
  
13. 在 **量值**窗格中，以滑鼠右鍵按一下`Sales Quotas`量值群組，然後按一下**新的量值**。  
  
     此時會開啟 [新增量值] 對話方塊，它包含使用類型為 [總和] 的量值可用的來源資料行。  
  
14. 在 **新的量值**對話方塊方塊中，選取**相異計數量**中**使用量**清單中，確認`SalesQuotas`中選取**來源資料表**清單中，選取**EmployeeKey**中**來源資料行**清單，然後再按**確定**。  
  
     請注意，量值是建立在一個叫作 [銷售配額 1] 的新量值群組中。 而 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的相異計數量值則建立在其自己的量值群組中，以使處理效能最大化。  
  
15. 值變更**名稱**屬性**員工索引鍵相異計數**量值加入`Sales Person Count`，然後輸入`#,#`的值為**FormatString**屬性。  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>按日期瀏覽銷售配額量值群組中的量值  
  
1.  在 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
2.  順利完成部署之後，針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube，按一下 [Cube 設計師] 的 [瀏覽器] 索引標籤，然後按一下 [重新連接] 按鈕。  
  
3.  按一下 Excel 捷徑，然後按一下 [啟用]。  
  
4.  在樞紐分析表欄位清單中，依序展開`Sales Quotas`量值群組，並將拖曳**銷售量配額**量值加入 [值] 區域。  
  
5.  展開 [銷售領域] 維度，然後將 [銷售領域] 使用者定義階層拖曳至 [資料列標籤]。  
  
     請注意，[銷售領域] Cube 維度與 [事實銷售配額] 資料表並無直接或間接關係，如下圖所示。  
  
     ![銷售區域 cube 維度](../../2014/tutorials/media/l5-granularity-2.gif "銷售區域 cube 維度")  
  
     在這個主題的下一系列的步驟中，您將會在這個維度與這個事實資料表之間定義參考維度關聯性。  
  
6.  將 [銷售領域] 使用者階層從 [資料列標籤] 區域移至 [資料行標籤] 區域。  
  
7.  在樞紐分析表欄位清單中，選取 [銷售領域] 使用者定義階層，然後按一下右側的向下箭號。  
  
     ![在欄位清單中的銷售領域階層](../../2014/tutorials/media/l5-granularity-1a.png "欄位清單中的銷售領域階層")  
  
8.  在篩選中，按一下 [全選] 核取方塊以清除所有選取項目，然後只選擇 [北美洲]。  
  
     ![篩選窗格來選取北美](../../2014/tutorials/media/l5-granularity-1b.png "來選取北美的篩選窗格")  
  
9. 在樞紐分析表欄位清單中，展開  `Date`。  
  
10. 將 [Date.Fiscal Date] 使用者階層拖曳至 [資料列標籤]  
  
11. 在樞紐分析表上，按一下 [資料列標籤] 旁邊的向下鍵。 清除 [FY 2008] 之外的所有年份。  
  
     請注意，只有**2007 年 7 月**隸屬**月份**層級隨即出現，而不是**2007 年 7 月，**， **2007 年 8 月，**，以及**2007 年 9 月，** 的成員**月份**層級，而且只有**2007 年 7 月 1 日**隸屬`Date`層級隨即出現，而不是全部的 31 天。 會發生此問題的事實資料表中的資料粒度是在季層級，而資料粒度的`Date`維度是每日層級。 您會在這個主題的下一項工作中變更這種行為。  
  
     同樣也請注意，月和日層級的 [銷售量配額] 值與季層級的值相同，都是 $13,733,000.00。 這是因為 [銷售配額] 量值群組中的資料最低層級是在季層級。 您會在第 6 課變更這種行為。  
  
     下圖顯示 [銷售量配額] 的值。  
  
     ![值的銷售金額配額](../../2014/tutorials/media/l5-granularity-3.png "值 Sales Amount，配額")  
  
## <a name="defining-dimension-usage-properties-for-the-sales-quotas-measure-group"></a>定義 [銷售配額] 量值群組的維度使用方式屬性  
  
1.  針對 [員工] 維度開啟 [維度設計師]，以滑鼠右鍵按一下 [資料來源檢視] 窗格中的 [SalesTerritoryKey]，然後按一下 [從資料行新增屬性]。  
  
2.  在 [屬性] (attribute) 窗格中，選取 [SalesTerritoryKey]，然後在 [屬性] (property) 視窗中，將 [AttributeHierarchyVisible] 屬性 (property) 設定為 [False]、將 [AttributeHierarchyOptimizedState] 屬性 (property) 設定為 [NotOptimized]，並且將 [AttributeHierarchyOrdered] 屬性 (property) 設定為 [False]。  
  
     這個屬性，才能連結**Sales Territory**維度`Sales Quotas`並**銷售配額 1**量值群組成為參考維度。  
  
3.  在 Cube 設計師[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]教學課程 cube，按一下**維度使用方式**索引標籤，然後再檢閱內的維度使用方式`Sales Quotas`並**銷售配額 1**量值群組。  
  
     請注意，**員工**並`Date`cube 維度連結至**銷售 Quotasand 銷售配額 1**量值群組，透過一般關聯性。 也請注意，[銷售領域] Cube 維度並未連結到其中任何量值群組。  
  
4.  按一下資料格的交集處**Sales Territory**維度並`Sales Quotas`量值群組，然後按一下 瀏覽按鈕 (**...**).此時會開啟 定義關聯性 對話方塊。  
  
5.  在 [選取關聯性類型] 清單中，選取 [參考的]。  
  
6.  在 [中繼維度] 清單中，選取 [員工]。  
  
7.  在 [參考維度屬性] 清單中，選取 [銷售領域地區]。  
  
8.  在 [中繼維度屬性] 清單中，選取 [銷售領域索引鍵]。 ([銷售領域地區] 屬性的索引鍵資料行是 SalesTerritoryKey 資料行)。  
  
9. 確認已選取 [具體化] 核取方塊。  
  
10. 按一下 [確定] 。  
  
11. 按一下資料格的交集處**Sales Territory**維度並**銷售配額 1**量值群組，然後按一下 瀏覽按鈕 (**...**).此時會開啟 定義關聯性 對話方塊。  
  
12. 在 [選取關聯性類型] 清單中，選取 [參考的]。  
  
13. 在 [中繼維度] 清單中，選取 [員工]。  
  
14. 在 [參考維度屬性] 清單中，選取 [銷售領域地區]。  
  
15. 在 [中繼維度屬性] 清單中，選取 [銷售領域索引鍵]。 ([銷售領域地區] 屬性的索引鍵資料行是 SalesTerritoryKey 資料行)。  
  
16. 確認已選取 [具體化] 核取方塊。  
  
17. 按一下 [確定] 。  
  
18. 刪除`Date`cube 維度。  
  
     您不需要四個時間相關 cube 維度，您將使用**訂單日期**中的 cube 維度`Sales Quotas`做為日期的銷售配額會對其建立維度的量值群組。 您也會使用這個 Cube 維度做為 Cube 中的主要日期維度。  
  
19. 在 **維度**清單中，重新命名**訂單日期**cube 維度，以便`Date`。  
  
     重新命名**訂單日期**cube 維度，以便`Date`容易了解其角色是扮演主要日期維度在這個 cube 中的使用者。  
  
20. 按一下 瀏覽按鈕 (**...**) 的交集處的儲存格中`Sales Quotas`量值群組和`Date`維度。  
  
21. 在 [定義關聯性] 對話方塊中，選取 [選取關聯性類型] 清單中的 [一般]。  
  
22. 在 [資料粒度屬性] 清單中，選取 [日曆季]。  
  
     請注意，會出現警告通知您，因為您已選取非索引鍵屬性做為資料粒度屬性，所以必須以指定為成員屬性的方式，來確定所有其他屬性均與資料粒度屬性直接或間接有關。  
  
23. 在 [定義關聯性] 對話方塊的 [關聯性] 區域中，將 [日期] Cube 維度之基礎資料表中的 [CalendarYear] 及 [CalendarQuarter] 維度資料行，與 [銷售配額] 量值群組之基礎資料表中的 [CalendarYear] 及 [CalendarQuarter] 資料行相連結，然後按一下 [確定]。  
  
    > [!NOTE]  
    >  「日曆季」是定義為「銷售配額」量值群組中之日期 Cube 維度的資料粒度屬性，但 [日期] 屬性仍會是「網際網路銷售」及「轉售商銷售」量值群組的資料粒度屬性。  
  
24. 對 [銷售配額 1] 量值群組重複前面 4 個步驟。  
  
## <a name="defining-attribute-relationships-between-the-calendar-quarter-attribute-and-the-other-dimension-attributes-in-the-date-dimension"></a>在日曆季屬性和日期維度的其他維度屬性之間定義屬性關聯性  
  
1.  切換至**維度設計師**for`Date`維度，然後再按**屬性關聯性** 索引標籤。  
  
     請注意，雖然**日曆年度**連結至**日曆季**透過**日曆半年度**屬性，會計日曆屬性只連結到其中一個另一個，未連結至**日曆季**屬性，因此將不會彙總正確`Sales Quotas`量值群組。  
  
2.  在圖表中，以滑鼠右鍵按一下 [日曆季] 屬性，然後選取 [新增屬性關聯性]。  
  
3.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [日曆季]。 將 [相關屬性] 設定為 [會計季度]。  
  
4.  按一下 [確定] 。  
  
     請注意，出現警告訊息的訊息，指出`Date`維度包含一或多個重複的屬性關聯性，而可能讓資料無法進行彙總時為非索引鍵屬性做為資料粒度屬性。  
  
5.  刪除 [月份] 屬性與 [會計季度] 屬性之間的屬性關聯性。  
  
6.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>按日期瀏覽銷售配額量值群組中的量值  
  
1.  在 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
2.  順利完成部署之後，針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube，按一下 [Cube 設計師] 的 [瀏覽器] 索引標籤，然後按一下 [重新連接]。  
  
3.  按一下 Excel 捷徑，然後按一下 [啟用]。  
  
4.  將 [銷售量配額] 量值拖曳至 [值] 區域。  
  
5.  將 [銷售領域] 使用者階層拖曳至 [資料行標籤]，然後針對 [北美洲] 篩選。  
  
6.  將 [Date.FiscalDate] 使用者階層拖曳至 [資料列標籤] 中，然後按一下樞紐分析表上 [資料列標籤] 旁邊的向下箭號，並清除 [FY 2008] 以外的所有核取方塊，只顯示 2008 會計年度。  
  
7.  按一下 [確定]。  
  
8.  依序展開 [FY 2008]、[H1 FY 2008] 和 [Q1 FY 2008]。  
  
     下圖顯示適用於 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 的樞紐分析表，其 [銷售配額] 量值群組已正確建立維度。  
  
     請注意，會計季度層級的每一個成員都有與季層級相同的值。 使用 [Q1 FY 2008] 當作範例，[Q1 FY 2008] 的配額 $9,180,000.00 也是其每個成員的值。 之所以會發生這種行為，是因為事實資料表中的資料粒度是在季層級，而 [日期] 維度的資料粒度也是在季層級。 在第 6 課，您將了解如何按比例配置每月的季量。  
  
     ![銷售配額量值群組已正確建立維度](../../2014/tutorials/media/l5-granularity-7.gif "已正確建立維度的銷售配額量值群組")  
  
## <a name="next-lesson"></a>下一課  
 [第 6 課：定義計算](lesson-6-defining-calculations.md)  
  
## <a name="see-also"></a>另請參閱  
 [維度關聯性](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [定義一般關聯性及一般關聯性屬性](multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)   
 [在資料來源檢視設計工具中使用圖表 &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
