---
title: 若要從 SQL Server Machine Learning 中使用 R 模型預測並繪製的快速入門 |Microsoft Docs
description: 在此快速入門中，了解評分使用 R 和 SQL Server 資料中的預先建置的模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 60e152948945f4e86cc1114ae7b20c0e48b403bf
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086650"
---
# <a name="quickstart-predict-and-plot-from-model-using-r-in-sql-server"></a>快速入門： 從預測並繪製在 SQL Server 中使用 R 模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入門中，使用您在要評分新資料的預測先前的快速入門中建立的模型。 若要執行_評分_使用新的資料，從資料表取得其中一個定型模型，然後呼叫 一組新的資料上要做預測。 計分是有時會用於表示產生預測、 機率或其他值根據送入定型模型的新資料的資料科學的詞彙。

## <a name="prerequisites"></a>先決條件

本快速入門是擴充功能[建立預測模型](rtsql-create-a-predictive-model-r.md)。

## <a name="create-the-table-of-new-speeds"></a>建立新速度的資料表

您是否注意到原始的定型資料是以每小時 25 英里的速度停止？ 這是因為原始資料所根據的是來自 1920 年的實驗！

您可能想要知道 1920 年代的汽車需要多長時間才能停下來，假設它的速度可高達每小時 60 英里，或甚至可達每小時 100 英里？ 若要回答這個問題，您必須提供一些新的速度值。

```sql
CREATE TABLE [dbo].[NewCarSpeed]([speed] [int] NOT NULL,
    [distance] [int]  NULL) ON [PRIMARY]
GO
INSERT [dbo].[NewCarSpeed] (speed)
VALUES (40),  (50),  (60), (70), (80), (90), (100)
```

## <a name="predict-stopping-distance"></a>預測停止距離

現在，您的資料表可能包含多個 R 模型，所有模型都是使用不同的參數或演算法來建置，或是以不同的資料子集來定型。

![rsql_basictut_listofmodels](media/rsql-basictut-listofmodels.png)

若要取得一個特定的模型為基礎的預測，您必須撰寫會執行下列 SQL 指令碼：

1. 取得您所需的模型
2. 取得新的輸入資料
3. 呼叫與該模型相容的 R 預測函數

在此範例中，因為您的模型根據**rxLinMod**演算法的一部分**RevoScaleR**封裝時，呼叫[rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)函式，而非泛型 R`predict`函式。

```sql
DECLARE @speedmodel varbinary(max) = (SELECT model FROM [dbo].[stopping_distance_models] WHERE model_name = 'latest model');
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(speedmodel));
            new <- data.frame(NewCarData);
            predicted.distance <- rxPredict(current_model, new);
            str(predicted.distance);
            OutputDataSet <- cbind(new, ceiling(predicted.distance));
            '
    , @input_data_1 = N'SELECT speed FROM [dbo].[NewCarSpeed]'
    , @input_data_1_name = N'NewCarData'
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ 使用 SELECT 陳述式，從資料表取得單一模型，並傳遞它做為輸入參數。
+ 從資料表擷取模型之後，在模型上呼叫 `unserialize` 函數。

    > [!TIP] 
    > 也請查看新[序列化函式](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)提供的 RevoScaleR，支援[即時評分](../real-time-scoring.md)。
+  搭配適當引數將 `rxPredict` 函數套用至模型，並提供新的輸入資料。
+  在範例中，`str`函式會加入在測試階段中，若要檢查從 r 傳回的資料結構描述您可以移除之後的陳述式。
+ R 指令碼中使用的資料行名稱不一定會傳遞至預存程序的輸出。 這裡我們使用 WITH RESULTS 子句來定義一些新的資料行名稱。

**結果**

![rsql_basictut_scoringresults_smalldata](media/rsql-basictut-scoringresults-smalldata.PNG)

## <a name="perform-scoring-in-parallel"></a>以平行方式執行計分

在這個小型資料集中，預測是以相當快的速度回傳。 但是，假如您需要以非常快的速度進行大量預測？ 有許多種方式來加快 SQL Server 中的作業，如果作業可以平行處理。 特別是計分，有個簡單的方式是以新增*@parallel* sp_execute_external_script 的參數並將值設定為**1**。

假設您已取得更大型的可能車速表，其中包括數十萬個值。 有許多來自社群的範例 T-SQL 指令碼，可協助您產生數字資料表，因此我們將不會在此處重現那些指令碼。 我們只假設您有一個包含許多整數的資料行，而且想要使用該資料行做為模型中 `speed` 的輸入。

若要這樣做，只要執行相同的預測查詢，但替換成較大的資料集，並新增`@parallel = 1`引數。

```sql
DECLARE @speedmodel varbinary(max) = (select model from [dbo].[stopping_distance_models] where model_name = 'default model');
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(speedmodel));
            new <- data.frame(NewCarData);
            predicted.distance <- rxPredict(current_model, new);
            OutputDataSet <- cbind(new, ceiling(predicted.distance));
            '
    , @input_data_1 = N' SELECT [speed] FROM [dbo].[HugeTableofCarSpeeds] '
    , @input_data_1_name = N'NewCarData'
    , @parallel = 1
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ 平行執行在處理非常大型的資料時，才，通常會提供優點。 SQL 資料庫引擎可能會決定不需要 平行執行。 此外，取得資料的 SQL 查詢必須能夠產生平行查詢計劃。

