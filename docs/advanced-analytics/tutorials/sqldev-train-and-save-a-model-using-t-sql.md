---
title: R + T-SQL 教學課程：定型模型
description: 教學課程示範如何使用 SQL Server 預存程序和 T-SQL 函式來定型、序列化和儲存 R 模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 406f8e1c60c5820f9edaaf7760b7aeed321d2611
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73724453"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>第 3 課：使用 T-SQL 定型及儲存模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本篇教學課程文章適用 SQL 開發人員，說明如何在 SQL Server 中使用 R。

在本課程中，您將學習如何使用 R 來定型機器學習模型。您將使用在上一課中建立的資料功能來定型模型，然後將定型的模型儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。 在此情況下，R 套件已隨 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]安裝，因此可以從 SQL 完成所有作業。

## <a name="create-the-stored-procedure"></a>建立預存程序

從 T-SQL 呼叫 R 時，您會使用系統預存程序 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 但是，對於經常重複的程序 (例如重新定型模型)，更輕鬆的方式可能是封裝另一個預存程序中對 sp_execute_exernal_script 的呼叫。

1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，開啟新的 [查詢]  視窗。

2. 執行下列陳述式來建立預存程序 **RxTrainLogitModel**。 這個預存程序會定義輸入資料，並使用 RevoScaleR 的 **rxLogit** 來建立羅吉斯迴歸模型。

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

    - 為了確保會剩下一些資料來測試模型，系統會從計程車資料表隨機選取 70% 的資料，以供定型之用。

    - SELECT 查詢會使用自訂的純量函數 *fnCalculateDistance* 計算上車和下車位置之間的直線距離。 查詢的結果會儲存在預設的 R 輸入變數 `InputDataset`中。
  
    - R 指令碼會呼叫 **rxLogit** 函數 (其為 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 隨附的其中一個增強 R 函數)，以建立羅吉斯迴歸模型。
  
        二進位變數 _tipped_ 可做為「標籤」  或結果資料行，而模型則是使用下列功能資料行進行調整︰_passenger_count_、_trip_distance_、_trip_time_in_secs_和 _direct_distance_。
  
    - 儲存在 R 變數 `logitObj` 中的定型模型會被序列化並作為輸出參數返回。

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>使用預存程序定型和部署 R 模型

因為預存程序已經包含輸入資料的定義，因此您不需要提供輸入查詢。

1. 若要定型和部署 R 模型，請呼叫預存程序並將它插入資料庫資料表 _nyc_taxi_models_ 中，以針對未來的預測使用：

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. 觀察 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的 [訊息]  視窗，查看將通過管道傳遞到 R 的 **stdout** 資料流的訊息，例如下列訊息： 

    STDOUT message(s) from external script:Rows Read:1193025, Total Rows Processed:1193025, Total Chunk Time:0.093 seconds"

    您也可能會看到個別 `rxLogit` 函式的特定訊息，其顯示在模型建立過程中產生的變數和測試單位。

3.  當陳述式完成時，開啟資料表 *nyc_taxi_models*。 資料處理和模型調整可能需要一些時間。

    您可以看到當中已新增一個新的資料列，其 _model_ 資料行中包含序列化的模型，以及 _name_ 資料行中的模型名稱 **RxTrainLogit_model**。

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

在下一個步驟中，您將使用定型的模型來產生預測。

## <a name="next-lesson"></a>下一課

[第 4 課：在預存程序中使用 R 模型預測可能的結果](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>上一課

[第 2 課：使用 R 和 T-SQL 函式建立資料特徵](..//tutorials/sqldev-create-data-features-using-t-sql.md)

