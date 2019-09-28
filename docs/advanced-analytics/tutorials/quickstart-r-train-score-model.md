---
title: 在 R 中建立預測模型並為其評分
titleSuffix: SQL Server Machine Learning Services
description: 使用 SQL Server Machine Learning 服務在 R 中建立簡單的預測模型，然後使用新的資料來預測結果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5aad027f84bc1116aa57c6b0bc0d7b0893519c36
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/20/2019
ms.locfileid: "71150331"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-server-machine-learning-services"></a>快速入門：使用 SQL Server Machine Learning 服務在 R 中建立預測模型並為其評分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入門中，您將使用 R 建立和定型預測模型、將模型儲存至 SQL Server 實例中的資料表，然後使用模型，利用[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)來預測新資料中的值。

您將在本快速入門中使用的模型是一個簡單的一般化線性模型（GLM），可預測車輛已符合手動傳輸的機率。 您將使用 R 隨附的**mtcars**資料集。

> [!TIP]
> 如果您需要對線性模型進行重新整理程式，請嘗試此教學課程，其中描述使用 rxLinMod 來調整模型的程式：[調整線性模型 (英文)](/machine-learning-server/r/how-to-revoscaler-linear-model)

## <a name="prerequisites"></a>必要條件

- 本快速入門需要使用已安裝 R 語言的[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)，來存取 SQL Server 的實例。

  您的 SQL Server 實例可以位於 Azure 虛擬機器或內部部署中。 請注意，預設會停用外部腳本功能，因此您可能需要[啟用外部腳本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)，並在開始之前確認**SQL Server Launchpad 服務**正在執行。

- 您也需要工具來執行包含 R 腳本的 SQL 查詢。 您可以使用任何資料庫管理或查詢工具來執行這些腳本，只要它可以連接到 SQL Server 實例，並執行 T-SQL 查詢或預存程式即可。 本快速入門使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="create-the-model"></a>建立模型

若要建立模型，您將建立用於定型的來源資料、建立模型並使用資料進行定型，然後將模型儲存在 SQL 資料庫中，以便用來產生含有新資料的預測。

### <a name="create-the-source-data"></a>建立來源資料

1. 開啟**SQL Server Management Studio** ，並連接到您的 SQL Server 實例。

1. 建立用來儲存定型資料的資料表。

   ```sql
   CREATE TABLE dbo.MTCars(
       mpg decimal(10, 1) NOT NULL,
       cyl int NOT NULL,
       disp decimal(10, 1) NOT NULL,
       hp int NOT NULL,
       drat decimal(10, 2) NOT NULL,
       wt decimal(10, 3) NOT NULL,
       qsec decimal(10, 2) NOT NULL,
       vs int NOT NULL,
       am int NOT NULL,
       gear int NOT NULL,
       carb int NOT NULL
   );
   ```

1. 插入內建資料集`mtcars`的資料。

   ```SQL
   INSERT INTO dbo.MTCars
   EXEC sp_execute_external_script @language = N'R'
       , @script = N'MTCars <- mtcars;'
       , @input_data_1 = N''
       , @output_data_1_name = N'MTCars';
   ```

   > [!TIP]
   > R 執行階段隨附許多大大小小的資料集。 若要取得隨 r 安裝的資料集清單， `library(help="datasets")`請從 r 命令提示字元輸入。

### <a name="create-and-train-the-model"></a>建立和定型模型

汽車速度資料包含兩個數據行，也就是`hp`數值：動力（`wt`）和權數（）。 您將從這種資料建立一般化線性模型（GLM），以評估車輛已符合手動傳輸的機率。

若要建立模型, 請在您的 R 程式碼內定義公式, 並將資料當做輸入參數傳遞。

```sql
DROP PROCEDURE IF EXISTS generate_GLM;
GO
CREATE PROCEDURE generate_GLM
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'carsModel <- glm(formula = am ~ hp + wt, data = MTCarsData, family = binomial);
        trained_model <- data.frame(payload = as.raw(serialize(carsModel, connection=NULL)));'
    , @input_data_1 = N'SELECT hp, wt, am FROM MTCars'
    , @input_data_1_name = N'MTCarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model VARBINARY(max)));
END;
GO
```

- 的第一個自`glm`變數是*公式*參數, 其`hp + wt`定義`am`為相依于。
- 輸入資料儲存在變數 `MTCarsData` 中，會由 SQL 查詢填入。 如果您沒有為輸入資料指定特定的名稱，預設變數名稱將會是 _InputDataSet_。

