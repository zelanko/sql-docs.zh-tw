---
title: Analysis Services 教學課程第 4 課： 建立關聯性 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 564126e1de4a8019778e33718b48462f633ae232
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044642"
---
# <a name="create-relationships"></a>建立關聯性

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您會驗證匯入資料時自動建立的關聯性，並加入不同資料表之間的新關聯性。 關聯性是在兩個資料表之間的一種連接，這種連接會建立這兩個資料表中資料相互關聯的方式。 例如，DimProduct 資料表和 DimProductSubcategory 資料表的關聯性是以每個產品都屬於某個子類別目錄為基礎。 若要進一步了解，請參閱[關聯性](../tabular-models/relationships-ssas-tabular.md)。
  
完成本課程的估計時間：**10 分鐘**  
  
## <a name="prerequisites"></a>필수 구성 요소  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 然後再執行工作，在這一課，您應已完成上一課：[第 3 課： 標記為日期資料表](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)。 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>檢閱現有的關聯性並加入新的關聯性  

當您匯入資料時使用 取得資料時，您會有七個資料表，從 AdventureWorksDW 資料庫。 一般而言，當您從關聯式來源匯入資料，會與資料一起自動匯入現有的關聯性。 為了讓取得資料來自動建立資料模型中的關聯性，必須有關聯性在資料來源的資料表之間。

在您繼續撰寫模型之前，您應該確認這些資料表之間的關聯性已正確建立。 此教學課程中，您也會加入三個新的關聯性。  

  
#### <a name="to-review-existing-relationships"></a>若要檢閱現有的關聯性  
  
1.  按一下**模型**功能表 >**模型檢視** > **圖表檢視**。  

    模型設計師現在會出現在圖表檢視以圖形格式顯示所有資料表匯入之間會線條。 資料表之間的線條表示匯入資料時自動建立的關聯性。
    
    ![做為 lesson4 圖表](../tutorial-tabular-1400/media/as-lesson4-diagram.png)
  
    > [!NOTE]
    > 如果您沒有看到任何資料表之間的關聯性，也可能表示在資料來源中這些資料表之間有任何關聯性。

    最大數量的資料表可能包含使用模型設計工具右下角的 [迷你地圖] 控制項。 您也可以按一下並拖曳資料表至不同位置、讓資料表彼此更靠近，或是以特定次序排列資料表。 移動資料表不會影響資料表之間的關聯性。 若要檢視特定資料表中的所有資料行，按一下並拖曳資料表邊緣，若要展開或讓較小。  
  
2.  按一下 之間的實線**DimCustomer**資料表和**DimGeography**資料表。 這兩個資料表之間的實線顯示此關聯性為作用中，也就是說，它預設會使用計算 DAX 公式時。  
  
    請注意**GeographyKey**中的資料行**DimCustomer**資料表和**GeographyKey**中的資料行**DimGeography**資料表現在都出現的方塊內。 這些資料行用於關聯性。 現在關聯性的屬性也會出現在 [屬性] 視窗中。  
  
    > [!TIP]  
    > 您也可以使用 [管理關聯性] 對話方塊顯示的資料表中的所有資料表之間的關聯性。 在表格式模型總管 中，以滑鼠右鍵按一下**關聯性** > **管理關聯性**。
  
3.  請確認下列關聯性時所建立每個資料表已從 AdventureWorksDW 資料庫匯入：  
  
    |作用中|Table|相關查閱資料表|  
    |----------|---------|------------------------|  
    |是|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |是|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |是|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |是|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |是|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    如果任何關聯性已遺失，請確認您的模型包含下列資料表： DimCustomer、 DimDate、 DimGeography、 DimProduct、 DimProductCategory、 DimProductSubcategory 和 FactInternetSales。 如果在不同時間之間的關聯性匯入來自相同的資料來源連接的資料表不會建立這些資料表，並必須手動建立。 如果不出現任何關聯性，這表示在資料來源沒有任何關聯性。 您可以建立它們以手動方式在資料模型中。

### <a name="take-a-closer-look"></a>更仔細

在圖表檢視中，請注意箭號，星號，並且顯示資料表之間的關聯性的線條上的數字。

![做為 lesson4 列](../tutorial-tabular-1400/media/as-lesson4-line.png)

箭號會顯示篩選方向。 此資料表會顯示星號*許多*中關聯性的基數，另一個側邊顯示此資料表是*一個*側邊的關聯性。 如果您要編輯關聯性;例如，變更的關聯性篩選方向或基數，按兩下以開啟 [編輯關聯性] 對話方塊的關聯線。

![做為 lesson4 編輯](../tutorial-tabular-1400/media/as-lesson4-edit.png)

這些功能是為了進階資料模型化，並會在本教學課程的範圍之外。 若要進一步了解，請參閱[雙向交叉篩選中 Analysis Services 表格式模型的](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)。

在某些情況下，您可能需要在模型中的資料表之間建立其他關聯性，以支援特定商務邏輯。 此教學課程中，您需要建立三個 FactInternetSales 資料表和 DimDate 資料表之間的其他關聯性。  
  
#### <a name="to-add-new-relationships-between-tables"></a>若要在資料表之間加入新的關聯性  
  
1.  在模型設計師中，在**FactInternetSales**資料表，按一下並按住**OrderDate**資料行，然後拖曳游標以**日期**中的資料行**DimDate**資料表，然後再放開。  

    實線顯示您已建立作用中的關聯**OrderDate**中的資料行**Internet Sales**資料表，而**日期**中的資料行**日期**資料表。 
  
      ![為-lesson4-新增](../tutorial-tabular-1400/media/as-lesson4-new.png) 
  
    > [!NOTE]  
    > 在建立關聯性時，會自動選取之間主資料表] 和 [相關的查閱資料表的基數和篩選方向。  
  
2.  在**FactInternetSales**資料表、 按住**DueDate**資料行，然後拖曳游標以**日期**中的資料行**DimDate**資料表，然後再放開。  
  
    此時會顯示您已建立的非作用中的關聯性之間出現虛線**DueDate**中的資料行**FactInternetSales**資料表，和**日期**中的資料行**DimDate**資料表。 資料表之間可以擁有多項關聯性，但是一次只能有一項使用中的關聯性。 非使用中關聯性可以設為使用中，執行自訂的 DAX 運算式中的特殊的彙總。  
  
3.  最後，建立一項關聯性。 在**FactInternetSales**資料表、 按住**ShipDate**資料行，然後拖曳游標以**日期**中的資料行**DimDate**資料表，然後再放開。  
    
     ![as-lesson4-newinactive](../tutorial-tabular-1400/media/as-lesson4-newinactive.png)
  
## <a name="whats-next"></a>下一步

[第 5 課： 建立導出資料行](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)。
  
  
  
