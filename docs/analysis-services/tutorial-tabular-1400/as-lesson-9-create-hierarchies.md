---
title: Analysis Services 教學課程第 9 課：建立階層 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 92f83e1e2b3553f85301574e98f95ed7e22c1184
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469778"
---
# <a name="create-hierarchies"></a>建立階層

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您可以建立階層。 階層是以層級排列的資料行的群組。 例如，地理階層可能有國家/地區、 狀態、 縣和城市子層級。 在報表用戶端應用程式欄位清單中，階層可以與其他資料行分開顯示，讓用戶端使用者更易於導覽及包含在報表中。 若要進一步了解，請參閱[階層](../tabular-models/hierarchies-ssas-tabular.md)
  
若要建立階層，請使用 模型設計師中的*圖表檢視*。 建立及管理階層不支援在資料檢視中。  
  
估計的時間才能完成這一課：**20 分鐘的時間**  
  
## <a name="prerequisites"></a>先決條件  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 執行工作之前在這一課，您應已完成上一課：[第 8 課：建立檢視方塊](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)。  
  
## <a name="create-hierarchies"></a>建立階層  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>若要在 DimProduct 資料表中建立 Category 階層  
  
1.  在模型設計師 （[圖表檢視]） 中，以滑鼠右鍵按一下**DimProduct**資料表 >**建立階層**。 新的階層會出現在資料表視窗的底部。 重新命名該階層**分類**。  
  
2.  按一下並拖曳**ProductCategoryName**新的資料行**分類**階層。  
  
3.  在**分類**階層，以滑鼠右鍵按一下**ProductCategoryName** > **重新命名**，然後輸入**類別**。  
  
    > [!NOTE]  
    > 重新命名階層中的資料行並不會重新命名資料表中的該資料行。 階層中的資料行只是資料表中資料行的表示。  
  
4.  按一下並拖曳**ProductSubcategoryName**資料行**分類**階層。 將它重新命名**Subcategory**。 
  
5.  以滑鼠右鍵按一下**ModelName**資料行 >**新增至階層**，然後選取**分類**。 將它重新命名**模型**。

6.  最後，新增**EnglishProductName**至 Category 階層。 將它重新命名**產品**。  

    ![as-lesson9-category](../tutorial-tabular-1400/media/as-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>若要在 DimDate 資料表中建立階層  
  
1.  在  **DimDate**資料表中，建立名為階層**行事曆**。  
  
3.  新增下列資料行中的順序：

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  在  **DimDate**資料表中，建立**會計**階層。 包括下列資料行中的順序：  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  最後，在**DimDate**資料表中，建立**ProductionCalendar**階層。 包括下列資料行中的順序：  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>下一步

[第 10 課：建立分割區](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)。 
  
  
