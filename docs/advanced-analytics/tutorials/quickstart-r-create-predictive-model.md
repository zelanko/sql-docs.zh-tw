---
title: 若要建立預測模型，使用 R-SQL Server Machine Learning 的快速入門
description: 在本快速入門，了解如何建置在 R 中使用 SQL Server 資料來繪製預測模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 278eba1189b376b57f2dec7249a378832c18095c
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046754"
---
# <a name="quickstart-create-a-predictive-model-using-r-in-sql-server"></a>快速入門：建立預測模型，在 SQL Server 中使用 R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入門中，您將了解如何使用 R 來定型模型，並再將模型儲存至 SQL Server 中的資料表。 模型是簡單的廣義線性模型 (GLM)，可預測車輛手動傳輸，已調整大小的機率。 您將使用`mtcars`隨附 r 的資料集

## <a name="prerequisites"></a>先決條件

先前的快速入門中，[確認 R 存在於 SQL Server](quickstart-r-verify.md)，提供資訊並連結設定本快速入門所需的 R 環境。

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

接下來，將資料從資料集建置為插入`mtcars`。

```SQL
INSERT INTO dbo.MTCars
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'MTCars <- mtcars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'MTCars';
```

+ 有些人喜歡使用暫存資料表，但請注意，有些 R 用戶端中斷連線工作階段之間的批次。

+ R 執行階段隨附許多大大小小的資料集。 若要取得隨 R 一起安裝的資料集清單，請從 R 命令提示字元處，輸入 `library(help="datasets")`。

## <a name="create-a-model"></a>建立模型

汽車速度資料包含兩個資料行，這兩個數值、 馬力 (`hp`) 和重量 (`wt`)。 從這項資料，您將建立廣義線性模型 (GLM) 估計手動傳輸的一種工具，已納入的機率。

若要建立模型，您 R 程式碼內部定義的公式，並傳遞做為輸入參數的資料。

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

+ 第一個引數`glm`已*公式*參數，定義`am`為相依於`hp + wt`。
+ 輸入資料儲存在變數 `MTCarsData` 中，會由 SQL 查詢填入。 如果您沒有為輸入資料指定特定的名稱，預設變數名稱將會是 _InputDataSet_。

## <a name="create-a-table-for-the-model"></a>建立模型的資料表

接下來，儲存模型，以便您可以重新定型或預測中使用它。 R 套件如果會建立模型，其輸出通常會是「二進位物件」。 因此，將模型儲存的資料表必須提供的資料行**varbinary （max)** 型別。

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

請注意，是否第二次執行此程式碼，您會收到這個錯誤：

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

現在，您就會以模型中，在最後的快速入門中，您將了解如何從它產生預測並繪製結果。

> [!div class="nextstepaction"]
> [快速入門：從模型預測並繪製](quickstart-r-predict-from-model.md)