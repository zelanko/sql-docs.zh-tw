---
description: PREDICT (Transact-SQL)
title: PREDICT (Transact-SQL)
titleSuffix: SQL machine learning
ms.custom: ''
ms.date: 06/26/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||>=azure-sqldw-latest'
ms.openlocfilehash: 83205b4a11be46888f8c7da8f29c84494d012740
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460851"
---
# <a name="predict-transact-sql"></a>PREDICT (Transact-SQL)

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

根據預存模型產生預測值或分數。 如需詳細資訊，請參閱[使用 PREDICT T-SQL 函式進行原生評分](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)。

## <a name="syntax"></a>語法

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current"

```syntaxsql
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>
  [, RUNTIME = ONNX ]
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

MODEL = @model | model_literal  
```

::: moniker-end

::: moniker range=">=azure-sqldw-latest"

```syntaxsql
PREDICT  
(  
  MODEL = <model_object>,
  DATA = object AS <table_alias>
  [, RUNTIME = ONNX ]
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

<model_object> ::=
  {
    model_literal
    | model_variable
    | ( scalar_subquery )
  }
```

::: moniker-end

### <a name="arguments"></a>引數

**MODEL**

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017"
`MODEL` 參數用來指定用於計分或預測的模型。 模型指定為變數、常值或純量運算式。

`PREDICT` 支援使用 [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) 和 [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) 套件進行定型的模型。
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
`MODEL` 參數用來指定用於計分或預測的模型。 模型指定為變數、常值或純量運算式。