### <a name="store-the-model-in-the-sql-database"></a>將模型儲存在 SQL 資料庫中

接下來，將模型儲存在 SQL 資料庫中，讓您可以使用它來進行預測或重新定型。 

1. 建立用來儲存模型的資料表。

   建立模型的 R 套件輸出通常是二進位物件。 因此, 您用來儲存模型的資料表必須提供**Varbinary (max)** 類型的資料行。

   ```sql
   CREATE TABLE GLM_models (
       model_name varchar(30) not null default('default model') primary key,
       model varbinary(max) not null
   );
   ```

1. 執行下列 Transact-sql 語句來呼叫預存程式、產生模型，並將它儲存至您所建立的資料表。

   ```sql
   INSERT INTO GLM_models(model)
   EXEC generate_GLM;
   ```

   > [!TIP]
   > 如果您第二次執行此程式碼，就會收到此錯誤：「違反 PRIMARY KEY 條件約束 ...無法在物件 dbo. stopping_distance_models 中插入重複的索引鍵。 有一個可避免發生此錯誤的選項，就是更新每個新模型的名稱。 例如，您可以將名稱變更成更具描述性且包含模型類型、模型建立日期等等的名稱。

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>使用定型的模型為新資料評分

「*計分*」是一種用於資料科學的詞彙，表示根據送至定型模型的新資料來產生預測、機率或其他值。 您將使用您在上一節中建立的模型，對新資料進行預測評分。

### <a name="create-a-table-of-new-data"></a>建立新資料的資料表

首先, 建立含有新資料的資料表。

```sql
CREATE TABLE dbo.NewMTCars(
    hp INT NOT NULL
    , wt DECIMAL(10,3) NOT NULL
    , am INT NULL
)
GO

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (110, 2.634)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (72, 3.435)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (220, 5.220)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (120, 2.800)
GO
```

### <a name="predict-manual-transmission"></a>預測手動傳輸

若要取得以您的模型為基礎的預測，請撰寫可執行下列動作的 SQL 腳本：

1. 取得您所需的模型
1. 取得新的輸入資料
1. 呼叫與該模型相容的 R 預測函數

一段時間之後，資料表可能會包含多個 R 模型、使用不同的參數或演算法來建立，或在不同的資料子集上進行定型。 在此範例中，我們將使用名為`default model`的模型。

```sql
DECLARE @glmmodel varbinary(max) = 
    (SELECT model FROM dbo.GLM_models WHERE model_name = 'default model');

EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(glmmodel));
            new <- data.frame(NewMTCars);
            predicted.am <- predict(current_model, new, type = "response");
            str(predicted.am);
            OutputDataSet <- cbind(new, predicted.am);
            '
    , @input_data_1 = N'SELECT hp, wt FROM dbo.NewMTCars'
    , @input_data_1_name = N'NewMTCars'
    , @params = N'@glmmodel varbinary(max)'
    , @glmmodel = @glmmodel
WITH RESULT SETS ((new_hp INT, new_wt DECIMAL(10,3), predicted_am DECIMAL(10,3)));
```

上述腳本會執行下列步驟:

- 使用 SELECT 陳述式，從資料表取得單一模型，並傳遞它做為輸入參數。

- 從資料表擷取模型之後，在模型上呼叫 `unserialize` 函數。

- 搭配適當引數將 `predict` 函數套用至模型，並提供新的輸入資料。

> [!NOTE]
> 在此範例中, `str`會在測試階段加入函式, 以檢查從 R 傳回的資料架構。您稍後可以移除此語句。
>
> R 腳本中使用的資料行名稱不一定會傳遞至預存程式輸出。 這裡使用 WITH RESULTS 子句來定義一些新的資料行名稱。

**結果**

![用於預測手動傳輸 properbility 的結果集](./media/r-predict-am-resultset.png)

您也可以使用[PREDICT （transact-sql）](../../t-sql/queries/predict-transact-sql.md)語句，根據預存模型產生預測值或分數。

## <a name="next-steps"></a>後續步驟

若要瞭解如何在 SQL Server 中處理 R 資料類型，請遵循此快速入門：

> [!div class="nextstepaction"]
> [在 SQL Server Machine Learning 服務中使用 R 處理資料類型和物件](quickstart-r-data-types-and-objects.md)

如需 SQL Server Machine Learning 服務的詳細資訊，請參閱下列文章。

- [使用 SQL Server Machine Learning 服務撰寫 advanced R 函數](quickstart-r-functions.md)
- [什麼是 SQL Server Machine Learning 服務（Python 和 R）？](../what-is-sql-server-machine-learning.md)
