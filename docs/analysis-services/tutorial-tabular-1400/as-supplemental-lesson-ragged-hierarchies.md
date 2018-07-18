---
title: Analysis Services 教學課程補充課程： 不完全階層 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bc5a2164576e2e6142d8835dad6f6c114b7a9c5b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38042302"
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>補充課程-不完全階層

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在此補充課程中，您會解決常見的問題時包含空白值 （成員），在不同層級的階層進行樞紐分析。 比方說，高階主管其中擁有部門經理和非主管級直屬員工的組織。 或者，地理階層所組成的國家/地區-區域-城市，其中有些城市缺少父州或省，例如華盛頓特區、 梵蒂岡。 當階層具有空白成員時，它通常會向下延伸至不同，或不完全的層級。

![as-lesson-detail-ragged-hierarchies-table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

在 1400年相容性層級的表格式模型具有額外**隱藏成員**階層的屬性。 **預設**設定假設任何層級沒有空白的成員。 **隱藏空白成員**設定加入至樞紐分析表或報表時，從階層中排除空白成員。  
  
完成本課程的估計時間： **20 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本文補充課程是表格式模型教學課程的一部分。 執行工作之前在此補充課程中，您應已完成所有先前的課程或已完成的 Adventure Works Internet Sales 範例模型專案。 

如果您已建立 AW 網際網路銷售專案作為本教學課程的一部分，您的模型不尚未包含任何資料或不完全的階層。 若要完成此補充課程中，您有加上一些額外的資料表中建立問題、 建立關聯性、 導出資料行、 量值和新的組織階層。 該部分大約需要 15 分鐘。 然後，您可以解決此問題在幾分鐘的時間。  

## <a name="add-tables-and-objects"></a>新增資料表和物件
  
### <a name="to-add-new-tables-to-your-model"></a>將新的資料表加入至您的模型
  
1.  在表格式模型總管 中，依序展開**資料來源**，然後以滑鼠右鍵按一下您的連線 >**匯入新資料表**。
  
2.  在 導覽器中，選取  **DimEmployee**並**FactResellerSales**，然後按一下**確定**。

3.  在 [查詢編輯器] 中，按一下**匯入**

4.  建立下列[關聯性](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | 表格 1           | 「資料行」       | 篩選方向   | 表格 2     | 「資料行」      | 作用中 |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | 預設            | DimDate     | date        | 是    |
    | FactResellerSales | DueDate      | 預設            | DimDate     | date        | 否     |
    | FactResellerSales | ShipDateKey  | 預設            | DimDate     | date        | 否     |
    | FactResellerSales | ProductKey   | 預設            | DimProduct  | ProductKey  | 是    |
    | FactResellerSales | EmployeeKey  | 這兩個資料表 | DimEmployee | EmployeeKey | 是    |

5. 在  **DimEmployee**資料表中，建立下列[導出資料行](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

    **路徑** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **fullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **層級 2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],2,1)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],3,1)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],4,1)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],5,1)) 
    ```

6.  在  **DimEmployee**資料表中，建立[階層](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)名為**組織**。 新增下列資料行中的順序： **Level1**， **Level2**， **Level3**， **Level4**， **Level5**。

7.  在  **FactResellerSales**資料表中，建立下列[量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  使用[在 Excel 中的進行分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)以開啟 Excel 並自動建立樞紐分析表。

9.  在 **樞紐分析表欄位**，新增**組織**階層**DimEmployee**資料表**資料列**，和**ResellerTotalSales**量值從**FactResellerSales**資料表**值**。

    ![as-lesson-detail-ragged-hierarchies-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    當您在樞紐分析表中所見，階層會顯示不完全的資料列。 有許多資料列，其中顯示空白的成員。

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>若要修正不完全的階層，藉由設定 隱藏成員屬性

1.  在 **表格式模型總管**，展開**資料表** > **DimEmployee** > **階層** > **組織**。

2.  在 **屬性** > **隱藏成員**，選取**隱藏空白成員**。 

    ![as-lesson-detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  上一步是在 Excel 中重新整理樞紐分析表。 

    ![as-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    現在看起來好多了 ！

## <a name="see-also"></a>另請參閱   
[課程 9：建立階層](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[補充課程-動態安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[補充課程-詳細資料列](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
