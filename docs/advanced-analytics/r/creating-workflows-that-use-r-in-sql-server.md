---
title: 使用 R-SQL Server Machine Learning 服務建立的 SSIS 和 SSRS 的工作流程
description: 結合 SQL Server 機器學習服務和 R Services、 Reporting Services (SSRS) 和 SQL Server Integration Services (SSIS) 的整合案例。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a9f3a76ac1829f529e0f3e5459ab842dcafa7c80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962691"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>使用 R 在 SQL Server 上建立 SSIS 和 SSRS 的工作流程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何使用內嵌的 R 和 Python 指令碼使用兩個重要的 SQL Server 功能的 SQL Server Machine Learning 服務的語言和資料科學功能：SQL Server Integration Services (SSIS) 和 SQL Server Reporting Services SSRS。 SQL Server 中的 R 和 Python 程式庫提供的統計和預測函數。 SSIS 和 SSRS 分別提供協調 ETL 的轉換和視覺效果。 這篇文章說明如何將所有這些功能一起放在此模式中工作流程：

> [!div class="checklist"]
> * 建立包含可執行的 R 或 Python 的預存程序
> * 從 SSIS 或 SSRS 執行預存程序

這篇文章中的範例多半是 R 和 SSIS，但概念和步驟同樣適用於 Python。 第二個區段將提供 SSRS 視覺效果的指引和連結。

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>使用 SSIS 進行自動化

資料科學工作流程的互動性很高，並涉及許多資料的轉換，包括縮放、彙總、機率計算，以及重新命名與合併屬性。 資料科學家已習慣以 R、Python 或其他語言執行許多這些工作；不過，在企業資料上執行這類工作流程需要與 ETL 工具和程序的緊密整合。

因為[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]可讓您在 R 中執行複雜的作業，透過 TRANSACT-SQL 和預存程序，您可以整合現有的 ETL 程序中的資料科學工作。 而是執行需要大量記憶體的工作鏈結，資料準備可最佳化使用最有效率的工具，包括[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和[!INCLUDE[tsql](../../includes/tsql-md.md)]。 

以下是如何自動化您的資料處理的一些概念，以及使用的模型管線[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ 從中擷取資料在內部部署或雲端來建立定型資料的來源 
+ 建置並執行 R 或 Python 模型的資料整合工作流程
+ 重新定型模型，定期 （排程）
+ 從 R 或 Python 指令碼的結果載入到其他目的地，例如 Excel、 Power BI、 Oracle 和 Teradata 等等
+ 使用 SSIS 工作來建立 SQL database 中的資料特徵
+ 使用條件式分支切換 R 和 Python 作業的計算內容

## <a name="ssis-example"></a>SSIS 範例

下列範例是來自作者 Jimmy Wong 位於此 URL 現在已淘汰的 MSDN 部落格文章： `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

此範例會示範如何使用 SSIS 自動化工作。 您使用內嵌 R 中使用 SQL Server Management Studio，建立預存程序，並再執行這些預存程序[執行 T-SQL 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)SSIS 封裝中。

若要逐步執行此範例中，您應該熟悉如何使用 Management Studio、 SSIS、 SSIS 設計工具、 套件設計和 T-SQL。 SSIS 封裝會使用三個[執行 T-SQL 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)，插入資料表中的定型資料、 模型化資料，及評分資料，進而取得預測的輸出。

### <a name="load-training-data"></a>載入訓練資料

若要建立資料表來儲存資料的 SQL Server Management Studio 中執行下列指令碼。 您應該建立，並針對此練習中使用測試資料庫。 

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

建立載入資料框架中的定型資料的預存程序。 這個範例使用內建的鳶尾花資料集。 

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

在 SSIS 設計師中，建立[執行 SQL 」 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)執行您剛才定義的預存程序。 指令碼**SQLStatement**移除現有的資料，請指定要插入的資料，然後呼叫預存程序，以提供資料。

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![將資料插入](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "插入資料")

### <a name="generate-a-model"></a>產生模型

若要建立資料表的 SQL Server Management Studio 中執行下列指令碼儲存模型。 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

建立會產生線性模型，使用預存程序[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)。 RevoScaleR 和 revoscalepy 程式庫會自動出現在 SQL Server 上的 R 和 Python 工作階段，這樣就不需要匯入程式庫。

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

在 SSIS 設計師中，建立[執行 SQL 」 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)來執行**generate_iris_rx_model**預存程序。 模型會序列化並儲存到 ssis_iris_models 資料表。 指令碼**SQLStatement**如下所示：

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![會產生線性模型](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "會產生線性模型")

為檢查點，這項工作完成之後，您可以查詢以查看它包含一個二元模型 ssis_iris_models。

### <a name="predict-score-outcomes-using-the-trained-model"></a>預測 （分數） 使用 「 定型 」 模型的結果

已載入定型資料，並產生模型的程式碼之後，剩下的唯一步驟就使用模型來產生預測。 

若要這樣做，請將 R 指令碼放在觸發程序的 SQL 查詢[rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) ssis_iris_model 中內建的 R 函式。 呼叫預存程序**predict_species_length**完成此項工作。

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

在 SSIS 設計師中，建立[執行 SQL 」 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)執行**predict_species_length**預存程序來產生預測的花瓣長度。

```T-SQL
exec predict_species_length 'rxLinMod';
```

![產生預測](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "產生預測")

### <a name="run-the-solution"></a>執行解決方案

在 SSIS 設計師中，按下 f5 鍵來執行封裝。 您應該會看到類似下列螢幕擷取畫面的結果。

![F5 在偵錯模式中執行](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "F5 以偵錯模式執行")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>SSRS 用於視覺效果

雖然 R 可以建立圖表和有趣的視覺效果，並不完美整合與外部資料來源，這表示每個圖表或圖形有必須個別產生。 此外，可能也很難進行共用。

藉由使用[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，您可以透過 R 中執行複雜的作業[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序，由各種企業報告工具，包括可以輕鬆地取用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 Power BI。

### <a name="ssrs-example"></a>SSRS 範例

[R Graphics Device for Microsoft Reporting Services (SSRS) (英文)](https://rgraphicsdevice.codeplex.com/)

這個 CodePlex 專案提供的程式碼，可協助您建立自訂報表項目，做為映像，可用於呈現的 R 圖形輸出[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]報表。  透過使用自訂報表項目，您可以：

+ 將使用 R Graphics Device 建立的圖表和繪圖發佈到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 儀表板

+ 將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 參數傳遞給 R 繪圖

> [!NOTE]
> 此範例中，必須在 Reporting Services 伺服器上，以及在 Visual Studio 中安裝支援 R Graphics Device for Reporting Services 的程式碼。 此外，還需要手動編譯和設定。

## <a name="next-steps"></a>後續步驟

這篇文章中的 SSIS 和 SSRS 的範例說明兩種情況下，執行包含內嵌的 R 或 Python 指令碼的預存程序。 重點是，您可以將 R 或 Python 指令碼提供給任何應用程式或工具，可傳送預存程序的執行要求。 適用於 SSIS 的其他重點是，您可以建立封裝，自動化並排程包含作業的鏈結中的 R 或 Python 資料科學功能的各種不同的作業，例如資料取得、 清理、 操作和其他等等。 如需詳細資訊和想法，請參閱[在 SQL Server Machine Learning 服務中使用預存程序的實作 R 程式碼](operationalizing-your-r-code.md)。