---
title: "建立新的 SQL Server 資料表，使用 rxDataStep |Microsoft 文件"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a5a8aaa8df1df4d34216f9d55806ccf5594292a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-new-sql-server-table-using-rxdatastep"></a>使用 rxDataStep 建立新的 SQL Server 資料表

在這一課，您將了解如何在記憶體中資料框架之間移動資料、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內容，以及本機檔案。

> [!NOTE]
> 在這一課，您將使用不同的資料集。 Airline 延遲 dataset 是廣泛用於機器學習實驗的公用資料集。 如果您才剛開始使用 R，這是很適合測試用的資料集，用於已和 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 一起發行的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的各種產品範例。 這個範例所需的資料檔案提供於與其他產品範例相同的目錄。

## <a name="create-sql-server-table-from-local-data"></a>從本機資料建立 SQL Server 資料表

在本教學課程的第一個部分中，使用**RxTextData** R 從文字檔案，將資料匯入函式，並接著使用**RxDataStep**函式將資料插入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

在這一課，您將使用不同的方式，以及從 [XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format)儲存的檔案取得資料。 XDF 格式是針對高維度資料開發的 XML 標準。 它是最佳化資料列和資料行處理與分析之 R 介面的二進位檔案格式。  您可以使用它來移動資料以及儲存對分析有用的資料子集。

使用 XDF 檔案對資料執行一些輕量型轉換之後，您會將轉換的資料儲存至新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。

> [!NOTE]
> 在此步驟，您將需要 DDL 權限。

1. 將計算內容設為您的本機工作站。
  
    ```R
    rxSetComputeContext("local")
    ```
  
2. 使用 **RxXdfData** 函數，來定義新的資料來源物件。 針對 XDF 資料來源，您只需要指定資料檔案的路徑。  您可以指定文字變數，該檔案的路徑但在此情況下，很方便的捷徑，因為範例資料檔 (AirlineDemoSmall.xdf) 具有 rxGetOption 函數所傳回的目錄。
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. 呼叫 rxGetVarInfo 記憶體中的資料，以檢視資料集的摘要。
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**結果**

*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*

*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*

> [!NOTE]
> 
> 您是否注意到您不需要呼叫其他函式將資料載入至 XDF 檔案，並無法呼叫 rxGetVarInfo 的資料立即？ 原因是 XDF 是 RevoScaleR 的預設暫時儲存方法。 如需 XDF 檔案的詳細資訊，請參閱[建立 XDF](https://msdn.microsoft.com/microsoft-r/scaler-data-xdf)。
  
4. 現在，您將此資料放入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，並將 _DayOfWeek_ 儲存為從 1 到 7 的整數值。
  
    若要這樣做，請先定義 SQL Server 資料來源。
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. 檢查是否有相同名稱的資料表存在，並刪除存在的資料表。
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. 建立資料表，然後使用 **rxDataStep**的各種產品範例。 此函式移動兩個資料已經定義資料來源，而且可以在轉換資料路由。
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    這是相當大的資料表，因此請稍候，而您將會看到最終狀態訊息：*Rows Read: 200000, Total Rows Processed: 600000*。
     
7. 將計算內容設定回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. 在新的資料表上使用簡單 SQL 查詢，建立新的 SQL Server 資料來源。 此定義會使用 RxSqlServerData 的 *colInfo* 引數，為 *DayOfWeek* 資料行加入因數層級。
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. 呼叫 rxSummary 一次，以檢閱您在查詢中資料的摘要。
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>下一個步驟

[執行區塊使用 rxDataStep 分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>上一個步驟

[將資料載入至使用 rxImport 記憶體](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)



