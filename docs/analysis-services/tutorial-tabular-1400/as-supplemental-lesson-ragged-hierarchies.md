---
title: Analysis Services 教學課程，補充課程： 不完全階層 |Microsoft 文件
description: 描述如何在 Analysis Services 教學課程中修正不完全的階層。
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 0ab9620add67094ac4115ea670c08328d7c075de
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>補充課程-不完全階層

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這個補充課程中，您會解決常見的問題時包含空白值 （成員），在不同層級的階層上進行樞紐分析。 例如，組織之高階主管同時部門主管級和非主管直屬員工。 或者，地理階層是由國家/地區-區域-城市，其中部分城市缺少父州或省，例如華盛頓特區、 梵蒂岡所組成。 當階層具有空白的成員時，它通常會向下延伸至不同的或不完全，層級。

![as-lesson-detail-ragged-hierarchies-table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

1400 相容性層級的表格式模型具有其他**隱藏成員**屬性階層。 **預設**設定假設任何層級沒有空白的成員。 **隱藏空白成員**設定從階層加入至樞紐分析表或報表時排除空白的成員。  
  
完成本課程的估計時間：**20 分鐘**  
  
## <a name="prerequisites"></a>필수 구성 요소  
本文補充課程是表格式模型教學課程的一部分。 然後再執行工作，這個補充課程中，您應已完成所有先前的課程或已完成的 Adventure Works Internet Sales 範例模型專案。 

如果您已建立 AW Internet Sales 專案做為本教學課程的一部分，您的模型不包含任何資料或不完全階層。 若要完成這個補充課程，首先必須加入一些其他的資料表來建立問題，請建立關聯性、 導出資料行、 量值和新的組織階層。 部分需要大約 15 分鐘。 然後，您可以解決在短短幾分鐘內。  

## <a name="add-tables-and-objects"></a>加入資料表和物件
  
### <a name="to-add-new-tables-to-your-model"></a>將新資料表加入至您的模型
  
1.  在表格式模型總管 中，依序展開**資料來源**，然後以滑鼠右鍵按一下您的連線 >**匯入新資料表**。
  
2.  在 導覽器中，選取  **DimEmployee**和**FactResellerSales**，然後按一下 **確定**。

3.  在 [查詢編輯器] 中，按一下**匯入**

4.  建立下列[關聯性](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | 表格 1           | 資料行       | 篩選方向   | 表格 2     | 資料行      | 作用中 |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | 預設值            | DimDate     | 日期        | 是    |
    | FactResellerSales | DueDate      | 預設值            | DimDate     | 日期        | 否     |
    | FactResellerSales | ShipDateKey  | 預設值            | DimDate     | 日期        | 否     |
    | FactResellerSales | ProductKey   | 預設值            | DimProduct  | ProductKey  | 是    |
    | FactResellerSales | EmployeeKey  | 為兩個資料表 | DimEmployee | EmployeeKey | 是    |

5. 在**DimEmployee**資料表中，建立下列[導出資料行](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

    **路徑** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **階層 1** 
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

6.  在**DimEmployee**資料表中，建立[階層](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)名為**組織**。 加入下列資料行中的順序： **Level1**， **Level2**， **Level3**， **Level4**， **Level5**。

7.  在**FactResellerSales**資料表中，建立下列[量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  使用[在 Excel 中的進行分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)開啟 Excel，並自動建立樞紐分析表。

9.  在**樞紐分析表欄位**，新增**組織**階層**DimEmployee**資料表**列**，和**ResellerTotalSales**量值從**FactResellerSales**資料表**值**。

    ![as-lesson-detail-ragged-hierarchies-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    當您在樞紐分析表中所見，階層會顯示不完全的資料列。 有許多資料列，其中會顯示空白的成員。

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>若要修正不完全的階層，藉由設定隱藏成員屬性

1.  在**表格式模型總管**，依序展開**資料表** > **DimEmployee** > **階層** > **組織**。

2.  在**屬性** > **隱藏成員**，選取**隱藏空白成員**。 

    ![as-lesson-detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  上一步是在 Excel 中重新整理樞紐分析表。 

    ![as-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    現在，看起來更好 ！

## <a name="see-also"></a>另請參閱   
[課程 9：建立階層](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[補充課程-動態安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[補充課程-詳細資料列](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
