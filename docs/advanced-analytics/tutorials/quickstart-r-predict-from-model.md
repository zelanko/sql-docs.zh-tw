---
title: 使用 R 從模型預測的快速入門
description: 在本快速入門中, 您將瞭解如何在 R 中使用預先建立的模型, 並 SQL Server 資料進行計分。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4058725227deea1f6755c8e6272265ecdf91e59c
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714783"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>快速入門：在 SQL Server 中使用 R 從模型預測
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入門中, 使用您在先前的快速入門中建立的模型, 對新資料進行預測評分。 若要使用新資料執行_計分_, 請從資料表中取得其中一個定型模型, 然後呼叫一組新的資料來做為預測基礎。 「計分」 (data 科學) 一詞有時會用來表示根據送入定型模型中的新資料來產生預測、機率或其他值。

## <a name="prerequisites"></a>先決條件

本快速入門是[建立預測模型](quickstart-r-create-predictive-model.md)的延伸模組。

## <a name="create-the-table-of-new-data"></a>建立新資料的資料表

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

## <a name="predict-manual-transmission"></a>預測手動傳輸

現在, 您`dbo.GLM_models`的資料表可能包含多個 R 模型, 全都使用不同的參數或演算法來建立, 或在不同的資料子集上進行定型。

若要根據一個特定模型取得預測, 您必須撰寫一個可執行下列動作的 SQL 腳本:

1. 取得您所需的模型
2. 取得新的輸入資料
3. 呼叫與該模型相容的 R 預測函數

在此範例中, 我們將使用名為`default model`的模型。

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

+ 使用 SELECT 陳述式，從資料表取得單一模型，並傳遞它做為輸入參數。

+ 從資料表擷取模型之後，在模型上呼叫 `unserialize` 函數。

+ 搭配適當引數將 `predict` 函數套用至模型，並提供新的輸入資料。

+ 在此範例中, `str`會在測試階段加入函式, 以檢查從 R 傳回的資料架構。您稍後可以移除此語句。

+ R 腳本中使用的資料行名稱不一定會傳遞至預存程式輸出。 在這裡, 我們使用 WITH RESULTS 子句來定義一些新的資料行名稱。

**結果**

![用於預測手動傳輸 properbility 的結果集](./media/r-predict-am-resultset.png)

您也可以使用[transact-sql 中的 PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) , 根據預存模型產生預測值或分數。

## <a name="next-steps"></a>後續步驟

R 與 SQL Server 的整合，讓您能夠更輕鬆地大規模部署 R 方案，運用 R 和關聯式資料庫的最佳功能，以進行高效能的資料處理和快速的 R 分析。 

透過 Microsoft 資料科學和 R 服務開發小組所建立的端對端案例, 繼續瞭解使用 R 搭配 SQL Server 的解決方案。

> [!div class="nextstepaction"]
> [SQL Server R 教學課程](sql-server-r-tutorials.md)
