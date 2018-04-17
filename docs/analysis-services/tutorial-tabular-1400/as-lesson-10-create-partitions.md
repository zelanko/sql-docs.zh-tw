---
title: Analysis Services 教學課程第 10 課： 建立資料分割 |Microsoft 文件
description: 描述如何在 Analysis Services 教學課程專案中建立資料分割。
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
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 9f393e0f7100236df428dcceacf55444048fddef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="create-partitions"></a>建立資料分割

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您建立資料分割來分割 FactInternetSales 資料表分成較小的邏輯部分可處理 （重新整理） 獨立於其他資料分割。 根據預設，您在模型中包含每個資料表有一個資料分割，其中包含所有資料表的資料行和資料列。 [FactInternetSales] 資料表中，我們想要將資料分割的年份，每個資料表的五年的一個資料分割。 接著，每個資料分割就可以單獨處理。 若要進一步了解，請參閱[分割](../tabular-models/partitions-ssas-tabular.md)。 
  
完成本課程的估計時間： **15 分鐘**  
  
## <a name="prerequisites"></a>필수 구성 요소  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 然後再執行工作，在這一課，您應已完成上一課：[第 9 課： 建立階層](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)。  
  
## <a name="create-partitions"></a>建立資料分割  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>若要建立 FactInternetSales 資料表的資料分割  
  
1.  在表格式模型總管 中，依序展開**資料表**，然後以滑鼠右鍵按一下**FactInternetSales** > **分割**。  
  
2.  在 [資料分割管理員] 中，按一下**複製**，然後變更名稱以**FactInternetSales2010**。
  
    因為您想要在特定期間，2010 年內包含這些資料列的資料分割，您必須修改的查詢運算式。
  
4.  按一下**設計**以開啟 查詢編輯器中，然後按一下  **FactInternetSales2010**查詢。

5.  在預覽中，按一下向下的箭號，在**OrderDate**資料行標題，然後按一下**日期/時間篩選器** > **之間**。

    ![as-lesson10-query-editor](../tutorial-tabular-1400/media/as-lesson10-query-editor.png)

6.  在 [篩選資料列] 對話方塊中**顯示資料列，其中： OrderDate**，保留**之後或等於**，然後在 [日期] 欄位中，輸入**1/1/2010年**。 保留**和**運算子選取，然後選取**之前**，然後在 日期 欄位中，輸入**2011 年 1 月 1 日**，然後按一下 **確定**。

    ![為-lesson10-篩選的資料列](../tutorial-tabular-1400/media/as-lesson10-filter-rows.png)
    
    請注意在查詢編輯器] 中套用的步驟，您會看到另一個名為 [已篩選資料列的步驟。 此篩選器是從 2010年選取訂單日期。

8.  **가져오기**를 클릭합니다.

    在 [資料分割管理員] 中，請注意，查詢運算式中有其他篩選的資料列子句。

    ![做為 lesson10 查詢](../tutorial-tabular-1400/media/as-lesson10-query.png)
  
    這個陳述式會指定此分割區應該只包含資料，其中 OrderDate 處於 2010年日曆年度的資料列篩選的子句中所指定資料列中。  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>建立 2011 年的資料分割  
  
1.  在資料分割清單中，按一下  **FactInternetSales2010**您所建立，資料分割，然後按一下 **複製**。  將資料分割名稱變更為**FactInternetSales2011**。 

    您不需要使用查詢編輯器來建立新的資料列篩選的子句。 2010 中建立查詢的複本，因為您只需要為 2011 在查詢中有些微變更。
  
2.  在**查詢運算式**，為了讓這個資料分割的資料列包含 2011 年、 取代具有篩選資料列子句中的年**2011年**和**2012年**分別類似：  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a>若要建立資料分割 2013、 2012年和 2014年。  
  
- 遵循先前的步驟，建立資料分割的 2013、 2012年和 2014，變更要包含該年份只有資料列篩選 Rows 子句中的年。 
  

## <a name="delete-the-factinternetsales-partition"></a>刪除 FactInternetSales 磁碟分割

現在，您會有每年的資料分割，您可以刪除 FactInternetSales 資料分割;處理資料分割時，選擇所有的程序時，請避免重疊。

#### <a name="to-delete-the-factinternetsales-partition"></a>若要刪除 FactInternetSales 分割

-  按一下**FactInternetSales**分割，，然後按一下 **刪除**。



## <a name="process-partitions"></a>處理資料分割  

在 [資料分割管理員] 中，請注意**最後一個處理**資料行的每個新的資料分割所建立顯示絕對不會處理這些資料分割。 當您建立資料分割時，您應該執行的處理資料分割或處理程序資料表作業以重新整理這些資料分割中的資料。  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>若要處理 FactInternetSales 的資料分割  
  
1.  按一下**確定**以關閉 資料分割管理員。  
  
2.  按一下**FactInternetSales**資料表，然後按一下 **模型**功能表 >**程序** > **處理資料分割**。  
  
3.  在 [處理資料分割] 對話方塊中，確認**模式**設**處理預設**。  
  
4.  在 [處理] 資料行中選取您所建立的五個資料分割各自的核取方塊，然後按一下 [確定]。  

    ![為-lesson10-處理的資料分割](../tutorial-tabular-1400/media/as-lesson10-process-partitions.png)
  
    如果系統提示您輸入模擬認證，請輸入 Windows 使用者名稱和您在第 2 課中指定的密碼。  
  
    [資料處理] 對話方塊隨即出現，並顯示每個資料分割的處理詳細資料。 您會發現每個資料分割傳送了不同數目的資料列。 每個資料分割包含 SQL 陳述式中的 WHERE 子句中指定之年份的資料列。 處理完成時，請繼續並關閉 [資料處理] 對話方塊。  
  
    ![做為 lesson10-處理序-完成](../tutorial-tabular-1400/media/as-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>下一步

移至下一課：[第 11 課： 建立角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)。 
