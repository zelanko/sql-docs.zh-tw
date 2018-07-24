---
title: PREDICT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/02/2018
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= sql-server-2017 || = azuresqldb-current || = sqlallproducts-allversions'
ms.openlocfilehash: 4ec9f538c7506375adc74b4a0b2779b40bafab2f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37970998"
---
# <a name="predict-transact-sql"></a>PREDICT (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

根據預存模型產生預測值或分數。  

## <a name="syntax"></a>語法

```
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>  
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

### <a name="arguments"></a>引數

**model**

`MODEL` 參數用來指定用於計分或預測的模型。 模型指定為變數、常值或純量運算式。

使用 R 或 Python 或其他工具，可以建立模型物件。

**data**

DATA 參數用來指定用於計分或預測的資料。 資料是以查詢中的資料表來源形式指定。 資料表來源可以是資料表、資料表別名、CTE 別名、檢視或資料表值函數。

**parameters**

PARAMETERS 參數用來指定用於計分或預測的選擇性使用者定義參數。

每個參數的名稱都與模型類型有關。 例如，RevoScaleR 中的 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 函數援參數 `@computeResiduals`，表示評分羅吉斯迴歸模型時是否應該計算殘值。 如果您呼叫相容模型，就可以將該參數名稱與 TRUE 或 FALSE 值傳遞到 `PREDICT` 函數。

> [!NOTE]
> 此選項不適用於 SQL Server 2017 的發行前版本。

**WITH ( <result_set_definition> )**

WITH 子句用來指定 `PREDICT` 函數傳回之輸出的結構描述。

除了 `PREDICT` 函數傳回的資料行本身，屬於資料輸入的所有資料行都可在查詢中使用。

### <a name="return-values"></a>傳回值

沒有預先定義的結構描述。SQL Server 不會驗證模型的內容，也不會驗證傳回的資料行值。

- `PREDICT` 函數會傳入資料行做為輸入。
- `PREDICT` 函數也會產生新的資料行，但資料行數目和資料類型取決於用於預測的模型類型。

與模型相關聯的基礎預測函數，會傳回與資料、模型或資料行格式相關的任何錯誤訊息。

- 對於 RevoScaleR，對等的函數是 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)  
- 對於 MicrosoftML，對等的函數是 [rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict)  

使用 `PREDICT` 無法檢視內部模型結構。 如果您想要了解模型本身的內容，必須載入模型物件、將物件還原序列化，並使用適當的 R 程式碼剖析模型。

## <a name="remarks"></a>Remarks

所有版本的 SQL Server 2017 和更新版本都支援 `PREDICT` 函數。 此支援包括 SQL Server 2017 的 Linux 版。 雲端的 Azure SQL Database 也支援 `PREDICT`。 這些支援都已啟用，不論是否已啟用其他機器學習功能。

在要使用 `PREDICT` 函數的伺服器上，不一定要安裝 R、Python 或其他機器學習語言。 您可以在另一個環境中訓練模型，並將它儲存到 SQL Server 資料表，搭配 `PREDICT` 使用，或從儲存模型的另一個 SQL Server 執行個體呼叫模型。

### <a name="supported-algorithms"></a>支援的演算法

您使用的模型必須使用 RevoScaleR 套件中其中一種支援的演算法建立。 如需目前支援的模型清單，請參閱[即時計分](../../advanced-analytics/real-time-scoring.md)。

### <a name="permissions"></a>[權限]

`PREDICT` 不需要任何權限，不過，使用者需要資料庫的 `EXECUTE` 權限和查詢做為輸入之任何資料的權限。 如果模型儲存在資料表中，使用者也必須能夠從資料表讀取模型。

## <a name="examples"></a>範例

下列範例示範呼叫 `PREDICT` 的語法。

### <a name="call-a-stored-model-and-use-it-for-prediction"></a>呼叫預存的模型，並將它用於預測

此範例呼叫 [models_table] 資料表中儲存的現有羅吉斯迴歸模型。 範例會使用 SELECT 陳述式取得最新定型的模型，然後將二進位模型傳遞至 PREDICT 函數。 輸入值代表功能；輸出代表模型所指派的分類。

```sql
DECLARE @logit_model varbinary(max) = "SELECT TOP 1 [model_binary] from [models_table] ORDER BY [trained_date] DESC";
DECLARE @input_qry = "SELECT ID, [Gender], [Income] from NewCustomers";

SELECT PREDICT [class]
FROM PREDICT( MODEL = @logit_model,  DATA = @input_qry
WITH (class string);
```

### <a name="using-predict-in-a-from-clause"></a>在 FROM 子句中使用 PREDICT

此範例在 `SELECT` 陳述式的 `FROM` 子句中參考 `PREDICT` 函數：

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

`DATA` 參數中為資料表來源指定的別名 **d** 用來參考屬於 dbo.mytable 的資料行。 為 **PREDICT** 函數指定的別名 **p** 用來參考 PREDICT 函數所傳回的資料行。

### <a name="combining-predict-with-an-insert-statement"></a>合併 PREDICT 與 INSERT 陳述式

其中一個用於預測的常見使用案例是為輸入資料產生分數，然後再將預測的值插入資料表。 下列範例假設呼叫應用程式使用預存程序，將包含預測值的資料列插入資料表：

```sql
CREATE PROCEDURE InsertLoanApplication
(@p1 varchar(100), @p2 varchar(200), @p3 money, @p4 int)
AS
BEGIN
  DECLARE @model varbinary(max) = (select model
  FROM scoring_model
  WHERE model_name = 'ScoringModelV1');
  WITH d as ( SELECT * FROM (values(@p1, @p2, @p3, @p4)) as t(c1, c2, c3, c4) )

  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = d) WITH(score float) as p;
END;
```

如果程序透過資料表值參數取得多個資料列，就可以如下撰寫為：

```sql
CREATE PROCEDURE InsertLoanApplications (@new_applications dbo.loan_application_type)
AS
BEGIN
  DECLARE @model varbinary(max) = (SELECT model_bin FROM scoring_models WHERE model_name = 'ScoringModelV1');
  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = @new_applications as d)
  WITH (score float) as p;
END;
```

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>建立 R 模型，並使用選擇性的模型參數產生分數

> [!NOTE]
> 在候選版 1 中不支援使用參數引數。

此範例假設您已使用 RevoScaleR 的呼叫，建立一個以共變數矩陣擬合的羅吉斯迴歸模型，如下所示：

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

如果您以二進位格式將模型儲存在 SQL Server 中，使用 PREDICT 函數不只可以產生預測，還能產生模型類型支援的其他資訊，例如誤差或信賴區間。

下列程式碼示範從 R 對 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 的對等呼叫：

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

使用 `PREDICT` 函數的對等呼叫也提供分數 (預測值)、誤差和信賴區間：

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```
