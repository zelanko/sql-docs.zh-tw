---
title: "轉換 R 服務中使用的 R 程式碼 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 轉換 R 服務中使用的 R 程式碼
當您將 R 程式碼從 R Studio 或另一個環境移至 SQL Server 時，通常使用的程式碼將不需要進一步修改時加入至 *@script* 參數 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 特別是如果您開發方案使用 ScaleR 函式，因此若要變更執行內容相當簡單。    
    
不過，通常會想要修改 R 程式碼來執行 SQL server 會同時利用更緊密的整合與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，並避免資料傳輸成本。   
   
   
## 資源  
  
若要檢視如何執行 R 程式碼，在 SQL Server 中的範例，請參閱這些逐步解說︰   
+ [資料庫中 SQL 開發人員分析](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)    
  示範如何讓您的 R 程式碼更模組化，並在預存程序  
+ [端對端資料科學解決方案](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)    
  R 和 T-SQL 中包含的特性工程設計的比較

## SQL Server 中的資料科學程序的變更  
  
當您使用 [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)], ，RStudio，或其他環境中，一般的工作流程是將資料提取到您的電腦、 分析資料，然後寫出或顯示結果。 不過，當獨立 R 程式碼移轉至 SQL Server 時，此程序的許多簡化或委派給其他 SQL Server 工具︰

| 外部程式碼 | SQL Server 中的 R |
|-------|-------|
| 擷取資料| 輸入的資料定義為資料庫內部的 SQL 查詢 | 
| 摘要，並將資料視覺化| 沒有變更。可以匯出為影像或傳送到遠端工作站的繪圖|
|功能工程| 您可以使用 R 中的資料庫，但它可以更有效率的方式呼叫 T-SQL 函數或自訂的 Udf|
|資料清理分析程序的一部分| 資料清理可以委派給 ETL 程序和事先執行|
|將預測輸出至檔案| 輸出資料表或換行的預測 `predict` 應用程式的直接存取的預存程序|
  

  
## 最佳作法  
  
+ 事先記下的相依性，例如必要的套件。 在開發和測試環境中，可能可以做為您的程式碼的一部分安裝封裝，但這是不良作法，在生產環境中。 通知系統管理員，使封裝可以安裝和測試後再部署您的程式碼。  
+ 請輸入問題的可能資料的檢查清單。 文件的結構描述的程式碼的每個區段中預期的結果。  
+ 識別主要資料來源，例如模型定型資料或對等因素、 其他的群組變數等的第二個來源的預測的輸入的資料。 對應的輸入參數的最大資料集 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。  
+ 變更您輸入的資料的陳述式來直接在資料庫中。 而不是將資料移至本機的 CSV 檔案，或進行重複呼叫 ODBC，得到更好的效能使用 SQL 查詢或檢視，可以直接對資料庫執行避免資料移動。  
+ 使用 SQL Server 查詢計畫來找出可以平行執行的工作。 如果輸入的查詢可平行處理，設定 `@parallel=1` sp_execute_external_script 程式引數的一部分。 平行處理這個旗標是通常可能隨時 SQL Server 可以使用資料分割資料表或分散在多個處理序之間的查詢和彙總的結果。 
   平行處理這個旗標通常是不可能如果您使用需要要讀取的所有資料的演算法訓練模型，或是如果您要建立彙總。 
+ 如果可行的話，取代傳統的 R 函式與 **ScaleR** 支援分散式的執行的函式。 如需詳細資訊，請參閱 [比較函式的小數位數 R 和 CRAN R](Summary%20of%20rx%20Functions.md)。
+ 檢閱您的 R 程式碼，以判斷是否可以獨立執行，或使用不同的預存程序呼叫更有效率地執行的步驟。 例如，您可能決定分開執行擷取的特徵工程設計和特性，並將值加入新的資料行。 以集合為基礎的計算使用 T-SQL，而不是 R 程式碼。 一種比較效能的功能工程工作 Udf 和 R 的 R 解決方案的詳細資訊，請參閱本教學課程︰ [資料科學的端對端逐步解說](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)。  
  
    
## 限制    
 請注意下列限制時轉換 R 程式碼︰    
   
**資料類型**    
-   支援的所有 R 資料類型。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援更多種類的資料型別比 R，因此傳送時，會執行某些隱含資料型別轉換 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料以及 R。 您可能也需要明確轉型或轉換部分資料。    
    
- 支援 NULL 值。 使用 R `na` 資料建構來表示遺漏值，類似於 null。    
    
- 如需詳細資訊，請參閱 [R 資料型別](../../advanced-analytics/r-services/working-with-r-data-types.md)。    
 
 **輸入及輸出**   
+ 您可以定義只有一個輸入資料集的預存程序參數的一部分。 這個預存程序的輸入的查詢可以是任何有效的單一 SELECT 陳述式。 我們建議您使用此輸入的最大的資料集，並視需要使用呼叫 RODBC 取得較小的資料集。 

+ 預存程序加上執行的呼叫不能做為 sp_execute_external_script 的輸入。    
    
+ 輸入資料集中的所有資料行必須對應至 R 指令碼中的變數。 變數會自動對應名稱。 例如，假設您的 R 指令碼包含此類公式︰    
    
    ```    
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek    
    ```    
    
     如果輸入資料集不包含 ArrDelay、 CRSDepTime、 DayOfWeek、 CRSDepHour 和 DayOfWeek 相符名稱的資料行，就會引發錯誤。    

+ 您也可以提供多個純量參數做為輸入。 不過，您將傳遞做為參數的預存程序中的任何變數 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 必須對應到 R 程式碼中的變數。 根據預設，變數會依名稱對應。
+ 若要包含純量輸入的變數的 R 程式碼的輸出中，只是附加 **輸出** 關鍵字定義的變數。             
+ 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，R 程式碼僅限於輸出為 data.frame 物件的單一資料集。 不過，您也可以輸出多個純量輸出的二進位格式，包括繪圖和 varbinary 格式中的模型。    
    
+ 您通常可以輸出資料集傳回的 R 指令碼，而不需要使用與結果集未定義的選項指定輸出資料行的名稱。 不過，您想要輸出的 R 指令碼中的任何變數必須對應到 SQL 輸出參數。
    
+ 如果您的 R 指令碼會使用引數 `@parallel=1`, ，您必須定義輸出結構描述。 原因是 SQL Server 執行查詢，以平行方式，在結束時所收集的結果，可能會建立多個處理序。 因此，可以建立的平行處理程序之前，必須定義輸出結構描述。

 **相依性**
 + 避免 R 程式碼從安裝套件。 SQL Server 上應該預先安裝套件。  
  
  
  

