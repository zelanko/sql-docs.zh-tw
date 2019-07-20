---
title: '第3課: 使用 R 和 T-sql 來定型和儲存模型'
description: 教學課程示範如何使用 SQL Server 預存程式和 T-sql 函數來定型、序列化和儲存 R 模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0d26f549bcca4860f4febe01a868f360edfa4fa2
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345866"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>第 3 課：使用 T-sql 定型及儲存模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有關如何在 SQL Server 中使用 R 的 SQL 開發人員教學課程的一部分。

在這一課, 您將瞭解如何使用 R 來定型機器學習模型。您將使用您在上一課中建立的資料功能來定型模型, 然後將定型的模型儲存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表中。 在此情況下, R 封裝已隨一起[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]安裝, 因此可以從 SQL 完成所有作業。

## <a name="create-the-stored-procedure"></a>建立預存程式

從 T-sql 呼叫 R 時, 您會使用系統預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 不過, 對於您經常重複的進程 (例如重新定型模型), 在另一個預存程式中將 sp_execute_exernal_script 的呼叫封裝起來比較容易。

1. 在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中, 開啟新的**查詢**視窗。

2. 執行下列語句來建立預存程式**RxTrainLogitModel**。 這個預存程式會定義輸入資料, 並使用來自 RevoScaleR 的**rxLogit**來建立羅吉斯回歸模型。

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

    - 為了確保某些資料會停留在測試模型, 會從計程車資料表隨機選取 70% 的資料, 以供定型之用。

    - SELECT 查詢會使用自訂的純量函數 *fnCalculateDistance* 計算上車和下車位置之間的直線距離。 查詢的結果會儲存在預設的 R 輸入變數`InputDataset`中。
  
    - R 腳本會呼叫**rxLogit**函數 (這是隨附[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的其中一個增強 R 函數) 來建立羅吉斯回歸模型。
  
        二進位變數 _tipped_ 可做為「標籤」  或結果資料行，而模型則是使用下列功能資料行進行調整︰_passenger_count_、_trip_distance_、_trip_time_in_secs_和 _direct_distance_。
  
    - 儲存在 R 變數`logitObj`中的定型模型會序列化並當做輸出參數傳回。

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>使用預存程式來定型和部署 R 模型

因為預存程式已經包含輸入資料的定義, 所以您不需要提供輸入查詢。

1. 若要定型和部署 R 模型, 請呼叫預存程式並將它插入至資料庫資料表_nyc_taxi_models_, 讓您可以將它用於未來的預測:

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. 針對會輸送至 R **stdout**資料流程的訊息, 監看的 [**訊息**] 視窗, 如下列訊息所示: [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 

    來自外部腳本的 STDOUT 訊息:讀取的資料列:1193025, 已處理的資料列總數:1193025, 總區塊時間:0.093 秒」

    您也可能會看到個別函數的特定訊息, `rxLogit`顯示在模型建立過程中產生的變數和測試計量。

3.  當語句完成時, 開啟資料表*nyc_taxi_models*。 處理資料並對模型進行調整可能需要一段時間。

    您可以看到已經加入一個新的資料列, 其中包含資料行_模型_中的序列化模型, 以及資料行_名稱_中的模型名稱**RxTrainLogit_model** 。

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

在下一個步驟中, 您將使用定型的模型來產生預測。

## <a name="next-lesson"></a>下一課

[第 4 課：在預存程式中使用 R 模型來預測潛在結果](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>上一課

[第 2 課：使用 R 和 T-sql 函數建立資料特徵](..//tutorials/sqldev-create-data-features-using-t-sql.md)

