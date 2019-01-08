---
title: 課程 3 的定型及儲存使用 R 和 T-SQL-SQL Server Machine Learning 模型
description: 教學課程示範如何訓練、 序列化及儲存 R 模型來使用 SQL Server 預存程序和 T-SQL 函式。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f3abe58aac4d5920e64337f63a40dc8f87fb12d9
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645107"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>第 3 課：訓練及儲存模型，使用 T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在這一課，您將了解如何使用 r 來定型機器學習服務模型您將使用您在上一課中建立資料特徵來定型模型，然後將儲存的定型的模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。 在此情況下，R 套件已安裝與[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，因此可以從 SQL 進行的所有項目。

## <a name="create-the-stored-procedure"></a>建立預存程序

當從 T-SQL 呼叫 R，您會使用系統預存程序中， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 不過，處理序重複執行的情況下，例如重新定型模型，它是您更輕鬆地將封裝另一個預存程序 sp_execute_exernal_script 的呼叫。

1. 在  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，開啟新**查詢**視窗。

2. 執行下列陳述式，建立預存程序**RxTrainLogitModel**。 這個預存程序會定義輸入的資料，並使用**rxLogit**來自 RevoScaleR 建立羅吉斯迴歸模型。

    ```sql
    CREATE PROCEDURE [dbo].[RxTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
    
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model 
    trained_model <- as.raw(serialize(logitObj, NULL));
    ',
      @input_data_1 = @inquery,
      @params = N'@trained_model varbinary(max) OUTPUT',
      @trained_model = @trained_model OUTPUT; 
    END
    GO
    ```

    - 若要確保某些資料會剩下來測試模型，會從定型基於計程車資料表隨機選取 70%的資料。

    - SELECT 查詢會使用自訂的純量函數 *fnCalculateDistance* 計算上車和下車位置之間的直線距離。 查詢的結果會儲存在預設 R 輸入變數， `InputDataset`。
  
    - R 指令碼會呼叫**rxLogit**函式，也就是其中一個增強型 R 函數隨附[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，以建立羅吉斯迴歸模型。
  
        二進位變數 _tipped_ 可做為「標籤」或結果資料行，而模型則是使用下列功能資料行進行調整︰_passenger_count_、_trip_distance_、_trip_time_in_secs_和 _direct_distance_。
  
    - 定型的模型，並儲存在 R 變數`logitObj`序列化，是做為輸出參數傳回。

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>定型和部署 R 模型，使用預存程序

預存程序已經包含輸入資料的定義，因為您不必提供輸入的查詢。

1. 若要定型和部署 R 模型，呼叫預存程序並將它插入資料庫資料表_nyc_taxi_models_，如此一來，您可以將它用於未來的預測：

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. 監看式**訊息**窗口[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]經由管道輸出至 R 的訊息**stdout**資料流，就如同此訊息： 

    「 從外部指令碼的 STDOUT 訊息：Rows Read:1193025，total 處理的資料列：1193025，total 區塊時間：0.093 seconds"

    您也可能會看到個別的函數，特定訊息`rxLogit`、 顯示變數與測試的模型建立過程中產生的度量。

3.  陳述式完成之後，請開啟資料表*nyc_taxi_models*。 資料處理和模型調整可能需要一段時間。

    您可以看到的一個新的資料列已經加入，其中包含資料行中的序列化的模型_模型_和 模型名稱**RxTrainLogit_model**資料行中_名稱_。

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

在下一個步驟中，您將使用定型的模型來產生預測。

## <a name="next-lesson"></a>下一課

[第 4 課：預測潛在的預存程序中使用 R 模型的結果](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>上一課

[第 2 課：使用 R 和 T-SQL 函式建立資料特徵](..//tutorials/sqldev-create-data-features-using-t-sql.md)

