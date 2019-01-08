---
title: Analysis Services 教學課程第 10 課：建立資料分割 |Microsoft Docs
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: f7b6e5bfd4c533028758f553e5d8c9b2ca21e6f2
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401141"
---
# <a name="create-partitions"></a>建立資料分割

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您建立資料分割來將 FactInternetSales 資料表分割成較小的邏輯部分，可以處理 （重新整理） 其他資料分割。 根據預設，您在模型中包含每個資料表會有一個分割區，其中包含所有資料表的資料行和資料列。 FactInternetSales 資料表中，我們想要將資料依年度;針對每個資料表的五年的一個資料分割。 接著，每個資料分割就可以單獨處理。 若要進一步了解，請參閱[分割區](../tabular-models/partitions-ssas-tabular.md)。 
  
完成本課程的估計時間：**15 分鐘**  
  
## <a name="prerequisites"></a>先決條件  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 執行工作之前在這一課，您應已完成上一課：[第 9 課：建立階層](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)。  
  
## <a name="create-partitions"></a>建立資料分割  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>若要建立資料分割 FactInternetSales 資料表中  
  
1.  在表格式模型總管 中，依序展開**資料表**，然後以滑鼠右鍵按一下**FactInternetSales** > **分割**。  
  
2.  在 [資料分割管理員] 中，按一下**複製**，然後將名稱變更為**FactInternetSales2010**。
  
    因為您想要在特定期間，2010 年內包含的資料列的資料分割，所以您必須修改查詢運算式。
  
4.  按一下 **設計**以開啟 查詢編輯器 中，然後按一下**FactInternetSales2010**查詢。

5.  在預覽中，按一下 向下的箭號，在**OrderDate**資料行標題，然後按一下**日期/時間篩選器** > **之間**。

    ![as-lesson10-query-editor](../tutorial-tabular-1400/media/as-lesson10-query-editor.png)

6.  在 [篩選資料列] 對話方塊中，在**顯示資料列，其中：OrderDate**，保留**之後或等於**，然後在 [日期] 欄位中，輸入**1/1/2010年**。 離開**並**運算子選取，然後選取**之前**，然後在 [日期] 欄位中，輸入**2011 年 1 月 1 日**，然後按一下 **[確定]**。

    ![為-lesson10-篩選-資料列](../tutorial-tabular-1400/media/as-lesson10-filter-rows.png)
    
    請注意在查詢編輯器 的 APPLIED STEPS 中，您會看到名為 Filtered Rows 的另一個步驟。 此篩選器是從 2010年選取只有訂單日期。

8.  按一下 **[匯入]**。

    在 [資料分割管理員] 中，請注意查詢運算式現在有額外的 Filtered Rows 子句。

    ![為 lesson10 查詢](../tutorial-tabular-1400/media/as-lesson10-query.png)
  
    此陳述式指定這個資料分割應該只包含資料，其中 OrderDate 為 2010年日曆年度 filtered 的 rows 子句中所指定的資料列。  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>建立 2011 年的資料分割  
  
1.  在 [資料分割] 清單中，按一下**FactInternetSales2010**分割您所建立，然後按一下**複製**。  將資料分割名稱變更為**FactInternetSales2011**。 

    您不需要使用查詢編輯器來建立新的 filtered 的 rows 子句。 因為您可以建立一份查詢 2010，您只需要是在查詢中進行些微變更，2011 年。
  
2.  在 **查詢運算式**，為了讓此磁碟分割包含 2011 年度的那些資料列，請將 Filtered Rows 子句中的年份**2011年**並**2012年**，分別，例如：  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a>若要建立 2012年、 2013年和 2014年的分割區。  
  
- 請遵循先前步驟中，建立 2012年、 2013年和 2014 年起，變更至包含該年度的只有資料列的 Filtered Rows 子句中的年份的資料分割。 
  

## <a name="delete-the-factinternetsales-partition"></a>刪除 FactInternetSales 分割區

現在，您會有每年的分割區，您可以刪除 FactInternetSales 分割區;處理資料分割時，請選擇所有的程序時，請避免重疊。

#### <a name="to-delete-the-factinternetsales-partition"></a>若要刪除 FactInternetSales 分割區

-  按一下  **FactInternetSales**分割，然後按一下**刪除**。



## <a name="process-partitions"></a>處理資料分割  

在 [資料分割管理員] 中，請注意**上次處理**資料行會針對每個新資料分割您建立顯示永遠不會處理這些資料分割。 當您建立資料分割時，您應該執行處理資料分割] 或 [處理資料表的作業，重新整理這些分割區中的資料。  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>處理 FactInternetSales 分割區  
  
1.  按一下 **確定**以關閉 資料分割管理員。  
  
2.  按一下  **FactInternetSales**資料表，然後按一下**模型**功能表 >**程序** > **處理資料分割**。  
  
3.  在 [處理資料分割] 對話方塊中，確認**模式**設為**處理預設**。  
  
4.  在 [處理] 資料行中選取您所建立的五個資料分割各自的核取方塊，然後按一下 [確定]。  

    ![為-lesson10-處理-資料分割](../tutorial-tabular-1400/media/as-lesson10-process-partitions.png)
  
    如果系統提示您輸入模擬認證時，輸入 Windows 使用者名稱和您在第 2 課中指定的密碼。  
  
    [資料處理] 對話方塊隨即出現，並顯示每個資料分割的處理詳細資料。 您會發現每個資料分割傳送了不同數目的資料列。 每個分割區包含 SQL 陳述式中的 WHERE 子句中指定之年份的資料列。 處理完成時，請繼續並關閉 [資料處理] 對話方塊。  
  
    ![為 lesson10-程序-完成](../tutorial-tabular-1400/media/as-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>下一步

請移至下一課：[第 11 課：建立角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)。 