在 Azure SQL 受控執行個體中，`PREDICT` 支援具有 [Open Neural Network Exchange (ONNX)](https://onnx.ai/get-started.html) \(英文\) 格式的模型，或是使用 [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) 和 [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) 套件進行定型的模型。
::: moniker-end

::: moniker range=">=azure-sqldw-latest"
`MODEL` 參數用來指定用於計分或預測的模型。 此模型會指定為變數、常值、純量運算式或純量子查詢。

在 Azure Synapse Analytics 中，`PREDICT` 支援具有 [Open Neural Network Exchange (ONNX)](https://onnx.ai/get-started.html) \(英文\) 格式的模型。
::: moniker-end

**資料**

DATA 參數用來指定用於計分或預測的資料。 資料是以查詢中的資料表來源形式指定。 資料表來源可以是資料表、資料表別名、CTE 別名、檢視或資料表值函數。

**RUNTIME = ONNX**

> [!IMPORTANT]
> `RUNTIME = ONNX` 引數僅在 [Azure SQL 受控執行個體](/azure/azure-sql/managed-instance/machine-learning-services-overview)、[Azure SQL Edge](/azure/sql-database-edge/onnx-overview)，以及 [Azure Synapse Analytics](/azure/synapse-analytics/overview-what-is) 中提供。

指出機器學習引擎是用於模型執行。 `RUNTIME` 參數值一律是 `ONNX`。 該參數為 Azure SQL Edge 與 Azure Synapse Analytics 的必要項目。 在 Azure SQL 受控執行個體上，該參數為選擇性，且只會在使用 ONNX 模型時使用。

**WITH ( <result_set_definition> )**

WITH 子句用來指定 `PREDICT` 函數傳回之輸出的結構描述。

除了 `PREDICT` 函數傳回的資料行本身，屬於資料輸入的所有資料行都可在查詢中使用。

### <a name="return-values"></a>傳回值

沒有預先定義的結構描述可用；模型的內容不會驗證，且傳回的資料行值也不會驗證。

- `PREDICT` 函數會傳入資料行做為輸入。
- `PREDICT` 函數也會產生新的資料行，但資料行數目和資料類型取決於用於預測的模型類型。

與模型相關聯的基礎預測函數，會傳回與資料、模型或資料行格式相關的任何錯誤訊息。

::: moniker range=">=sql-server-2017||>=sql-server-linux-2017"
## <a name="remarks"></a>備註

Windows 和 Linux 上所有版本的 SQL Server 2017 和更新版本都支援 `PREDICT` 函式。 並不需要啟用[機器學習服務](../../machine-learning/sql-server-machine-learning-services.md)以使用 `PREDICT`。
::: moniker-end

### <a name="supported-algorithms"></a>支援的演算法

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017"
您使用的模型必須使用 [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) 或 [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) 套件中其中一種支援的演算法建立。 如需目前所支援模型的清單，請參閱[使用 PREDICT T-SQL 函式進行原生評分](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)。
::: moniker-end
::: moniker range="=azure-sqldw-latest"
支援可轉換為 [ONNX](https://onnx.ai/) \(英文\) 模型格式的演算法。
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
支援可轉換為 [ONNX](https://onnx.ai/) \(英文\) 模型格式的演算法，以及使用 [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) 或 [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) 套件中其中一種支援的演算法所建立的模型。 如需 RevoScaleR 和 revoscalepy 中目前所支援演算法的清單，請參閱[使用 PREDICT T-SQL 函式進行原生評分](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)。
::: moniker-end

### <a name="permissions"></a>權限

`PREDICT` 不需要任何權限，不過，使用者需要資料庫的 `EXECUTE` 權限和查詢做為輸入之任何資料的權限。 如果模型儲存在資料表中，使用者也必須能夠從資料表讀取模型。

## <a name="examples"></a>範例

下列範例示範呼叫 `PREDICT` 的語法。

### <a name="using-predict-in-a-from-clause"></a>在 FROM 子句中使用 PREDICT

此範例在 `SELECT` 陳述式的 `FROM` 子句中參考 `PREDICT` 函數：

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current"

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @model,
    DATA = dbo.mytable AS d) WITH (Score FLOAT) AS p;
```

:::moniker-end

::: moniker range=">=azure-sqldw-latest"

```sql
DECLARE @model VARBINARY(max) = (SELECT test_model FROM scoring_model WHERE model_id = 1);

SELECT d.*, p.Score
FROM PREDICT(MODEL = @model,
    DATA = dbo.mytable AS d, RUNTIME = ONNX) WITH (Score FLOAT) AS p;
```

::: moniker-end

`DATA` 參數中為資料表來源指定的別名 **d** 是用來參考屬於 `dbo.mytable` 的資料行。 為 `PREDICT` 函式指定的別名 **p** 是用來參考 `PREDICT` 函式所傳回的資料行。

- 模型會以 `varbinary(max)` 資料行的形式儲存在名為 **Models** 的資料表中。 如 **識別碼** 和 **描述** 的其他資訊會儲存在資料表中以識別模式。
- `DATA` 參數中為資料表來源指定的別名 **d** 是用來參考屬於 `dbo.mytable` 的資料行。 輸入資料資料行應該要符合模型的輸入名稱。
- 為 `PREDICT` 函式指定的別名 **p** 是用來參考 `PREDICT` 函式所傳回的預測資料行。 資料行名稱應該要有和模型的輸出名稱相同的名稱。
- 所有輸入資料資料行和預測資料行都可在 SELECT 陳述式中顯示。

::: moniker range=">=azure-sqldw-latest"

您可藉由將 `MODEL` 指定為純量子查詢來重寫上述範例查詢以建立檢視：

```sql
CREATE VIEW predictions
AS
SELECT d.*, p.Score
FROM PREDICT(MODEL = (SELECT test_model FROM scoring_model WHERE model_id = 1),
             DATA = dbo.mytable AS d, RUNTIME = ONNX) WITH (Score FLOAT) AS p;
```

:::moniker-end

### <a name="combining-predict-with-an-insert-statement"></a>合併 PREDICT 與 INSERT 陳述式

預測的常見使用案例是為輸入資料產生分數，然後再將預測的值插入資料表。 下列範例假設呼叫應用程式是使用預存程序，將包含預測值的資料列插入資料表：

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current"

```sql
DECLARE @model VARBINARY(max) = (SELECT model FROM scoring_model WHERE model_name = 'ScoringModelV1');

INSERT INTO loan_applications (c1, c2, c3, c4, score)
SELECT d.c1, d.c2, d.c3, d.c4, p.score
FROM PREDICT(MODEL = @model, DATA = dbo.mytable AS d) WITH(score FLOAT) AS p;
```

:::moniker-end

::: moniker range=">=azure-sqldw-latest"

```sql
DECLARE @model VARBINARY(max) = (SELECT model FROM scoring_model WHERE model_name = 'ScoringModelV1');

INSERT INTO loan_applications (c1, c2, c3, c4, score)
SELECT d.c1, d.c2, d.c3, d.c4, p.score
FROM PREDICT(MODEL = @model, DATA = dbo.mytable AS d, RUNTIME = ONNX) WITH(score FLOAT) AS p;
```

:::moniker-end

- `PREDICT` 的結果會儲存在稱為 PredictionResults 的資料表中。 
- 模型會以 `varbinary(max)` 資料行的形式儲存在名為 **Models** 的資料表中。 如識別碼和描述的其他資訊可以儲存在資料表中以識別模型。
- 在 `DATA` 參數中針對資料表來源所指定的別名 **d** 是用來參考 `dbo.mytable` 中的資料行。輸入資料資料行名稱應該要符合模型的輸入名稱。
- 為 `PREDICT` 函式指定的別名 **p** 是用來參考 `PREDICT` 函式所傳回的預測資料行。 資料行名稱應該要有和模型的輸出名稱相同的名稱。
- 所有輸入資料行和預測資料行都可在 SELECT 陳述式中顯示。

## <a name="next-steps"></a>後續步驟

- [使用 PREDICT T-SQL 函式進行原生評分](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)
::: moniker range="=azure-sqldw-latest||=azuresqldb-mi-current"
-   [深入了解 ONNX 模型](/azure/machine-learning/concept-onnx#get-onnx-models)
::: moniker-end
