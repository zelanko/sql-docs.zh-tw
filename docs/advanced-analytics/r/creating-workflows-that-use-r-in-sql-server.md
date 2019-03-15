---
title: 使用 R-SQL Server Machine Learning 服務建立的 SSIS 和 SSRS 的工作流程
description: 結合 SQL Server 機器學習服務和 R Services、 Reporting Services (SSRS) 和 SQL Server Integration Services (SSIS) 的整合案例。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 76ddf3e3fdb43fea6bb8fd224f8199cda4134b64
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976298"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>使用 R 在 SQL Server 上建立 SSIS 和 SSRS 的工作流程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何使用結合關聯式資料，從 Microsoft R 程式庫的資料科學函式的方式在兩個重要的 SQL Server 功能，SQL Server Integration Services (SSIS) 和 SQL Server Reporting Services SSRS 中的預存程序和 BI 功能，來協調的資料轉換和視覺效果。 了解哪些功能的[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]擇資料科學解決方案。 這篇文章也會提醒您，程式碼和資料在 SQL Server，例如內嵌 R 程式碼，預存程序，輕鬆地取用中提供的視覺效果中[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。

## <a name="bring-compute-power-to-the-data"></a>為資料帶入計算能力

R 和 Python 與 SQL Server 整合的主要設計目標是要讓分析貼近資料。 這會提供多項優點：

+ 資料安全性。 接近 R 帶入的資料來源，可避免浪費資源或不安全的資料移動。
+ 速度。 資料庫已針對集合型操作進行最佳化。 最新的創新，例如記憶體中資料表的資料庫中進行摘要和彙總作業如閃電般，而且與資料科學完美互補。
+ 簡化部署和整合。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是許多其他資料管理工作和應用程式的作業中心點。 使用位於報表倉儲的資料庫中的資料，您可以確定機器學習服務解決方案所使用的資料是一致且最新狀態。 
+ 跨雲端和內部部署的效率。 您可以倚賴企業資料管線 (包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 Azure Data Factory)，而不以 R 處理資料。 透過 Power BI 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 很容易就能報告結果或分析。

資料科學家和開發人員可以使用正確的 SQL 和 R 組合，來進行不同的資料處理和分析工作，因此更有效率。

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-data-transformation-and-automation"></a>使用 SSIS 進行資料轉換和自動化

資料科學工作流程的互動性很高，並涉及許多資料的轉換，包括縮放、彙總、機率計算，以及重新命名與合併屬性。 資料科學家已習慣以 R、Python 或其他語言執行許多這些工作；不過，在企業資料上執行這類工作流程需要與 ETL 工具和程序的緊密整合。

由於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可讓您透過 Transact-SQL 和預存程序在 R 中執行複雜的作業，因此您連最小程度的重新開發工作都不需要，就能將 R 特定的工作與現有的 ETL 程序整合。 而是在 R 中執行需要大量記憶體的工作鏈結，資料準備可最佳化使用最有效率的工具，包括[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和[!INCLUDE[tsql](../../includes/tsql-md.md)]。 

以下是如何自動化您的資料處理的一些概念，以及使用的模型管線[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ 使用[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]工作，以在 SQL database 中建立必要的資料特徵
+ 使用條件式分支切換 R 工作的計算內容
+ 執行 R 作業，在資料庫中，產生自己的資料，並與應用程式共用該資料
+ 當使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，載入儲存在文字變數中的 R 指令碼，並在 SQL Server 中執行

## <a name="ssis-example"></a>SSIS 範例

下列範例是來自目前已停用 MSDN 部落格文章作者 Jimmy Wong 位於此 URL: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`。

此範例會示範如何使用 SSIS 自動化工作。 您使用內嵌 R 中使用 SQL Server Management Studio，建立預存程序，並再執行這些預存程序[執行 T-SQL 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)SSIS 封裝中。

若要逐步執行此範例中，您應該熟悉如何使用 Management Studio、 SSIS、 SSIS 設計工具、 套件設計和 T-SQL。 SSIS 封裝會使用三個[執行 T-SQL 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)，插入資料表中的定型資料、 模型化資料，及評分資料，進而取得預測的輸出。

### <a name="create-tables"></a>建立資料表

若要建立幾個資料表的 SQL Server Management Studio 中執行下列程式碼： 一個用來儲存資料，另一個要儲存模型。 Ssis_iris 資料表的角色是作為運算化案例中的定型資料。 

```T-SQL
Use irissql
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

### <a name="create-a-stored-procedure-that-loads-training-data"></a>建立預存程序，以載入訓練資料

此指令碼會建立載入資料框架中，使用內建的 R 資料集的鳶尾花的預存程序。

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

### <a name="define-an-execute-sql-task-that-refreshes-the-model"></a>定義重新整理模型的 「 執行 SQL 」 工作

在 SSIS 設計師中，建立[執行 SQL 」 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)。

![將資料插入](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "插入資料")

[Sqlstatement] 的指令碼如下所示。 指令碼中移除現有的資料，然後再重新載入新資料使用**load_iris**預存程序，您在上一個步驟中建立。

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

### <a name="create-a-stored-procedure-that-generates-a-model"></a>建立預存程序所產生的模型

這個預存程序是建立線性模型，使用程式碼[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)。 RevoScaleR 和 revoscalepy 程式庫會自動載入 SQL Server 上的 R 和 Python 工作階段中。

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

### <a name="define-an-execute-sql-task-that-runs-the-model-generation-stored-procedure"></a>定義 「 執行 SQL 」 工作執行模型產生的預存程序

在此步驟中，[執行 SQL 」 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)執行**generate_iris_rx_model**預存程序，建立模型，並將其插入至 ssis_iris_models 資料表。

![會產生線性模型](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "會產生線性模型")

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

這項工作完成之後，您可以查詢以查看它包含一個二元模型 ssis_iris_models。

### <a name="predict-score-outcomes-using-the-trained-model"></a>預測 （分數） 使用 「 定型 」 模型的結果

在此簡單範例中，假設會是該 ssis_iris_model 是定型的模型。 由於定型模型的目的是要產生預測，不過我們現在已準備好執行預測，使用它。 

若要這樣做，請將 R 指令碼放在觸發程序的 SQL 查詢[rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) ssis_iris_model 中內建的 R 函式。 SQL Server 中的預存程序稱為**predict_species_length**完成此項工作。

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

### <a name="define-an-execute-sql-task-that-predicts-outcomes"></a>定義執行 SQL 」 工作，可預測的結果

使用[執行 SQL 」 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)，執行**predict_species_length**預存程序來產生預測的花瓣長度。

![產生預測](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "產生預測")

```T-SQL
exec predict_species_length 'rxLinMod';
```

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