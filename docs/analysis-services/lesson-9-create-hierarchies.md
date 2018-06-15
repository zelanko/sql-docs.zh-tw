---
title: 第 10 課： 建立階層 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d4c1fc4905c52351b61a4e79b2ff21f47501f337
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34016325"
---
# <a name="lesson-9-create-hierarchies"></a>第 9 課： 建立階層
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將建立階層。 階層是以層級排列的資料行群組；例如，[地理位置] 階層可能有 [國家/地區]、[州省]、[縣市]、[縣 (市)] 的子層級。 在報表用戶端應用程式欄位清單中，階層可以與其他資料行分開顯示，讓用戶端使用者更易於導覽及包含在報表中。 若要進一步了解，請參閱[階層](../analysis-services/tabular-models/hierarchies-ssas-tabular.md)。  
  
若要建立階層，您將使用模型設計師中的*圖表檢視*。 資料檢視中不支援建立及管理階層。  
  
完成本課程的估計時間：**20 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 然後再執行工作，在這一課，您應已完成上一課：[第 8 課： 建立檢視方塊](../analysis-services/lesson-8-create-perspectives.md)。  
  
## <a name="create-hierarchies"></a>建立階層  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>在 DimProduct 資料表中建立類別目錄階層  
  
1.  在模型設計師 （圖表檢視） 中，以滑鼠右鍵按一下**DimProduct**資料表 >**建立階層**。 新的階層會出現在資料表視窗的底部。 重新命名該階層**類別**。  
  
2.  按一下並拖曳**ProductCategoryName**至新的資料行**類別**階層。  
  
3.  在**類別**階層，以滑鼠右鍵按一下**ProductCategoryName** > **重新命名**，然後輸入**類別**。  
  
    > [!NOTE]  
    > 重新命名階層中的資料行並不會重新命名資料表中的該資料行。 階層中的資料行只是資料表中資料行的表示。  
  
4.  按一下並拖曳**ProductSubcategoryName**欄**類別**階層。 將它重新命名**Subcategory**。 
  
5.  以滑鼠右鍵按一下**ModelName**資料行 >**將加入階層**，然後選取**類別**。 執行相同 **[englishproductname]**。 重新命名階層中的這些資料行**模型**和**產品**。  

    ![做為表格式-lesson9-類別](../analysis-services/media/as-tabular-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>若要建立 DimDate 資料表中的階層  
  
1.  在**DimDate**資料表中，建立名為新階層**行事曆**。  
  
3.  加入下列資料行中的順序：

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  在**DimDate**資料表中，建立**會計**階層。 包含下列資料行：  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  最後，在**DimDate**資料表中，建立**ProductionCalendar**階層。 包含下列資料行：  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>下一步
移至下一課：[第 10 課： 建立資料分割](../analysis-services/lesson-10-create-partitions.md)。 
  
  
