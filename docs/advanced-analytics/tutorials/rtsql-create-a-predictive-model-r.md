---
title: 若要建立預測模型，在 SQL Server Machine Learning 中使用 R 的快速入門 |Microsoft Docs
description: 在本快速入門，了解如何建置在 R 中使用 SQL Server 資料來繪製預測模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7ca2fcac5bef63a4abf2449b56c25a600b9255c3
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086820"
---
# <a name="quickstart-create-a-predictive-model-using-r-in-sql-server"></a>快速入門： 建立 SQL Server 中使用 R 的預測性模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入門中，您將了解如何使用 R 來定型模型，並再將模型儲存至 SQL Server 中的資料表。 此模型是一個簡單的迴歸模型，可根據速度預測汽車的停止距離。 您將使用`cars`隨附 R，因為它是小型且簡單易懂的資料集。

## <a name="prerequisites"></a>先決條件

先前的快速入門中， [Hello World R 與 SQL](rtsql-using-r-code-in-transact-sql-quickstart.md)，提供資訊並連結設定本快速入門所需的 R 環境。

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

+ 有些人喜歡使用暫存資料表，但請注意，有些 R 用戶端中斷連線工作階段之間的批次。

+ R 執行階段隨附許多大大小小的資料集。 若要取得隨 R 一起安裝的資料集清單，請從 R 命令提示字元處，輸入 `library(help="datasets")`。

## <a name="create-a-regression-model"></a>建立迴歸模型

汽車速度資料包含兩個資料行 `dist` 和 `speed` (都是數值資料行)。 某些速度有多個觀察值。 您將從這項資料建立線性迴歸模型，其中描述車速與停止車輛所需之距離間的關聯性。

線性模型的需求相當簡單：

+ 定義一個描述相依變數 `speed` 與獨立變數 `distance` 之間關聯性的公式

+ 提供要用於訓練模型的輸入資料

> [!TIP]
> 如果您需要複習一下線性模型，我們建議您使用本教學課程說明使用 rxlinmod 來將模型配適的程序：[契合線性模型](https://docs.microsoft.com/r-server/r/how-to-revoscaler-linear-model)

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

接下來，儲存模型，以便您可以重新定型或預測中使用它。 R 套件如果會建立模型，其輸出通常會是「二進位物件」。 因此，您儲存模型的資料表必須提供一個 **varbinary** 類型的資料行。

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

例如，假設您想要訓練模型，但要從該模型立即檢視係數資料表。 您可以將該係數資料表建立成主要結果集，然後以 SQL 變數輸出訓練過的模型。 您可以立即重複使用該模型藉由呼叫的變數，或您無法將模型儲存至資料表，如下所示。

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

請記住下列規則使用 SQL 參數和中的 R 變數`sp_execute_external_script`:

+ 中的名稱對應至 R 指令碼的所有 SQL 參數會都列出 _\@params_引數。
+ 其中一個參數的輸出，加入在 OUTPUT 關鍵字 _\@params_清單。
+ 之後列出對應的參數，提供對應，也就是一行一行地，SQL 參數與 R 變數，立即在後 _\@params_清單。

## <a name="next-steps"></a>後續步驟

現在，您就會以模型中，在最後的快速入門中，您將了解如何從它產生預測並繪製結果。

> [!div class="nextstepaction"]
> [快速入門： 從預測並繪製模型](../tutorials/rtsql-predict-and-plot-from-model.md)