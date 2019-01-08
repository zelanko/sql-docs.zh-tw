---
title: 第 4 課：建立關聯性 | Microsoft Docs
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2cfa28b4fa5575fbdda06ed64f8f52994b596186
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52411295"
---
# <a name="lesson-4-create-relationships"></a>第 4 課：建立關聯性
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將驗證匯入資料時自動建立的關聯性，以及在不同資料表之間加入新的關聯性。 關聯性是在兩個資料表之間的一種連接，這種連接會建立這兩個資料表中資料相互關聯的方式。 例如，DimProduct 資料表和 DimProductSubcategory 資料表的關聯性是以每個產品都屬於某個子類別目錄為基礎。 若要進一步了解，請參閱[關聯性](../analysis-services/tabular-models/relationships-ssas-tabular.md)。
  
完成本課程的估計時間：**10 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 3 課：標記為日期資料表](../analysis-services/lesson-3-mark-as-date-table.md)。 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>檢閱現有的關聯性並加入新的關聯性  
當您匯入資料，使用 [資料表匯入精靈] 時，您會取得七個資料表，從 AdventureWorksDW 資料庫。 一般而言，當您匯入資料，從關聯式來源，會與資料一起自動匯入現有的關聯性。 不過，在您繼續撰寫模型之前，應先確認資料表之間的關聯性已正確建立。 在這個教學課程中，您會另外加入三個新的關聯性。  
  
#### <a name="to-review-existing-relationships"></a>若要檢閱現有的關聯性  
  
1.  按一下 **模型**功能表 >**模型檢視** > **圖表檢視**。  

    模型設計師現在會出現在 [圖表檢視] 中，這是一種圖形化格式，會顯示您匯入的所有資料表，而且資料表之間會線條。 資料表之間的線條表示匯入資料時自動建立的關聯性。
    
    ![做為表格式-lesson4-圖表](../analysis-services/media/as-tabular-lesson4-diagram.png)
  
    使用模型設計師右下方的 [迷你地圖] 控制項即可調整檢視，以便包含更多資料表。 您也可以按一下，並將資料表拖曳到不同的位置，將資料表彼此更靠近結合在一起，或依照特定順序排列。 移動資料表不會影響資料表之間已存在的關聯性。 若要檢視特定資料表中的所有資料行，按一下，並拖曳資料表邊緣，將展開或縮小。  
  
2.  按一下 之間的實線**DimCustomer**資料表並**DimGeography**資料表。 這兩個資料表之間的實線說明這個關聯性為作用中狀態，也就是說，這是在計算 DAX 公式時預設使用的關聯性。  
  
    請注意**GeographyKey**中的資料行**DimCustomer**資料表， **GeographyKey**中的資料行**DimGeography**資料表現在都每個出現在方塊內。 此節目這些是使用關聯性中的資料行。 關聯性的屬性現在也會出現在**屬性**視窗。  
  
    > [!TIP]  
    > 除了使用模型設計師圖表檢視 中，您也可以使用 管理關聯性 對話方塊中顯示的資料表中的所有資料表之間的關聯性。 以滑鼠右鍵按一下**關聯性**在表格式模型總管 中，然後按一下**管理關聯性**。 [管理關聯性] 對話方塊會顯示您匯入資料時自動建立的關聯性。  
  
3.  使用模型設計師圖表檢視 或 管理關聯性 對話方塊中的，以確認下列關聯性時所建立每個資料表匯入從 AdventureWorksDW 資料庫：  
  
    |作用中|資料表|相關查閱資料表|  
    |----------|---------|------------------------|  
    |是|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |是|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |是|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |是|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |是|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    如果遺漏任何上述表格中的關聯性，請確認您的模型包含下列資料表：DimCustomer、 DimDate、 DimGeography、 DimProduct、 DimProductCategory、 DimProductSubcategory 和 FactInternetSales。 如果在不同時間從相同的資料來源連接匯入資料表，則不會建立這些資料表之間的任何關聯性，必須手動建立。  

### <a name="take-a-closer-look"></a>深入探討
在圖表檢視中，您會發現有箭號、 星號和資料表之間的關聯性線條上的數字。

![為表格式-lesson4-行](../analysis-services/media/as-tabular-lesson4-line.png)

箭號顯示篩選方向，星號顯示此資料表是關聯性的基數的多數邊，1 顯示此資料表是關聯性的一端。 如果您要編輯關聯性;比方說，變更關聯性的篩選方向或基數，連按兩下以開啟 [編輯關聯性] 對話方塊的 [圖表] 檢視中的關聯線。

![為表格式-lesson4-編輯](../analysis-services/media/as-tabular-lesson4-edit.png)

最有可能，您永遠不需要編輯關聯性。 這些功能主要用於進階資料模型化，而且已超出本教學課程的範圍。 若要進一步了解，請參閱[雙向交叉篩選的 SQL Server 2016 Analysis Services 表格式模型](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)。

在某些情況下，您可能需要在模型中的資料表之間建立其他關聯性，以支援特定商務邏輯。 本教學課程中，您需要建立三個 FactInternetSales 資料表和 DimDate 資料表之間的其他關聯性。  
  
#### <a name="to-add-new-relationships-between-tables"></a>若要在資料表之間加入新的關聯性  
  
1.  在模型設計師中，在**FactInternetSales**資料表中，按一下，並保留**OrderDate**資料行，然後拖曳游標以**日期**中的資料行**DimDate**資料表，然後再放開。  

    一條實線會出現並顯示您已建立作用中的關聯**OrderDate**中的資料行**Internet Sales**資料表的**日期**中的資料行**日期**資料表。 
  
      ![為表格式-lesson4-新](../analysis-services/media/as-tabular-lesson4-new.png) 
  
    > [!NOTE]  
    > 在建立關聯性時，會自動選取之間主資料表] 和 [相關的查閱資料表的基數和篩選方向。  
  
2.  在**FactInternetSales**資料表中，按一下，並保留**DueDate**資料行，然後拖曳游標以**日期**中的資料行**DimDate**資料表，然後放開。  
  
    點線會出現並顯示您已建立非作用中的關聯**DueDate**中的資料行**FactInternetSales**資料表的**日期**中的資料行**DimDate**資料表。 資料表之間可以擁有多項關聯性，但是一次只能有一項使用中的關聯性。  
  
3.  最後，建立一個關聯性;在**FactInternetSales**資料表中，按一下，並保留**ShipDate**資料行，然後拖曳游標以**日期**中的資料行**DimDate**資料表，然後再放開。  
    
     ![做為表格式-lesson4-newinactive](../analysis-services/media/as-tabular-lesson4-newinactive.png)
  
## <a name="whats-next"></a>下一步
請移至下一課：[第 5 課：建立計算結果的欄](../analysis-services/lesson-5-create-calculated-columns.md)。
  
  
  
