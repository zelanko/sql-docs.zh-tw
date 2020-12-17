---
title: R 教學課程：定型和儲存模型
titleSuffix: SQL machine learning
description: 在這五部分教學課程系列的第四部分中，您將在 SQL Server 上使用 Transact-SQL 搭配 SQL 機器學習，以 R 定型和儲存模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current'
ms.openlocfilehash: fe2d2a741e6e671eaadef96ee8539862535e51d7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470099"
---
# <a name="r-tutorial-train-and-save-model"></a>R 教學課程：定型和儲存模型
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

在這五部分教學課程系列的第四部分中，您將了解如何使用 R 來定型機器學習模型。您將使用在上一個部分中建立的資料功能來定型模型，然後將定型的模型儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。 在此情況下，R 套件已隨 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]安裝，因此可以從 SQL 完成所有作業。

在本文中，您將：

> [!div class="checklist"]
> + 使用 SQL 預存程序建立和定型模型
> + 將定型的模型儲存至 SQL 資料表

在[第一部分](r-taxi-classification-introduction.md)中，您已安裝必要條件並還原範例資料庫。

在[第二部分](r-taxi-classification-explore-data.md)中，您已檢閱範例資料並產生一些繪圖。

在[第三部分](r-taxi-classification-create-features.md)中，您已了解如何使用 Transact-SQL 函式，從未經處理的資料建立特徵。 接著，您從預存程序呼叫該函式，建立了包含特徵值的資料表。

在[第五部分](r-taxi-classification-deploy-model.md)中，您將了解如何運作您在第四部分中定型並儲存的模型。

## <a name="create-the-stored-procedure"></a>建立預存程序

從 T-SQL 呼叫 R 時，您會使用系統預存程序 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 但是，對於經常重複的流程 (例如重新訓練模型)，將對 `sp_execute_external_script` 的呼叫封裝在另一個預存程序中會更輕鬆。

1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，開啟新的 [查詢] 視窗。

2. 執行下列陳述式來建立預存程序 **RTrainLogitModel**。 這個預存程序會定義輸入資料，並使用 **glm** 建立羅吉斯迴歸模型。

   ```sql
   CREATE PROCEDURE [dbo].[RTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
   
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
   logitObj <- glm(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet, family = binomial)
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

   + 為了確保會剩下一些資料來測試模型，系統會從計程車資料表隨機選取 70% 的資料，以供定型之用。

   + SELECT 查詢會使用自訂的純量函數 *fnCalculateDistance* 計算上車和下車位置之間的直線距離。 查詢的結果會儲存在預設的 R 輸入變數 `InputDataset`中。
  
   + R 指令碼呼叫 R 函數 **glm** 來建立羅吉斯迴歸模型。
  
     二進位變數 _tipped_ 可做為「標籤」或結果資料行，而模型則是使用下列功能資料行進行調整︰_passenger_count_、_trip_distance_、_trip_time_in_secs_ 和 _direct_distance_。
  
   + 儲存在 R 變數 `logitObj` 中的定型模型會被序列化並作為輸出參數返回。

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>使用預存程序定型和部署 R 模型

因為預存程序已經包含輸入資料的定義，因此您不需要提供輸入查詢。

1. 若要定型和部署 R 模型，請呼叫預存程序並將它插入資料庫資料表 _nyc_taxi_models_ 中，以針對未來的預測使用：

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXEC RTrainLogitModel @model OUTPUT;
   INSERT INTO nyc_taxi_models (name, model) VALUES('RTrainLogit_model', @model);
   ```

2. 觀察 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的 [訊息] 視窗，查看將通過管道傳遞到 R 的 **stdout** 資料流的訊息，例如下列訊息： 

   STDOUT message(s) from external script:Rows Read:1193025, Total Rows Processed:1193025, Total Chunk Time:0.093 seconds"

3. 當陳述式完成時，開啟資料表 *nyc_taxi_models*。 資料處理和模型調整可能需要一些時間。

   您可以看到當中已新增一個新的資料列，其 _model_ 資料行中包含序列化的模型，以及 _name_ 資料行中的模型名稱 **RTrainLogit_model**。

   ```text
   model                        name
   ---------------------------- ------------------
   0x580A00000002000302020....  RTrainLogit_model
   ```

在本教學課程的下一個部分中，您將使用定型的模型來產生預測。

## <a name="next-steps"></a>後續步驟

在本文章中，您將：

> [!div class="checklist"]
> + 已使用 SQL 預存程序建立和定型模型
> + 已將定型的模型儲存至 SQL 資料表

> [!div class="nextstepaction"]
> [R 教學課程：在 SQL 預存程序中執行預測](r-taxi-classification-deploy-model.md)
