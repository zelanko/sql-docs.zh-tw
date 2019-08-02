---
title: 使用 R 建立 SSIS 和 SSRS 工作流程
description: 結合 SQL Server Machine Learning 服務和 R 服務、Reporting Services (SSRS) 和 SQL Server Integration Services (SSIS) 的整合案例。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2b8d55e95991437e4d76911fd26afb5b1bc9c550
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715176"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>使用 R on SQL Server 建立 SSIS 和 SSRS 工作流程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何使用內嵌的 R 和 Python 腳本, 並搭配兩個重要的 SQL Server 功能, 使用 SQL Server Machine Learning 服務的語言和資料科學功能:SQL Server Integration Services (SSIS) 和 SQL Server Reporting Services SSRS。 中的 R 和 Python 程式庫 SQL Server 提供統計和預測功能。 SSIS 和 SSRS 分別提供協調的 ETL 轉換和視覺效果。 本文說明如何將上述所有功能一起放在此工作流程模式中:

> [!div class="checklist"]
> * 建立包含可執行檔 R 或 Python 的預存程式
> * 從 SSIS 或 SSRS 執行預存程式

本文中的範例大多與 R 和 SSIS 有關, 但概念和步驟同樣適用于 Python。 第二節提供 SSRS 視覺效果的指引和連結。

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>使用 SSIS 進行自動化

資料科學工作流程的互動性很高，並涉及許多資料的轉換，包括縮放、彙總、機率計算，以及重新命名與合併屬性。 資料科學家已習慣以 R、Python 或其他語言執行許多這些工作；不過，在企業資料上執行這類工作流程需要與 ETL 工具和程序的緊密整合。

因為[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]可讓您透過 transact-sql 和預存程式在 R 中執行複雜的作業, 所以您可以將資料科學工作與現有的 ETL 進程整合。 資料準備作業可以使用最有效率的工具 (包括[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和[!INCLUDE[tsql](../../includes/tsql-md.md)]) 進行優化, 而不是執行一鏈記憶體密集型工作。 

以下是如何使用[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]來自動化資料處理和模型化管線的一些概念:

+ 從內部部署或雲端來源解壓縮資料, 以建立定型資料 
+ 建立並執行 R 或 Python 模型作為資料整合工作流程的一部分
+ 定期 (已排程) 重新訓練模型
+ 將 R 或 Python 腳本的結果載入至其他目的地, 例如 Excel、Power BI、Oracle 和 Teradata 等等。
+ 使用 SSIS 工作在 SQL 資料庫中建立資料功能
+ 使用條件分支來切換 R 和 Python 作業的計算內容

## <a name="ssis-example"></a>SSIS 範例

下列範例源自于立即淘汰的 MSDN blog 文章, 作者是 Jimmy Wong 在此 URL:`https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

這個範例會示範如何使用 SSIS 來自動化工作。 您可以使用 SQL Server Management Studio 來建立具有內嵌 R 的預存程式, 然後從 SSIS 封裝中的[執行 t-sql](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)工作執行這些預存程式。

若要逐步執行此範例, 您應該熟悉 Management Studio、SSIS、SSIS 設計工具、封裝設計和 T-sql。 SSIS 封裝會使用三個[執行 t-sql](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)工作, 將定型資料插入資料表、建立資料模型, 並對資料進行評分以取得預測輸出。

### <a name="load-training-data"></a>載入定型資料

在 SQL Server Management Studio 中執行下列腳本, 以建立用來儲存資料的資料表。 在此練習中, 您應該建立並使用測試資料庫。 

```T-SQL
Use test-db
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO
```

建立預存程式, 將定型資料載入資料框架中。 此範例使用內建的鳶尾花資料集。 

```T-SQL
Create procedure load_iris
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'iris_df <- iris;'
        , @input_data_1 = N''
        , @output_data_1_name = N'iris_df'
    with result sets (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100)));
end;
```

在 SSIS 設計師中, 建立執行您剛才定義之預存程式的「[執行 SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) 」工作。 **SQLStatement**的腳本會移除現有的資料、指定要插入的資料, 然後呼叫預存程式來提供資料。

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![插入資料](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "插入資料")

### <a name="generate-a-model"></a>產生模型

在 SQL Server Management Studio 中執行下列腳本, 以建立儲存模型的資料表。 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

建立使用[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)產生線性模型的預存程式。 RevoScaleR 和 revoscalepy 程式庫會自動在 SQL Server 的 R 和 Python 會話中使用, 因此不需要匯入程式庫。

```T-SQL
Create procedure generate_iris_rx_model
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'
          irisLinMod <- rxLinMod(Sepal.Length ~ Sepal.Width + Petal.Length + Petal.Width + Species, data = ssis_iris);
          trained_model <- data.frame(payload = as.raw(serialize(irisLinMod, connection=NULL)));'
        , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris'
        , @input_data_1_name = N'ssis_iris'
        , @output_data_1_name = N'trained_model'
    with result sets ((model varbinary(max)));
