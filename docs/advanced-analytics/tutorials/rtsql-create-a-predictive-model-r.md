---
title: 建立預測模型 (SQL 快速入門中的 R) |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3a56ddd95f0282550662cc559ff5a393d0bd236b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-predictive-model-r-in-sql-quickstart"></a>建立預測模型 (SQL 快速入門中的 R)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此步驟中，您將了解如何使用 R 來訓練模型，然後將該模型儲存至 SQL Server 中的資料表。 此模型是一個簡單的迴歸模型，可根據速度預測汽車的停止距離。 您將使用`cars`資料集包含使用 R，因為它是小型且容易理解。

## <a name="create-the-source-data"></a>建立來源資料

首先，建立資料表來儲存訓練資料。

```sql
CREATE TABLE CarSpeed ([speed] int not null, [distance] int not null)
INSERT INTO CarSpeed
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'car_speed <- cars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'car_speed'
```

+ 有些人喜歡使用暫存資料表，但請留意某些 R 用戶端中斷連接批次之間的工作階段。

+ R 執行階段隨附許多大大小小的資料集。 若要取得隨 R 一起安裝的資料集清單，請從 R 命令提示字元處，輸入 `library(help="datasets")`。

## <a name="create-a-regression-model"></a>建立迴歸模型

汽車速度資料包含兩個資料行 `dist` 和 `speed` (都是數值資料行)。 某些速度有多個觀察值。 您將從這項資料建立線性迴歸模型，其中描述車速與停止車輛所需之距離間的關聯性。

線性模型的需求相當簡單：

+ 定義一個描述相依變數 `speed` 與獨立變數 `distance` 之間關聯性的公式

+ 提供要用於訓練模型的輸入資料

> [!TIP]
> 如果您需要在線性模型上的重新整理程式，我們建議此教學課程，其中描述使用 rxLinMod 將模型配適的程序：[調整線性模型](https://docs.microsoft.com/r-server/r/how-to-revoscaler-linear-model)

若要實際建置該模型，您需在 R 程式碼中定義該公式，然後將資料當作輸入參數來傳遞。

```sql
DROP PROCEDURE IF EXISTS generate_linear_model;
GO
CREATE PROCEDURE generate_linear_model
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'lrmodel <- rxLinMod(formula = distance ~ speed, data = CarsData);
        trained_model <- data.frame(payload = as.raw(serialize(lrmodel, connection=NULL)));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model varbinary(max)));
END;
GO
```

+ rxLinMod 的第一個引數是 *formula* 參數，此參數將 distance 定義成與 speed 相依。
+ 輸入資料儲存在變數 `CarsData` 中，會由 SQL 查詢填入。 如果您沒有為輸入資料指定特定的名稱，預設變數名稱將會是 _InputDataSet_。

## <a name="create-a-table-for-storing-the-model"></a>建立用以儲存模型的資料表

接下來，儲存模型，所以您可以重新定型，或用於預測。 R 套件如果會建立模型，其輸出通常會是「二進位物件」。 因此，您儲存模型的資料表必須提供一個 **varbinary** 類型的資料行。

```sql
CREATE TABLE stopping_distance_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null);
```

## <a name="save-the-model"></a>儲存模型

若要儲存模型，請執行下列 Transact-SQL 陳述式來呼叫預存程序、產生模型，然後將它儲存至資料表。

```sql
INSERT INTO stopping_distance_models (model)
EXEC generate_linear_model;
```

請注意，是否第二次執行此程式碼，您會收到這個錯誤：

```
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

有一個可避免發生此錯誤的選項，就是更新每個新模型的名稱。 例如，您可以將名稱變更成更具描述性且包含模型類型、模型建立日期等等的名稱。

```sql
UPDATE stopping_distance_models
SET model_name = 'rxLinMod ' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="output-additional-variables"></a>輸出其他變數

一般而言，來自預存程序 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的 R 輸出會限制為單一資料框架。 (未來可能會移除這項限制)。

不過，除了資料框架之外，您還可以傳回其他類型 (例如純量) 的輸出。

例如，假設您想要訓練模型，但要從該模型立即檢視係數資料表。 您可以將該係數資料表建立成主要結果集，然後以 SQL 變數輸出訓練過的模型。 您無法立即重新使用模型，透過呼叫變數，或您無法將模型儲存至資料表，如下所示。

```sql
DECLARE @model varbinary(max), @modelname varchar(30)
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
        speedmodel <- rxLinMod(distance ~ speed, CarsData)
        modelbin <- serialize(speedmodel, NULL)
        OutputDataSet <- data.frame(coefficients(speedmodel));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @params = N'@modelbin varbinary(max) OUTPUT'
    , @modelbin = @model OUTPUT
    WITH RESULT SETS (([Coefficient] float not null));

-- Save the generated model
INSERT INTO [dbo].[stopping_distance_models] (model_name, model)
VALUES ('latest model', @model)
```

**結果**

![rslq_basictut_coefficients](media/rslq-basictut-coefficients.PNG)

### <a name="summary"></a>摘要

請記住這些規則使用的 SQL 參數與 R 變數中的`sp_execute_external_script`:

+ 名稱中所有的 SQL 參數對應至 R 指令碼會列出_@params_引數。
+ 若要輸出這其中一個參數，請在 _@params_ 清單中新增 OUTPUT 關鍵字。
+ 列出對應的參數之後，請緊接在 _@params_ 清單之後，逐行提供 SQL 參數與 R 變數的對應。

## <a name="next-lesson"></a>下一課

既然您已有模型，您將了解如何從該模型產生預測並繪製結果。

[從模型預測及繪製](../tutorials/rtsql-predict-and-plot-from-model.md)


