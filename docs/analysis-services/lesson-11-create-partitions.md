---
title: "第 11 課：建立資料分割 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 第 11 課：建立資料分割
在這一課，您將建立資料分割，以便將 [網際網路銷售] 資料表分成更小的邏輯部分，讓其他資料分割能夠單獨處理 (重新整理)。 根據預設，加入模型中的每個資料表都有一個資料分割，其中包括資料表的所有資料行和資料列。 我們要依年度分割 [網際網路銷售] 資料表的資料，一個資料分割代表每個資料表的五年。  接著，每個資料分割就可以單獨處理。 如需詳細資訊，請參閱[資料分割 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
完成本課程的估計時間：**15 分鐘**  
  
## 必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 在執行本課中的工作之前，您應已完成上一課：[第 10 課：建立階層](../analysis-services/lesson-10-create-hierarchies.md)。  
  
## 建立資料分割  
  
#### 在 [網際網路銷售額] 資料表中建立資料分割  
  
1.  在模型設計師中，依序按一下 [網際網路銷售] 資料表、[資料表] 功能表和 [資料分割]。  
  
    [資料分割管理員] 對話方塊隨即開啟。  
  
2.  在 [資料分割管理員] 對話方塊的資料分割清單中，按一下 [網際網路銷售] 資料分割。  
  
3.  在 [資料分割名稱] 中，將名稱變更為 [網際網路銷售 2010]。  
  
    > [!TIP]  
    > 在繼續進行下一步之前，您會發現 [資料表預覽] 視窗中的資料行名稱是以來源的資料行名稱顯示模型資料表中包含的資料行 (已核取)。 這是因為 [資料表預覽] 視窗是從來源資料表顯示資料行，而不是從模型資料表。  
  
4.  選取位於預覽視窗右側上方的 [查詢編輯器] 按鈕。  
  
    由於您希望資料分割只包含特定期間內的資料列，因此必須包含 WHERE 子句。 您只能使用 SQL 陳述式建立 WHERE 子句。  
  
5.  在 [SQL 陳述式] 欄位中貼入下列陳述式，以取代現有的陳述式：  
  
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
  
  
#### 建立 2011 年的資料分割  
  
1.  在資料分割清單中，按一下您剛才建立的 [網際網路銷售 2010] 資料分割，然後按一下 [複製]。  
  
2.  在 [資料分割名稱] 中輸入 [網際網路銷售 2011]。  
  
3.  在 SQL 陳述式中，將 WHERE 子句取代為下列子句，以便讓資料分割只包含 2011 年度的資料列：  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### 建立 2012 年的資料分割  
  
1.  在 [資料分割管理員] 對話方塊中，按一下 [複製]。  
  
2.  在 [資料分割名稱] 中輸入 [網際網路銷售 2012]。  
  
3.  在 SQL 陳述式中，將 WHERE 子句取代為下列子句，以便讓資料分割只包含 2012 年度的資料列：  
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### 建立 2013 年的資料分割  
  
1.  在 [資料分割管理員] 對話方塊中，按一下 [新增]。  
  
2.  在 [資料分割名稱] 中輸入 [網際網路銷售 2013]。  
  
3.  在 SQL 陳述式中，將 WHERE 子句取代為下列子句，以便讓資料分割只包含 2013 年度的資料列：  
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### 在網際網路銷售資料表中建立 2014 年的資料分割  
  
1.  在 [資料分割管理員] 對話方塊中，按一下 [新增]。  
  
2.  在 [資料分割名稱] 中輸入 [網際網路銷售 2014]。  
  
3.  在 SQL 陳述式中，將 WHERE 子句取代為下列子句，以便讓資料分割只包含 2014 年度的資料列：  
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  
  
## 處理資料分割  
在 [資料分割管理員] 對話方塊中，您會發現剛才建立的每個新資料分割名稱旁邊都有星號 (**\***)。 這表示資料分割尚未處理 (重新整理)。 當您建立新的資料分割時，應執行 [處理資料分割] 或 [處理資料表] 作業，重新整理這些資料分割中的資料。  
  
#### 處理網際網路銷售資料分割  
  
1.  按一下 [確定] 關閉 [資料分割管理員] 對話方塊。  
  
2.  在模型設計師中，依序按一下 [網際網路銷售] 資料表和 [模型] 功能表，然後指向 [處理] (重新整理)，再按一下 [處理資料分割]。  
  
3.  在 [處理資料分割] 對話方塊中，確認 [模式] 設定為 [處理預設]。  
  
4.  在 [處理] 資料行中選取您所建立的五個資料分割各自的核取方塊，然後按一下 [確定]。  
  
    如果系統提示您輸入模擬認證，請輸入您在第 2 課的步驟 6 中指定的 Windows 使用者名稱和密碼。  
  
    [資料處理] 對話方塊隨即出現，並顯示每個資料分割的處理詳細資料。 您會發現每個資料分割傳送了不同數目的資料列。 這是因為每個資料分割只包含 SQL 陳述式中的 WHERE 子句所指定年度的資料列。 處理完成時，請繼續並關閉 [資料處理] 對話方塊。  
  
  
  
## 後續步驟  
若要繼續進行本教學課程，請前往下一課：[第 12 課：建立角色](../analysis-services/lesson-12-create-roles.md)。  
  
  
  
