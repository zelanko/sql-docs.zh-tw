---
title: 第 10 課：建立資料分割 |Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dce53a4b4ae5a64a898eec2b30921fe7a7f2e242
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404250"
---
# <a name="lesson-10-create-partitions"></a>第 10 課：建立資料分割
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將建立資料分割來將 FactInternetSales 資料表分割成較小的邏輯部分，可以處理 （重新整理） 其他資料分割。 根據預設，您加入模型中每個資料表會有一個分割區會包含所有資料表的資料行和資料列。 FactInternetSales 資料表中，我們想要將資料依年度;針對每個資料表的五年的一個資料分割。 接著，每個資料分割就可以單獨處理。 若要進一步了解，請參閱[分割區](../tabular-models/partitions-ssas-tabular.md)。  
  
估計的時間才能完成這一課：**15 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 9 課：建立階層](lesson-9-create-hierarchies.md)。  
  
## <a name="create-partitions"></a>建立資料分割  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>若要建立資料分割 FactInternetSales 資料表中  
  
1.  在表格式模型總管 中，依序展開**資料表**，以滑鼠右鍵按一下**FactInternetSales** > **分割**。  
  
2.  在 [資料分割管理員] 對話方塊中，按一下**複製**。  
  
3.  在 **分割區名稱**，將名稱變更為**FactInternetSales2010**。  
  
    > [!TIP]  
    > 請注意，在 [資料表預覽] 視窗中的資料行名稱會顯示模型資料表 （核取） 從來源資料行名稱中包含的資料行。 這是因為 [資料表預覽] 視窗是從來源資料表顯示資料行，而不是從模型資料表。  
  
4.  選取  **SQL**以開啟 SQL 陳述式編輯器的 預覽 視窗右側的正上方的按鈕。  
  
    由於您希望資料分割只包含特定期間內的資料列，因此必須包含 WHERE 子句。 您只能使用 SQL 陳述式建立 WHERE 子句。  
  
5.  在  **SQL 陳述式**欄位中，取代現有的陳述式複製並貼上下列陳述式：  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2010-01-01 00:00:00') AND ([OrderDate] < N'2011-01-01 00:00:00'))  
    ```  
  
    這個陳述式會指定資料分割應包含 OrderDate 為 2010 日曆年度之資料列中的所有資料，如 WHERE 子句中所指定。  
  
6.  按一下 **[驗證]**。  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>建立 2011 年的資料分割  
  
1.  在 [資料分割] 清單中，按一下**FactInternetSales2010**您剛剛建立，資料分割，然後按一下**複製**。  
  
2.  在 **分割區名稱**，型別**FactInternetSales2011**。  
  
3.  在 SQL 陳述式中，將 WHERE 子句取代為下列子句，以便讓資料分割只包含 2011 年度的資料列：  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2012-year"></a>建立 2012 年的資料分割  
  
- 請遵循上述步驟，使用下列的 WHERE 子句。 
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2013-year"></a>建立 2013 年的資料分割  
  
- 請遵循上述步驟，使用下列的 WHERE 子句。 
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2014-year"></a>若要建立 2014 年的資料分割  
  
- 請遵循上述步驟，使用下列的 WHERE 子句。 
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  

## <a name="delete-the-factinternetsales-partition"></a>刪除 FactInternetSales 分割區
現在，您會有每年的分割區，您可以刪除 FactInternetSales 分割區。 處理資料分割時，請選擇所有的程序時，這可避免重疊。
#### <a name="to-delete-the-factinternetsales-partition"></a>若要刪除 FactInternetSales 分割區
-  按一下 FactInternetSales 分割區，然後按一下**刪除**。



## <a name="process-partitions"></a>處理資料分割  
在 [資料分割管理員] 中，請注意**上次處理**每個新的資料行分割您剛建立的示範，永遠不會處理這些資料分割。 當您建立新的資料分割時，應執行 [處理資料分割] 或 [處理資料表] 作業，重新整理這些資料分割中的資料。  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>處理 FactInternetSales 分割區  
  
1.  按一下 **確定**以關閉 資料分割管理員 對話方塊。  
  
2.  按一下  **FactInternetSales**資料表，然後按一下**模型**功能表 >**程序** > **處理資料分割**。  
  
3.  在 [處理資料分割] 對話方塊中，確認**模式**設為**處理預設**。  
  
4.  在 [處理] 資料行中選取您所建立的五個資料分割各自的核取方塊，然後按一下 [確定]。  

    ![as-tabular-lesson10-process-partitions](media/as-tabular-lesson10-process-partitions.png)
  
    如果系統提示您輸入模擬認證時，輸入 Windows 使用者名稱和您在第 2 課中指定的密碼。  
  
    [資料處理] 對話方塊隨即出現，並顯示每個資料分割的處理詳細資料。 您會發現每個資料分割傳送了不同數目的資料列。 這是因為每個資料分割只包含 SQL 陳述式中的 WHERE 子句所指定年度的資料列。 處理完成時，請繼續並關閉 [資料處理] 對話方塊。  
  
    ![as-tabular-lesson10-process-complete](media/as-tabular-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>下一步
請移至下一課：[第 11 課：建立角色](lesson-11-create-roles.md)。 
