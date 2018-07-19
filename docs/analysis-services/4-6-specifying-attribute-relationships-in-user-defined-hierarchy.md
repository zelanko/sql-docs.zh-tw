---
title: 4-6-指定使用者定義階層中的屬性關聯性 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 712172f7c74e1c7efa7766ce4c25a9a8fca173f0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34018795"
---
# <a name="4-6-specifying-attribute-relationships-in-user-defined-hierarchy"></a>4-6-指定使用者定義階層中的屬性關聯性
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

如同您在這個教學課程中已學到的，您可以將屬性階層組織成使用者階層內的層級，在 Cube 中為使用者提供導覽路徑。 使用者階層可代表自然階層，例如縣 (市)、省份和國家 (地區)，或只代表導覽路徑，例如員工姓名、職稱和部門名稱。 對於導覽階層的使用者而言，這兩種類型的使用者階層是一樣的。  
  
透過自然階層，當您在構成層級的屬性之間定義屬性關聯性時， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 可使用一個屬性的彙總來取得相關屬性的結果。 如果屬性之間沒有定義關聯性， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 將從索引鍵屬性中彙總所有非索引鍵屬性。 因此，如果基礎資料支援屬性關聯性，您就應該定義屬性之間的屬性關聯性。 定義屬性關聯性可改善維度、資料分割和查詢處理效能。 如需詳細資訊，請參閱[定義屬性關聯性](../analysis-services/multidimensional-models/attribute-relationships-define.md)和[屬性關聯性](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
當您定義屬性關聯性時，可以指定彈性或固定的關聯性。 如果您定義固定關聯性，當維度更新時， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會保留彙總。 如果定義為固定的關聯性實際上有所變更，除非已完全處理維度，否則在處理期間， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會產生錯誤。 指定適當的關聯性和關聯性屬性可增加查詢和處理效能。 如需詳細資訊，請參閱 [定義屬性關聯性](../analysis-services/multidimensional-models/attribute-relationships-define.md)和 [使用者階層屬性](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)。  
  
在這個主題的工作中，您會在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案中，為自然使用者階層中的屬性定義屬性關聯性。 這些包括 [客戶] 維度中的 [客戶地理位置] 階層、[銷售領域] 維度中的 [銷售領域] 階層、[產品] 維度中的 [產品型號線] 階層，以及 [日期] 維度中的 [會計日期] 和 [日曆日期] 階層。 這些使用者階層全都是自然階層。  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-customer-geography-hierarchy"></a>在 [客戶地理位置] 階層中定義屬性的屬性關聯性  
  
1.  針對 [客戶] 維度切換到 [維度設計師]，然後按一下 [維度結構] 索引標籤。  
  
    在 [階層] 窗格中，請注意 [客戶地理位置] 使用者定義階層中的層級。 這個階層目前只是使用者的向下鑽研路徑，因為您尚未定義任何層級或屬性之間的關聯性。  
  
2.  按一下 **[屬性關聯性]** 索引標籤。  
  
    請注意，有四種屬性關聯性會將 [地理位置] 資料表的非索引鍵屬性連結到 [地理位置] 資料表的索引鍵屬性。 [地理位置] 屬性與 [全名] 屬性相關。 [郵遞區號] 屬性會透過 [地理位置] 屬性間接連結到 [全名] 屬性，因為 [郵遞區號] 會連結到 [地理位置] 屬性，而 [地理位置] 屬性則連結到 [全名] 屬性。 接著，我們將變更屬性關聯性，如此它們就不會使用 [地理位置] 屬性。  
  
3.  在圖表中，以滑鼠右鍵按一下 [全名] 屬性，然後選取 [新增屬性關聯性]。  
  
4.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [全名]。 將 [相關屬性] 設定為 [郵遞區號]。 然後，在 [關聯性類型] 清單中，保持關聯性類型設定為 [彈性] 的狀態，因為成員之間的關聯性可能會隨著時間而變更。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    此時，圖表中會顯示一個警告圖示，因為關聯性是重複的。 [全名] -> [地理位置]-> [郵遞區號] 關聯性已經存在，而且您只有建立 [全名] -> [郵遞區號] 關聯性。 由於 [地理位置]-> [郵遞區號] 關聯性現在已重複，所以我們將移除它。  
  
6.  在 [屬性關聯性] 窗格中，以滑鼠右鍵按一下 [地理位置]-> [郵遞區號]，然後按一下 [刪除]。  
  
7.  當 [刪除物件] 對話方塊顯示時，按一下 [確定]。  
  
8.  在圖表中，以滑鼠右鍵按一下 [郵遞區號] 屬性，然後選取 [新增屬性關聯性]。  
  
9. 在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [郵遞區號]。 將 [相關屬性] 設定為 [縣 (市)]。 在 [關聯性類型] 清單中，保持關聯性類型設定為 [彈性]。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    由於 [地理位置]-> [縣 (市)] 關聯性現在已重複，所以我們將刪除它。  
  
11. 在 [屬性關聯性] 窗格中，以滑鼠右鍵按一下 [地理位置]-> [縣 (市)]，然後按一下 [刪除]。  
  
12. 當 [刪除物件] 對話方塊顯示時，按一下 [確定]。  
  
13. 在圖表中，以滑鼠右鍵按一下 [縣 (市)] 屬性，然後選取 [新增屬性關聯性]。  
  
14. 在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [縣 (市)]。 將 [相關屬性] 設定為 [省份]。 然後，在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]，因為縣 (市) 和省份之間的關聯性不會隨著時間而變更。  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. 以滑鼠右鍵按一下介於 [地理位置] 與 [省份] 之間的箭頭，然後按一下 [刪除]。  
  