end;
GO
```

在 SSIS 設計師中, 建立「[執行 SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) 」工作來執行**generate_iris_rx_model**預存程式。 模型會序列化並儲存至 ssis_iris_models 資料表。 **SQLStatement**的腳本如下所示:

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![產生線性模型](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "產生線性模型")

作為檢查點, 在此工作完成後, 您可以查詢 ssis_iris_models, 以查看它是否包含一個二進位模型。

### <a name="predict-score-outcomes-using-the-trained-model"></a>使用「定型」模型來預測 (計分) 結果

現在您已經有載入定型資料並產生模型的程式碼, 剩下的唯一步驟就是使用模型來產生預測。 

若要這麼做, 請將 R 腳本放在 SQL 查詢中, 以觸發 ssis_iris_model 上的[rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict)內建 R 函數。 名為**predict_species_length**的預存程式會完成這項工作。

```T-SQL
Create procedure predict_species_length (@model varchar(100))
as
begin
    declare @rx_model varbinary(max) = (select model from ssis_iris_models where model_name = @model);
    -- Predict based on the specified model:
    exec sp_execute_external_script
        @language = N'R'
        , @script = N'
irismodel <-unserialize(rx_model);
irispred <- rxPredict(irismodel, ssis_iris[,2:6]);
OutputDataSet <- cbind(ssis_iris[1], irispred$Sepal.Length_Pred, ssis_iris[2]);
colnames(OutputDataSet) <- c("id", "Sepal.Length.Actual", "Sepal.Length.Expected");
#OutputDataSet <- subset(OutputDataSet, Species.Length.Actual != Species.Expected);
'
    , @input_data_1 = N'
    select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris
    '
    , @input_data_1_name = N'ssis_iris'
    , @params = N'@rx_model varbinary(max)'
    , @rx_model = @rx_model
    with result sets ( ("id" int, "Species.Length.Actual" float, "Species.Length.Expected" float)
        );
end;
```

在「SSIS 設計師」中, 建立執行**predict_species_length**預存程式的「[執行 SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) 」工作, 以產生預測的花瓣長度。

```T-SQL
exec predict_species_length 'rxLinMod';
```

![產生預測](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "產生預測")

### <a name="run-the-solution"></a>執行解決方案

在 SSIS 設計師中, 按 F5 執行封裝。 您應該會看到類似下列螢幕擷取畫面的結果。

![F5 以在 debug 模式中執行](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "F5 以在 debug 模式中執行")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>使用 SSRS 做為視覺效果

雖然 R 可以建立圖表和有趣的視覺效果, 但它並未與外部資料源妥善整合, 這表示每個圖表或圖形都必須個別產生。 此外，可能也很難進行共用。

藉由[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]使用, 您可以透過[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程式在 R 中執行複雜的作業, 這可輕鬆地由各種企業報告工具 ( [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]包括和 Power BI) 使用。

### <a name="ssrs-example"></a>SSRS 範例

[R Graphics Device for Microsoft Reporting Services (SSRS) (英文)](https://rgraphicsdevice.codeplex.com/)

此 CodePlex 專案提供的程式碼可協助您建立自訂報表專案, 將 R 的圖形輸出轉譯成可在報表中[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]使用的影像。  透過使用自訂報表項目，您可以：

+ 將使用 R Graphics Device 建立的圖表和繪圖發佈到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 儀表板

+ 將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 參數傳遞給 R 繪圖

> [!NOTE]
> 針對此範例, 支援 R 圖形裝置的 Reporting Services 的程式碼必須安裝在 Reporting Services 伺服器上, 以及 Visual Studio。 此外，還需要手動編譯和設定。

## <a name="next-steps"></a>後續步驟

本文中的 SSIS 和 SSRS 範例說明執行包含內嵌 R 或 Python 腳本之預存程式的兩個案例。 重要的重點是, 您可以將 R 或 Python 腳本提供給任何應用程式或工具, 以便在預存程式上傳送執行要求。 SSIS 的另一個重點是, 您可以建立封裝, 以自動化和排程各種作業, 例如資料取得、清理、操作等等, 以及包含在作業鏈中的 R 或 Python 資料科學功能。 如需詳細資訊和想法, 請參閱[在 SQL Server Machine Learning 服務中使用預存程式來讓 R 程式碼](operationalizing-your-r-code.md)。