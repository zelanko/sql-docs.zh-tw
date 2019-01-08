---
title: 若要從模型中使用 R-SQL Server 機器學習服務預測的快速入門
description: 在此快速入門中，了解評分使用 R 和 SQL Server 資料中的預先建置的模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 7175b99eb20710f5dd08689bd055d3a4ec93ae92
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046809"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>快速入門：從 SQL Server 中使用 R 的模型預測
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入門中，使用您在要評分新資料的預測先前的快速入門中建立的模型。 若要執行_評分_使用新的資料，從資料表取得其中一個定型模型，然後呼叫 一組新的資料上要做預測。 計分是有時會用於表示產生預測、 機率或其他值根據送入定型模型的新資料的資料科學的詞彙。

## <a name="prerequisites"></a>先決條件

本快速入門是擴充功能[建立預測模型](quickstart-r-create-predictive-model.md)。

## <a name="create-the-table-of-new-data"></a>建立新的資料的資料表

首先，建立新資料的資料表。 

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

到目前為止，您`dbo.GLM_models`資料表可能包含多個 R 模型，所有已建置使用不同的參數或演算法，或定型資料的不同子集。

若要取得一個特定的模型為基礎的預測，您必須撰寫會執行下列 SQL 指令碼：

1. 取得您所需的模型
2. 取得新的輸入資料
3. 呼叫與該模型相容的 R 預測函數

在此範例中，我們將使用名為模型`default model`。

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

上述指令碼會執行下列步驟：

+ 使用 SELECT 陳述式，從資料表取得單一模型，並傳遞它做為輸入參數。

+ 從資料表擷取模型之後，在模型上呼叫 `unserialize` 函數。

+ 搭配適當引數將 `predict` 函數套用至模型，並提供新的輸入資料。

+ 在範例中，`str`函式會加入在測試階段中，若要檢查從 r 傳回的資料結構描述您可以移除之後的陳述式。

+ R 指令碼中使用的資料行名稱不一定會傳遞至預存程序的輸出。 這裡我們使用 WITH RESULTS 子句來定義一些新的資料行名稱。

**結果**

![結果集，可預測的手動傳輸 properbility](./media/r-predict-am-resultset.png)

您也可使用[在 TRANSACT-SQL 中的 PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)來產生預測的值，或者以預存模型為基礎的分數。

## <a name="next-steps"></a>後續步驟

R 與 SQL Server 的整合，讓您能夠更輕鬆地大規模部署 R 方案，運用 R 和關聯式資料庫的最佳功能，以進行高效能的資料處理和快速的 R 分析。 

繼續了解使用 SQL Server 中的 R，透過 Microsoft 資料科學和 R 服務的開發團隊所建立的端對端案例的解決方案。

> [!div class="nextstepaction"]
> [SQL Server R 教學課程](sql-server-r-tutorials.md)