17. 當 [刪除物件] 對話方塊顯示時，按一下 [確定]。  
  
18. 在圖表中，以滑鼠右鍵按一下 [省份] 屬性，然後選取 [新增屬性關聯性]。  
  
19. 在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [省份]。 將 [相關屬性] 設定為 [國家地區]。 然後，在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]，因為省份和國家地區之間的關聯性不會隨著時間而變更。  
  
20. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
21. 在 [屬性關聯性] 窗格中，以滑鼠右鍵按一下 [地理位置]-> [國家地區]，然後按一下 [刪除]。  
  
22. 當 [刪除物件] 對話方塊顯示時，按一下 [確定]。  
  
23. 按一下 [維度結構] 索引標籤。  
  
    請注意，當您刪除 [地理位置] 與其他屬性間的最後一個屬性關聯性時，就會刪除該 [地理位置] 本身。 這是因為不再使用該屬性。  
  
24. 按一下 [檔案] 功能表上的 [全部儲存]。  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-sales-territory-hierarchy"></a>在 [銷售領域] 階層中定義屬性的屬性關聯性  
  
1.  請針對 [銷售領域] 維度開啟 [維度設計師]，然後按一下 [屬性關聯性] 索引標籤。  
  
2.  在圖表中，以滑鼠右鍵按一下 [銷售領域國家 (地區)] 屬性，然後選取 [新增屬性關聯性]。  
  
3.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [銷售領域國家 (地區)]。 將 [相關屬性] 設定為 [銷售領域國家 (地區)]。 在 [關聯性類型] 清單中，保持關聯性類型設定為 [彈性]。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    [銷售領域群組] 現在連結到 [銷售領域國家 (地區)]，而 [銷售領域國家 (地區)] 現在則連結到 [銷售領域地區]。 其中每個關聯性的 [RelationshipType] 屬性會設為 [彈性]，因為國家 (地區) 內的地區群組可能會隨著時間而變更，而且將國家 (地區) 分成群組的分組設定也可能會隨著時間而變更。  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-product-model-lines-hierarchy"></a>在 [產品型號線] 階層中定義屬性的屬性關聯性  
  
