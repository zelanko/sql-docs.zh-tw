---
title: "第 2 課︰檢視和瀏覽資料 (資料科學端對端逐步解說) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: d3835d6d-e68b-486d-81a0-81b717cc6134
caps.latest.revision: 32
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 26
---
# 第 2 課︰檢視和瀏覽資料 (資料科學端對端逐步解說)
資料瀏覽是建立資料模型很重要的一部分，而且牽涉到檢視用於分析的資料物件摘要，以及資料視覺化。 在這一課，您將同時使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中包含的 R 函數，來瀏覽資料物件並產生繪圖。  
  
然後，您將使用隨 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]安裝的套件所提供的新函數，來產生繪圖以視覺化資料。  
  
> [!TIP]  
> 已經是 R 大師了嗎？  
>   
> 現在您已下載所有資料並備妥環境，您可以自由地在 RStudio 或任何其他環境中執行完整的 R 指令碼，並自行瀏覽功能。 只要開啟 RSQL_Walkthrough.R 檔案並反白顯示和執行每一行，或將整個指令碼當作示範來執行。  
>   
> 若要取得 RevoScaleR 函數的其他說明，以及在 R 中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的秘訣，請繼續進行本教學課程。 它會使用完全相同的指令碼。  
  
## <a name="verify-downloaded-data-using-sql"></a>使用 SQL 確認下載的資料  
首先，花點時間確定您的資料已正確載入。  
  
1.  連接到您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
    您可以使用各種工具來連接並檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
    -   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]    
    -   Visual Studio 中的伺服器總管  
  
2.  展開您建立的資料庫。 下圖顯示 [伺服器總管] 中新的資料庫、資料表和函數。  
  
    ![new database objects created by script](../../advanced-analytics/r-services/media/rsql-e2e-ssms-newobjects.PNG "new database objects created by script")  
  
3.  您也可以針對資料執行簡單查詢。 例如，在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，以滑鼠右鍵按一下資料表，然後選取 [選取前 1000 個資料列] 產生並執行此查詢：  
  
    ```  
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]  
    ```  
    如果您在資料表中看不到任何資料，請參閱上一個主題中的[疑難排解](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)一節。
      
4.  若要檢視資料的結構描述和資料類型，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的系統管理檢視。  
  
    ```  
    SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
    FROM [TaxiSample].INFORMATION_SCHEMA.COLUMNS  
    WHERE TABLE_NAME = N'nyctaxi_sample';  
    ```  
  
    > [!TIP]  
    > 若要取得有關如何建立資料表的詳細資料，您也可以檢閱指令碼 `create-db-tb-upload-data.sql`。  
  
### <a name="generate-summaries-using-sql"></a>使用 SQL 產生摘要  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其中一項優點，使其成為 R 的得力助手，那就是能夠很快地執行以集合為基礎的計算。  針對本逐步解說建立資料表的程式碼也會應用[資料行存放區索引](../Topic/Columnstore%20Indexes%20Guide.md)，來加快計算速度。   
  
```  
SELECT DISTINCT [passenger_count]  
    , ROUND (SUM ([fare_amount]),0) as TotalFares   
    , ROUND (AVG ([fare_amount]),0) as AvgFares  
FROM [dbo].[nyctaxi_sample]  
GROUP BY [passenger_count]   
ORDER BY  AvgFares desc  
```  

在後續步驟中，您將使用 R，利用 SQL Server 中的資料來產生一些更複雜的摘要和繪圖。  
  
## <a name="next-steps"></a>後續步驟  
[使用 R 檢視及摘要資料 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/view-and-summarize-data-using-r-data-science-end-to-end-walkthrough.md)  
  
[使用 R 建立圖形和繪圖 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>上一課  
[第 1 課︰準備資料 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>另請參閱  
[資料行存放區索引指南](../Topic/Columnstore%20Indexes%20Guide.md)  
  
  
  
