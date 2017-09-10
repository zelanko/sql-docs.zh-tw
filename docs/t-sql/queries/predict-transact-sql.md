---
title: "預測 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 529cb229b6658085d0f2122604a4ed638f66a84c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="predict-transact-sql"></a>預測 (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

會產生預測的值或預存的模型為基礎的分數。  

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

`MODEL`參數用來指定用於計分或預測的模型。 模型已指定為變數或常值或純量運算式。

使用 R 或 Python 或其他工具，可以建立模型物件。

**資料**

資料參數用來指定用於計分或預測的資料。 資料會指定查詢中的資料表來源的形式。 資料表、 資料表別名，CTE 別名、 檢視或資料表值函式，可以是資料表來源。

**參數**

參數的參數用來指定用於計分或預測選擇性使用者定義參數。

每個參數的名稱是模型類型特有的。 例如，在 RevoScaleR rxPredict 函式支援參數_@computeResiduals元_評分羅吉斯迴歸模型時，支援計算剩餘數。 您可以傳遞至參數名稱，且值`PREDICT`函式。

> [注意]這個選項不支援的 SQL Server 2017 發行前版本，並隨附僅供向前相容性。

**使用 ( \<result_set_definition >)**

在 WITH 子句用來指定所傳回的輸出結構描述`PREDICT`函式。

所傳回的資料行除了`PREDICT`函式本身，屬於資料的所有資料行輸入可在查詢中使用。

### <a name="return-values"></a>傳回值

會提供; 沒有預先定義的結構描述SQL Server 不會驗證模型的內容，並不會驗證傳回的資料行值。  
- `PREDICT`函式做為輸入通過資料行  
- `PREDICT`函式也會產生新的資料行，但資料行和資料類型的數目取決於用於預測模型的類型。  

與資料相關的任何錯誤訊息，該模型或資料行格式會傳回基礎的預測函數與模型相關聯。  
- 對等函式是 RevoScaleR， [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)  
- 對等函式是 MicrosoftML， [rxPredict.mlModel](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxpredict)  

不可能內部模型結構使用檢視`PREDICT`。 如果您想要了解模型本身的內容，必須載入模型物件、 還原序列化，並使用適當的 R 程式碼剖析的模型。

## <a name="remarks"></a>備註

`PREDICT`函式支援所有版本的 SQL Server，包括 Linux。

您不需要 R、 Python 或其他機器學習語言安裝在要使用的伺服器上`PREDICT`函式。 您可以訓練另一個環境中的模型，並將它儲存到 SQL Server 資料表搭配使用`PREDICT`，或從另一個具有已儲存的模型的 SQL Server 執行個體呼叫模型。

### <a name="supported-algorithms"></a>支援的演算法

您使用的模型必須建立使用其中一種支援的演算法，從 RevoScaleR 封裝。 如需目前支援的模型，請參閱[即時計分](../../advanced-analytics/real-time-scoring.md)。

### <a name="permissions"></a>Permissions

不需要任何權限`PREDICT`; 不過，使用者需要`EXECUTE`資料庫的權限和使用權限來查詢使用做為輸入的任何資料。 使用者也必須能夠讀取模型資料表時，如果模型已儲存在資料表中。

## <a name="examples"></a>範例

下列範例示範的語法呼叫`PREDICT`。

### <a name="call-a-stored-model-and-use-it-for-prediction"></a>呼叫預存的模型，並將它用於預測

這個範例會呼叫 [models_table] 資料表中儲存的現有羅吉斯迴歸模型。 並取得最新定型的模型，使用 SELECT 陳述式，然後將二進位的模型傳遞至預測函式。 輸入的值代表的功能。輸出代表模型所指派的分類。

```sql
DECLARE @logit_model varbinary(max) = "SELECT TOP 1 @model from [models_table]";
DECLARE @input_qry = "SELECT ID, [Gender], [Income] from NewCustomers";

SELECT PREDICT [class]
FROM PREDICT( MODEL = @logit_model,  DATA = @input_qry
WITH (class string);
```

### <a name="using-predict-in-a-from-clause"></a>FROM 子句中使用預測

這個範例會參考`PREDICT`函式在`FROM`子句`SELECT`陳述式：

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

別名**d**資料表來源中指定_資料_參數用來參考屬於 dbo.mytable 的資料行。 別名**p**指定**預測**函數用來參考預測函數所傳回的資料行。

### <a name="combining-predict-with-an-insert-statement"></a>搭配 INSERT 陳述式結合預測

其中一個常見使用案例進行預測是產生的分數是輸入的資料，然後再將預測的值插入資料表。 下列範例假設要插入的資料列插入資料表中包含預測的值，呼叫應用程式要使用預存程序：

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

如果程序將採用透過資料表值參數的多個資料列，然後它可以寫入，如下所示：

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

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>建立 R 模型，並使用選擇性的模型參數的分數

> [!NOTE]
> 發行候選版本 1 中不支援使用參數的引數。

這個範例假設您已建立羅吉斯迴歸模型，共變數矩陣中，搭配使用 RevoScaleR 呼叫這類：

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

如果您以二進位格式將模型儲存在 SQL Server 中，您可以使用預測函數來產生預測，不僅支援的模型類型，例如錯誤或信心間隔的其他資訊。

下列程式碼顯示 rxPredict 來自 R 的對等呼叫：

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

相等的呼叫使用`PREDICT`函式也提供分數 （預測值），錯誤和信心間隔：

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```



