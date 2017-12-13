---
title: "在 Azure SQL Database 中使用 R |Microsoft 文件"
ms.custom: 
ms.date: 12/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: cb43b2c1edb6ce03acd2e3e64eb077ca96c62304
ms.sourcegitcommit: 05e2814fac4d308196b84f1f0fbac6755e8ef876
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/12/2017
---
# <a name="using-r-in-azure-sql-database"></a>在 Azure SQL Database 中使用 R

在年 10 月 2017，SQL Server 開發團隊宣布計劃，以支援執行 R 程式碼中的資料庫使用預存程序，類似於 SQL Server 2016 中的 R Services。 

若要保持最新的公開發行排程和即將發生的事件，請參閱[SQL Server 部落格](https://blogs.technet.microsoft.com/dataplatforminsider/)或[Microsoft R Server 部落格](https://blogs.msdn.microsoft.com/rserver/)。

> [!IMPORTANT]
> 目前的 R 支援預覽僅提供在美國西部 Azure SQL Database，和功能都會受到限制 R 的功能相比，Python 程式碼，在 SQL Server 2016 或 2017年中的執行。

## <a name="whats-included"></a>包含的內容

在下列資料庫服務層和效能層級上可用的資料庫中的 R 功能：
 
- Premium 服務層 – P1、 P2、 P4、 P6、 P11、 P15
- Premium RS 服務層 – PRS1，PRS2，PRS4，PRS6
- 進階彈性集區-125 Edtu 或更新版本
- Premium RS 彈性集區-125 Edtu 或更新版本

這些套件包含預覽版本：

+   Microsoft R Open 與 R 版本 3.3.3
+   基底 R 封裝和函數是預先安裝
+   Microsoft R Server 9.2 包括 RevoScaleR 封裝

在目前的預覽版本中，您可以執行下列工作：

+ 使用適合放入記憶體中的任何資料模型的定型集
+   使用適合放入記憶體中的任何資料模型的計分
+   執行 R 指令碼的一般平行處理原則 (使用@parallelsp_execute_external_script 參數)
+   資料流執行 R 指令碼執行 (使用@r_RowsPerReadsp_execute_external_script 參數)
+   一次執行單一的 R 指令碼


在預覽版本的 R Azure SQL Database 上不支援下列工作：

+ 您無法啟用特定資料庫上的執行 R 指令碼。
+ Dmv 提供給監視 CPU 和記憶體使用量的 R 指令碼則無法使用。
+ 可以不安裝任何第三方封裝。 不支援建立外部程式庫陳述式。

## <a name="example"></a>範例

在 Azure SQL DB 中，所有 R 命令使用從都執行 T-SQL，預存程序[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。 

下列範例示範如何試用預覽功能，使用隨附於基底 r 光圈資料集

### <a name="step-1-create-the-data-tables"></a>步驟 1： 建立資料的資料表

開始建立兩個資料表： 一個用來儲存從 R，擷取的來源資料，另一個用於儲存已定型的模型。

```sql
DROP TABLE IF EXISTS iris_data, iris_models;
GO
CREATE TABLE iris_data (
        id INT NOT NULL IDENTITY PRIMARY KEY
        , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
        , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
        , "Species" VARCHAR(100) NULL
);
CREATE TABLE iris_models (
    model_name VARCHAR(30) NOT NULL PRIMARY KEY,
    model VARBINARY(max) NOT NULL,
    native_model VARBINARY(MAX) NOT NULL
);
GO
```

### <a name="step-2-populate-table-with-data-from-the-iris-dataset"></a>步驟 2： 擴展資料表光圈資料集的資料

在建立資料表之後，執行下列程式碼插入資料表中的定型資料。 預存程序 sp_execute_external_script 呼叫 R，並傳回成為資料框架，使用 INSERT INTO 陳述式中指定的結構描述的光圈資料集。

```sql
INSERT INTO iris_data
("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
EXEC sp_execute_external_script @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

### <a name="step-3-create-the-stored-procedure-that-generates-the-model"></a>步驟 3： 建立會產生模型的預存程序

下列預存程序會實際建立並定型模型，可以在兩種二進位格式儲存的工作。

```sql
CREATE PROCEDURE generate_iris_model (@trained_model VARBINARY(MAX) OUTPUT, @native_trained_model VARBINARY(MAX) OUTPUT
AS
BEGIN
  EXEC sp_execute_external_script @language = N'R'
    , @script = N'
    iris_model <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris_rx_data);
    trained_model <- as.raw(serialize(iris_model, connection=NULL));
    native_trained_model <- rxSerializeModel(iris_model, realtimeScoringOnly = TRUE)
    '
  , @input_data_1 = N'SELECT "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@trained_model VARBINARY(MAX) OUTPUT, @native_trained_model VARBINARY(MAX) OUTPUT'
    , @trained_model = @trained_model OUTPUT
```

+ **輸出**關鍵字的輸入參數表示值應該透過傳遞，而且用於以及輸出。
+ 行首`iris_model`定義決策樹模型來預測指定根據花屬性。
+ 若要呼叫`serialize`儲存適用於 SQL Server 中的儲存體的一種二進位格式中的模型。 
+ 或者，使用 RevoScaleR 演算法為基礎的模型，您可以使用[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)函式，將模型儲存在新的原生二進位格式。 以此格式儲存的模型可以載入計分與 SQL Server 中的預測函式。

### <a name="step-4-train-and-save-the-model"></a>步驟 4： 訓練和儲存模型

一旦建立預存程序，呼叫以處理輸入的資料，並建立模型。 下列程式碼也會將模型儲存至資料表**iris_models**，如此一來，您可以使用它稍後要預測的花牌指定。

```sql
DECLARE @model VARBINARY(MAX), @native_modelVARBINARY(MAX);
EXEC generate_iris_model @model OUTPUT, @native_model OUTPUT;
DELETE FROM iris_models WHERE model_name = 'iris.dtree';
INSERT INTO iris_models (model_name, model, native_model) VALUES('iris.dtree', @model, @native_model);
SELECT model_name, datalength(model)/1024. AS model_size_kb, datalength(native_model)/1024. AS native_model_size_kb FROM iris_models;
GO
```

### <a name="step-5-create-a-stored-procedure-for-scoring"></a>步驟 5： 建立預存程序進行評分

接下來，建立計分的預存程序。 這個預存程序會從資料表中，載入指定的模型，並建立根據輸入資料的分數。

```sql
CREATE PROCEDURE predict_iris_species (@model varchar(100))
AS
BEGIN
  DECLARE @rx_model VARBINARY(MAX) = (SELECT model FROM iris_models WHERE model_name = @model);
  EXEC sp_execute_external_script @language = N'R'
  , @script = N'
    irismodel<-unserialize(rx_model);
    OutputDataSet <-rxPredict(irismodel, iris_rx_data, extraVarsToWrite = c("Species", "id"));
      '
  , @input_data_1 = N'SELECT "id", "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@rx_model varbinary(max)'
  , @rx_model = @rx_model
  WITH RESULT SETS ( ("setosa_Pred" FLOAT, "versicolor_Pred" FLOAT, "virginica_Pred" FLOAT, "Species.Actual" VARCHAR(100), "id" INT));
END;
GO
```

這個預存程序會使用[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)函式，但您也可以使用原生的預測函式在 T-SQL 中所示[這裡](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-general-availability-of-native-scoring-using-predict-function-in-azure-sql-database/)。 使用預測函式會要求您使用[ **rx**模型](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler)並儲存在模型中使用[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)。

### <a name="step-6-use-the-stored-procedure-to-generate-predictions"></a>步驟 6： 使用預存程序來產生預測

若要從模型產生分數，請執行預存程序。 您可以將值插入資料表，或返回呼叫的應用程式中的預測。

```sql
EXEC predict_iris_species 'iris.dtree';
GO
```

## <a name="related-resources"></a>相關資源

Azure Marketplace 中也提供包含 SQL Server 2017 的多部虛擬機器：

+ [佈建虛擬機器上 Azure 機器學習](provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

也請查看這些各種常用的機器學習工具隨附預先設定的 Vm:

+ [資料科學虛擬機器](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)
+ [深入學習虛擬機器](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)