1.  請針對 [產品] 維度開啟 [維度設計師]，然後按一下 [屬性關聯性] 索引標籤。  
  
2.  在圖表中，以滑鼠右鍵按一下 [模型名稱] 屬性，然後選取 [新增屬性關聯性]。  
  
3.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [模型名稱]。 將 [相關屬性] 設定為 [產品線]。 在 [關聯性類型] 清單中，保持關聯性類型設定為 [彈性]。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-fiscal-date-hierarchy"></a>在會計日期階層中定義屬性的屬性關聯性  
  
1.  請針對 [日期] 維度切換至 [維度設計師]，然後按一下 [屬性關聯性] 索引標籤。  
  
2.  在圖表中，以滑鼠右鍵按一下 [月份] 屬性，然後選取 [新增屬性關聯性]。  
  
3.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [月份]。 將 [相關屬性] 設定為 [會計季度]。 在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  在圖表中，以滑鼠右鍵按一下 [會計季度] 屬性，然後選取 [新增屬性關聯性]。  
  
6.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [會計季度]。 將 [相關屬性] 設定為 [會計半年度]。 在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  在圖表中，以滑鼠右鍵按一下 [會計半年度] 屬性，然後選取 [新增屬性關聯性]。  
  
9. 在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [會計半年度]。 將 [相關屬性] 設定為 [會計年度]。 在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-calendar-date-hierarchy"></a>在日曆日期階層中定義屬性的屬性關聯性  
  
1.  在圖表中，以滑鼠右鍵按一下 [月份] 屬性，然後選取 [新增屬性關聯性]。  
  
2.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [月份]。 將 [相關屬性] 設定為 [日曆季]。 在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  在圖表中，以滑鼠右鍵按一下 [日曆季] 屬性，然後選取 [新增屬性關聯性]。  
  
5.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [日曆季]。 將 [相關屬性] 設定為 [日曆半年度]。 在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  在圖表中，以滑鼠右鍵按一下 [日曆半年度] 屬性，然後選取 [新增屬性關聯性]。  
  
8.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [日曆半年度]。 將 [相關屬性] 設定為 [日曆年度]。 在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-geography-hierarchy"></a>在 [地理位置] 階層中定義屬性的屬性關聯性  
  
1.  請針對 [地理位置] 維度開啟 [維度設計師]，然後按一下 [屬性關聯性] 索引標籤。  
  
2.  在圖表中，以滑鼠右鍵按一下 [郵遞區號] 屬性，然後選取 [新增屬性關聯性]。  
  
3.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [郵遞區號]。 將 [相關屬性] 設定為 [縣 (市)]。 在 [關聯性類型] 清單中，將關聯性類型設定為 [彈性]。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  在圖表中，以滑鼠右鍵按一下 [縣 (市)] 屬性，然後選取 [新增屬性關聯性]。  
  
6.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [縣 (市)]。 將 [相關屬性] 設定為 [省份]。 在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  在圖表中，以滑鼠右鍵按一下 [省份] 屬性，然後選取 [新增屬性關聯性]。  
  
9. 在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [省份]。 將 [相關屬性] 設定為 [國家地區]。 在 [關聯性類型] 清單中，將關聯性類型設定為 [固定]。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 在圖表中，以滑鼠右鍵按一下 [地理位置索引鍵] 屬性，然後選取 [屬性]。  
  
12. 將 [AttributeHierarchyOptimizedState] 屬性設定為 [NotOptimized]、將 [AttributeHierarchyOrdered] 屬性設定為 [False]，並且將 [AttributeHierarchyVisible] 屬性設定為 [False]。  
  
13. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
14. 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[定義未知的成員和 Null 處理屬性](../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
## <a name="see-also"></a>另請參閱  
[定義屬性關聯性](../analysis-services/multidimensional-models/attribute-relationships-define.md)  
[使用者階層屬性](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
  