+ 使用平行執行的選項時，您**必須**事先使用 WITH RESULT SETS 子句來指定輸出結果結構描述。 事先指定輸出結構描述，可讓 SQL Server 彙總多個平行資料集的結果，否則可能會有未知的結構描述。

+ 您若是*訓練*模型，而不是*評分*，此參數通常不會有作用。 根據模型類型，模型建立可能需要在可以建立摘要之前讀取所有資料列。

+ 若要取得平行處理，當您定型模型的優點，我們建議使用其中一種**RevoScaleR**演算法。 這些演算法設計用來自動分散處理，即使您未指定<code>@parallel =1</code>的呼叫中`sp_execute_external_script`。 如需如何取得 RevoScaleR 演算法的最佳效能的指引，請參閱 <<c0> [ 分散式和使用 Microsoft R 中的 ScaleR 的平行運算](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)。

## <a name="create-an-r-plot-of-the-model"></a>建立模型的 R 繪圖

許多用戶端 (包括 SQL Server Management Studio) 無法直接顯示使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 建立的繪圖。 相反地，產生 R 繪圖的一般程序是建立繪圖做為 R 程式碼的一部分，並接著將影像寫入檔案。

或者，您可以將序列化的二進位繪圖物件返回來顯示影像的任何應用程式。

下列範例示範如何使用預設隨附於 R 中的繪圖函數來建立簡單的圖形。影像會輸出到指定的檔案，同時也會透過預存程序輸出到 SQL 變數。

```sql
 EXECUTE sp_execute_external_script
 @language = N'R'
 , @script = N'
     imageDir <- ''C:\\temp\\plots'';
     image_filename = tempfile(pattern = "plot_", tmpdir = imageDir, fileext = ".jpg")
     print(image_filename);
     jpeg(filename=image_filename,  width=600, height = 800);
     print(plot(distance~speed, data=InputDataSet, xlab="Speed", ylab="Stopping distance", main = "1920 Car Safety"));
     abline(lm(distance~speed, data = InputDataSet));
     dev.off();
     OutputDataSet <- data.frame(data=readBin(file(image_filename, "rb"), what=raw(), n=1e6));
     '
  , @input_data_1 = N'SELECT speed, distance from [dbo].[CarSpeed]'
  WITH RESULT SETS ((plot varbinary(max)));
```

+ `tempfile`函式會傳回字串，可用來當做檔案名稱，但該檔案尚未產生。
+ 引數至`tempfile`，您可以指定前置詞和副檔名，以及目錄。 若要驗證的完整檔案名稱和路徑，列印訊息，使用`str()`。
+ `jpeg` 函數會使用指定的參數來建立 R 裝置。
+ 建立繪圖之後，您可以新增更多視覺功能給它。 在此情況下，使用加入迴歸線`abline`。
+ 當您完成加入繪圖功能之後，必須使用 `dev.off()` 函數來關閉圖形裝置。
+ `readBin` 函數會接受要讀取的檔案、格式規格，以及記錄數目。 `rb`* * ' 關鍵字表示檔案是二進位，而不是文字。

**結果**

![rsql_basictut_plotresult_small](media/rsql-basictut-plotresult-small.png)

如果您想要執行一些更複雜的繪圖，針對 R 使用一些很棒的圖形封裝，則我們推薦下列文章。 這兩篇文章都需要熱門的 **ggplot2** 封裝。

+ [使用 SQL Server 2016 R Services 的貸款分類 (英文)](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)︰以保險資料為基礎的完整案例。 需要**重塑**封裝。
+ [使用 R 建立圖形和繪圖](walkthrough-create-graphs-and-plots-using-r.md)

## <a name="next-steps"></a>後續步驟

R 與 SQL Server 的整合，讓您能夠更輕鬆地大規模部署 R 方案，運用 R 和關聯式資料庫的最佳功能，以進行高效能的資料處理和快速的 R 分析。 

繼續了解使用 SQL Server 中的 R，透過 Microsoft 資料科學和 R 服務的開發團隊所建立的端對端案例的解決方案。

> [!div class="nextstepaction"]
> [SQL Server R 教學課程](sql-server-r-tutorials.md)
