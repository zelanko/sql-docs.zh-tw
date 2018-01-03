---
title: "第 5 課： 定型和儲存模型，使用 T-SQL |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: "10"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f0d6043d21d7d25be02cae2873e6ca7c0fb4c61d
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="lesson-5-train-and-save-a-model-using-t-sql"></a>第 5 課： 定型和儲存模型，使用 T-SQL

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在這一課，您將學習如何在機器學習模型定型使用。您將定型的模型使用您剛才建立的資料功能，然後將儲存已定型的模型中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。 在此情況下，R 封裝已安裝與[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，因此可以從 SQL 完成的所有項目。

## <a name="create-the-stored-procedure"></a>建立預存程序

當從 T-SQL 呼叫 R，您會使用系統預存程序中， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 不過，定型模型，例如經常重複的處理程序很容易封裝呼叫`sp_execute_exernal_script`在另一個預存程序。

1.  首先，建立包含建立提示預測模型的 R 程式碼的預存程序。 在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，開啟新**查詢**視窗，然後執行下列陳述式來建立預存程序_TrainTipPredictionModel_。 這個預存程序會定義輸入資料，並使用 R 套件來建立羅吉斯迴歸模型。

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTipPredictionModel]
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
      -- Insert the trained model into a database table
      INSERT INTO nyc_taxi_models
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model and put it in data frame
    trained_model <- data.frame(model=as.raw(serialize(logitObj, NULL)));
    ',
      @input_data_1 = @inquery,
      @output_data_1_name = N'trained_model'
      ;
    
    END
    GO
    ```

    - 不過，若要確保部分資料保留一段，來測試模型，70%的資料會隨機選取計程車資料表。
    
    - SELECT 查詢會使用自訂的純量函數 _fnCalculateDistance_ 計算上車和下車位置之間的直線距離。  查詢的結果會儲存在預設的 R 輸入變數 `InputDataset`中。
  
    - R 指令碼會呼叫`rxLogit`函式，是增強的 R 函數的其中一個隨附[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，以建立羅吉斯迴歸模型。
  
        二進位變數 _tipped_ 可做為「標籤」或結果資料行，而模型則是使用下列功能資料行進行調整︰_passenger_count_、_trip_distance_、_trip_time_in_secs_和 _direct_distance_。
  
    -   系統會序列化儲存在 R 變數 `logitObj` 中的定型模型，並將其放入資料框架以輸出至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 系統會將該輸出插入至資料庫資料表 _nyc_taxi_models_，以供您用於未來的預測。
  
2.  執行陳述式來建立預存程序中，如果不存在。

## <a name="generate-the-r-model-using-the-stored-procedure"></a>產生使用預存程序的 R 模型

因為預存程序已經包含輸入資料的定義，您不必提供輸入的查詢。

1. 若要產生 R 模型，請呼叫預存程序，不使用任何其他參數：

    ```SQL
    EXEC TrainTipPredictionModel
    ```

2. 監看式**訊息**視窗[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的訊息會經由管道輸出至 R 的**stdout**資料流，例如此郵件： 

    「 從外部指令碼的 STDOUT 訊息： Rows Read: 1193025，總計資料列處理： 1193025，時間總計區塊： 0.093 秒 」

    您也可能會看到訊息至個別的函數，特定`rxLogit`、 顯示變數和測試模型建立時產生的度量。

3.  陳述式完成後，請開啟資料表*nyc_taxi_models*。 資料處理，並配適模型可能需要一點時間。

    您可以看到當中已新增一個新的資料列，其 _model_資料行中包含序列化的模型。

    ```
    model
    ------
    0x580A00000002000302020....
    ```

在下一個步驟中，您將使用定型的模型來建立預測。

## <a name="next-lesson"></a>下一課

[第 6 課： 實施模型](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>上一課

[第 4 課： 建立使用 T-SQL 資料功能](..//tutorials/sqldev-create-data-features-using-t-sql.md)

