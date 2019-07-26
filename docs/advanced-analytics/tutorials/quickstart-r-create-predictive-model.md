---
title: 使用 R 建立預測模型的快速入門
description: 在本快速入門中, 您將瞭解如何使用 SQL Server 資料來繪製預測, 以在 R 中建立模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 7de37b16c04cf2f972e36c11ba5dfb53721e6094
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469438"
---
# <a name="quickstart-create-a-predictive-model-using-r-in-sql-server"></a>快速入門：在 SQL Server 中使用 R 建立預測模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入門中, 您將瞭解如何使用 R 來定型模型, 然後將模型儲存至 SQL Server 中的資料表。 模型是簡單的一般化線性模型 (GLM), 可預測車輛已符合手動傳輸的機率。 您將使用 R `mtcars`隨附的資料集。

## <a name="prerequisites"></a>必要條件

先前的快速入門[中, 驗證 R 存在於 SQL Server 中](quickstart-r-verify.md), 提供設定本快速入門所需之 R 環境的相關資訊和連結。

## <a name="create-the-source-data"></a>建立來源資料

首先，建立資料表來儲存訓練資料。

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

接下來, 從 [資料集`mtcars`] 中的組建插入資料。

```SQL
INSERT INTO dbo.MTCars
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'MTCars <- mtcars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'MTCars';
```

+ 有些人喜歡使用臨時表, 但請注意, 有些 R 用戶端會中斷批次之間的會話連線。

+ R 執行階段隨附許多大大小小的資料集。 若要取得隨 R 一起安裝的資料集清單，請從 R 命令提示字元處，輸入 `library(help="datasets")`。

## <a name="create-a-model"></a>建立模型

汽車速度資料包含兩個數據行, 也就是`hp`數值、動力 (`wt`) 和權數 ()。 您將從這種資料建立一般化線性模型 (GLM), 以評估車輛已符合手動傳輸的機率。

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

+ 的第一個自`glm`變數是*公式*參數, 其`hp + wt`定義`am`為相依于。
+ 輸入資料儲存在變數 `MTCarsData` 中，會由 SQL 查詢填入。 如果您沒有為輸入資料指定特定的名稱，預設變數名稱將會是 _InputDataSet_。

## <a name="create-a-table-for-the-model"></a>建立模型的資料表

接下來, 儲存模型, 讓您可以重新定型或將它用於預測。 R 套件如果會建立模型，其輸出通常會是「二進位物件」。 因此, 您用來儲存模型的資料表必須提供**Varbinary (max)** 類型的資料行。

```sql
CREATE TABLE GLM_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
```

## <a name="save-the-model"></a>儲存模型

若要儲存模型，請執行下列 Transact-SQL 陳述式來呼叫預存程序、產生模型，然後將它儲存至資料表。

```sql
INSERT INTO GLM_models(model)
EXEC generate_GLM;
```

請注意, 如果您第二次執行此程式碼, 就會收到此錯誤:

```sql
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

有一個可避免發生此錯誤的選項，就是更新每個新模型的名稱。 例如，您可以將名稱變更成更具描述性且包含模型類型、模型建立日期等等的名稱。

```sql
UPDATE GLM_models
SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="next-steps"></a>後續步驟

既然您已有模型, 在最後一個快速入門中, 您將瞭解如何從它產生預測並繪製結果。

> [!div class="nextstepaction"]
> [入門從模型預測及繪製](quickstart-r-predict-from-model.md)