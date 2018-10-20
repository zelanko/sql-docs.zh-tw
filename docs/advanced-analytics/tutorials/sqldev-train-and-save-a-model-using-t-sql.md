---
title: 課程 3 的訓練和儲存模型，使用 R 和 T-SQL （SQL Server 機器學習服務） |Microsoft Docs
description: 教學課程示範如何在 SQL Server 中內嵌 R 預存程序和 T-SQL 函數
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 73e1b2ef70821af2247de000eba45a495075e614
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2018
ms.locfileid: "49463023"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>第 3 課： 訓練及儲存模型，使用 T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在這一課，您將了解如何使用 r 來定型機器學習服務模型您將使用您在上一課中建立資料特徵來定型模型，然後將儲存的定型的模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。 在此情況下，R 套件已安裝與[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，因此可以從 SQL 進行的所有項目。

## <a name="create-the-stored-procedure"></a>建立預存程序

當從 T-SQL 呼叫 R，您會使用系統預存程序中， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 不過，重複執行的情況下，例如重新定型模型，處理程序很容易封裝呼叫`sp_execute_exernal_script`在另一個預存程序。

1.  首先，建立包含 R 程式碼，建立提示預測模型的預存程序。 在  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，開啟新**查詢**視窗，然後執行下列陳述式來建立預存程序_TrainTipPredictionModel_。 這個預存程序會定義輸入資料，並使用 R 套件來建立羅吉斯迴歸模型。

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

    - 不過，若要確保某些資料會剩下來測試模型，70%的資料會隨機選取從計程車資料表。
    
    - SELECT 查詢會使用自訂的純量函數 _fnCalculateDistance_ 計算上車和下車位置之間的直線距離。  查詢的結果會儲存在預設的 R 輸入變數 `InputDataset`中。
  
    - R 指令碼會呼叫`rxLogit`函式，也就是其中一個增強型 R 函數隨附[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，以建立羅吉斯迴歸模型。
  
        二進位變數 _tipped_ 可做為「標籤」或結果資料行，而模型則是使用下列功能資料行進行調整︰_passenger_count_、_trip_distance_、_trip_time_in_secs_和 _direct_distance_。
  
    -   系統會序列化儲存在 R 變數 `logitObj` 中的定型模型，並將其放入資料框架以輸出至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 系統會將該輸出插入至資料庫資料表 _nyc_taxi_models_，以供您用於未來的預測。
  
2.  如果不存在，請執行陳述式來建立預存程序。

## <a name="generate-the-r-model-using-the-stored-procedure"></a>產生使用預存程序，在 R 模型

預存程序已經包含輸入資料的定義，因為您不必提供輸入的查詢。

1. 若要產生 R 模型，請呼叫預存程序，而不需要任何其他參數：

    ```SQL
    EXEC TrainTipPredictionModel
    ```

2. 監看式**訊息**窗口[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]經由管道輸出至 R 的訊息**stdout**資料流，就如同此訊息： 

    「 從外部指令碼的 STDOUT 訊息︰ Rows Read: 1193025，Total Rows Processed: 1193025，Total Chunk Time: 0.093 seconds"

    您也可能會看到個別的函數，特定訊息`rxLogit`、 顯示變數與測試的模型建立過程中產生的度量。

3.  陳述式完成之後，請開啟資料表*nyc_taxi_models*。 資料處理和模型調整可能需要一段時間。

    您可以看到當中已新增一個新的資料列，其 _model_資料行中包含序列化的模型。

    ```
    model
    ------
    0x580A00000002000302020....
    ```

在下一個步驟中，您將使用定型的模型來建立預測。

## <a name="next-lesson"></a>下一課

[第 4 課： 將模型作業化](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>上一課

[第 2 課： 建立使用 R 和 T-SQL 函式的資料特徵](..//tutorials/sqldev-create-data-features-using-t-sql.md)

