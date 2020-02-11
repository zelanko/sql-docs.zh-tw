---
title: 第11課：建立資料分割 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06ffe60802e52bd0ae141435628fc3812dc2c7c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079194"
---
# <a name="lesson-11-create-partitions"></a>第 11 課：建立資料分割
  在這一課，您將建立資料分割，以便將 [網際網路銷售] 資料表分成更小的邏輯部分，讓其他資料分割能夠單獨處理 (重新整理)。 根據預設，您在模型中包含的每個資料表都有一個資料分割，其中包含資料表的所有資料行和資料列。 針對 [網際網路銷售] 資料表，我們想要依年份分割資料;每一個資料表的五年都會有一個資料分割。  然後就可以獨立處理每個分割區。 如需詳細資訊，請參閱[資料分割 &#40;SSAS 表格式&#41;](tabular-models/partitions-ssas-tabular.md)。  
  
 這堂課的預估完成時間：**15 分鐘**  
  
## <a name="prerequisites"></a>Prerequisites  
 本主題是表格式模型教學課程的一部分，請依序完成。 在執行本課中的工作之前，您應已完成上一課：[第 10 課：建立階層](lesson-9-create-hierarchies.md)。  
  
## <a name="create-partitions"></a>建立資料分割  
  
#### <a name="to-create-partitions-in-the-internet-sales-table"></a>在 [網際網路銷售額] 資料表中建立資料分割  
  
1.  在模型設計師中，依序按一下 [網際網路銷售]**** 資料表、[資料表]**** 功能表和 [資料分割]****。  
  
     [資料分割管理員]**** 對話方塊隨即開啟。  
  
2.  在 [資料**分割管理員**] 對話方塊的 [資料分割 **] 中，** 按一下 [**網際網路銷售**] 資料分割。  
  
3.  在 [資料**分割名稱**] 中， `Internet Sales 2005`將名稱變更為。  
  
    > [!TIP]  
    >  在繼續進行下一步之前，您會發現 [資料表預覽] 視窗中的資料行名稱是以來源的資料行名稱顯示模型資料表中包含的資料行 (已核取)。 這是因為 [資料表預覽] 視窗是從來源資料表顯示資料行，而不是從模型資料表。  
  
4.  選取位於預覽視窗右側上方的 [查詢編輯器]**** 按鈕。  
  
     由於您希望資料分割只包含特定期間內的資料列，因此必須包含 WHERE 子句。 您只能使用 SQL 陳述式建立 WHERE 子句。  
  
5.  在 [SQL 陳述式]**** 欄位中貼入下列陳述式，以取代現有的陳述式：  
  
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
    WHERE (([OrderDate] >= N'2005-01-01 00:00:00') AND ([OrderDate] < N'2006-01-01 00:00:00'))  
    ```  
  
     這個陳述式會指定資料分割應包含 OrderDate 為 2005 日曆年度之資料列中的所有資料，如 WHERE 子句中所指定。  
  
6.  按一下 [驗證]****。  
  
     請注意，此時會顯示一個警告，指出特定資料行不存在來源中。 這是因為在[第3課：重新命名資料行](rename-columns.md)中，您將模型中的 [網際網路銷售] 資料表中的資料行重新命名，與來源上的相同資料行不同。  
  
#### <a name="to-create-a-partition-for-the-2006-year-in-the-internet-sales-table"></a>若要在網際網路銷售資料表中建立2006年的資料分割  
  
1.  在 [資料**分割管理員**] 對話方塊的 [資料分割 **] 中，** 按一下您剛才建立的`Internet Sales 2005`資料分割，然後**複製**。  
  
2.  在 [資料**分割名稱**] 中，輸入`Internet Sales 2006`。  
  
3.  在 SQL 語句中，若要讓資料分割只包含2006年的資料列，請將 WHERE 子句取代為下列內容：  
  
    ```  
    WHERE (([OrderDate] >= N'2006-01-01 00:00:00') AND ([OrderDate] < N'2007-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2007-year-in-the-internet-sales-table"></a>若要在網際網路銷售資料表中建立2007年的資料分割  
  
1.  在 [資料分割管理員]**** 對話方塊中，按一下 [複製]****。  
  
2.  在 [資料**分割名稱**] 中，輸入`Internet Sales 2007`。  
  
3.  在 [**切換至**] 中，選取 [**查詢編輯器**]。  
  
4.  在 SQL 語句中，若要讓資料分割只包含2007年的資料列，請將 WHERE 子句取代為下列內容：  
  
    ```  
    WHERE (([OrderDate] >= N'2007-01-01 00:00:00') AND ([OrderDate] < N'2008-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2008-year-in-the-internet-sales-table"></a>若要在網際網路銷售資料表中建立2008年的資料分割  
  
1.  在 [資料分割管理員]**** 對話方塊中，按一下 [新增]****。  
  
2.  在 [資料**分割名稱**] 中，輸入`Internet Sales 2008`。  
  
3.  在 [**切換至**] 中，選取 [**查詢編輯器**]。  
  
4.  在 SQL 語句中，若要讓資料分割只包含2008年的資料列，請將 WHERE 子句取代為下列內容：  
  
    ```  
    WHERE (([OrderDate] >= N'2008-01-01 00:00:00') AND ([OrderDate] < N'2009-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2009-year-in-the-internet-sales-table"></a>若要在網際網路銷售資料表中建立 2009 年度的資料分割  
  
1.  在 [資料分割管理員]**** 對話方塊中，按一下 [新增]****。  
  
2.  在 [資料**分割名稱**] 中，輸入`Internet Sales 2009`。  
  
3.  在 [**切換至**] 中，選取 [**查詢編輯器**]。  
  
4.  在 SQL 陳述式中，將 WHERE 子句取代為下列子句，以便讓資料分割只包含 2009 年度的資料列：  
  
    ```  
    WHERE (([OrderDate] >= N'2009-01-01 00:00:00') AND ([OrderDate] < N'2010-01-01 00:00:00'))  
    ```  
  
## <a name="process-partitions"></a>處理資料分割  
 在 [資料分割管理員]**** 對話方塊中，您會發現剛才建立的每個新資料分割名稱旁邊都有星號 (**\***)。 這表示資料分割尚未處理 (重新整理)。 當您建立新的資料分割時，應執行 [處理資料分割] 或 [處理資料表] 作業，重新整理這些資料分割中的資料。  
  
#### <a name="to-process-internet-sales-partitions"></a>處理網際網路銷售資料分割  
  
1.  按一下 [確定]**** 關閉 [資料分割管理員]**** 對話方塊。  
  
2.  在模型設計師中，依序按一下 [網際網路銷售]**** 資料表和 [模型]**** 功能表，然後指向 [處理]**** (重新整理)，再按一下 [處理資料分割]****。  
  
3.  在 [處理資料分割]**** 對話方塊中，確認 [模式]**** 設定為 [處理預設]****。  
  
4.  對於您建立的五個分割區，將 [處理]**** 資料行的核取方塊全部選取，然後按一下 [確定]****。  
  
     如果系統提示您輸入模擬認證，請輸入您在第 2 課的步驟 6 中指定的 Windows 使用者名稱和密碼。  
  
     [**資料處理**] 對話方塊隨即出現，並顯示每個分割區的處理詳細資料。 請注意，傳送給每個分割區的資料列數目都不同。 這是因為每個分割區只會包含 SQL 陳述式的 WHERE 子句已指定之年份的資料列。 2010 年則沒有資料。  
  
## <a name="next-steps"></a>後續步驟  
 若要繼續進行本教學課程，請前往下一課：[第 12 課：建立角色](lesson-11-create-roles.md)。  
  
  
