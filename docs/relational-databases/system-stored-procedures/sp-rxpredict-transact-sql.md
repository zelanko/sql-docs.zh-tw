---
title: sp_rxPredict |Microsoft 文件
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: jeannt
ms.author: jeannt
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cef37349cd363ad7baea6300f3d236eefafd0046
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

產生預存的模型為基礎的預測的值。

提供在機器學習模型，以接近即時的計分。 `sp_rxPredict` 提供的包裝函式為預存程序`rxPredict`函式在[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)和[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)。 它以 C + 撰寫，而且特別適合計分作業。 它支援這兩個 R 或 Python 機器學習模型。

**本主題適用於**:  
- SQL Server 2017  
- 升級為 Microsoft R Server 與 SQL Server 2016 R Services  

## <a name="syntax"></a>語法

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>引數

**model**

預先定型的模型中支援的格式。 

**input**

有效的 SQL 查詢

### <a name="return-values"></a>傳回值

傳回分數資料行，以及任何傳遞的資料行，從輸入的資料來源。
其他分數資料行，例如信賴區間、 演算法是否支援產生這類值傳回。

## <a name="remarks"></a>備註

若要啟用預存程序，必須在執行個體上啟用 SQLCLR。

> [!NOTE]
> 啟用此選項之前，請考慮的安全性含意。

使用者需求`EXECUTE`資料庫的權限。

### <a name="supported-platforms"></a>支援的平台

需要下列其中一個下列版本：  
- SQL Server 2017 機器學習服務 （包括 Microsoft R Server 9.1.0）  
- Microsoft Machine Learning 伺服器  
- SQL Server R Services 2016 中，與 Microsoft R server 9.1.0 R 服務執行個體的升級或更新版本  

### <a name="supported-algorithms"></a>支援的演算法

如需支援的演算法的清單，請參閱[即時計分](../../advanced-analytics/real-time-scoring.md)。

下列模型類型**不**支援：  
- 包含其他不受支援的 R 轉換類型的模型  
- 模型使用`rxGlm`或`rxNaiveBayes`RevoScaleR 的演算法  
- PMML 模型  
- 使用 CRAN 或其他儲存機制從其他 R 程式庫建立的模型  
- 包含 R 轉換此處所列以外的任何其他種類的模型  

## <a name="examples"></a>範例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

除了有效的 SQL 查詢，在輸入資料*@inputData*必須在預存的模型中包含資料行與資料行相容。

`sp_rxPredict` 僅支援下列.NET 資料行類型： 雙精確度、 float、 short、 ushort、 long、 ulong 和字串。 您可能需要篩選出您的輸入資料中不支援的型別，才能將它用於即時計分。 

  如需對應的 SQL 型別資訊，請參閱[SQL CLR 類型對應](https://msdn.microsoft.com/library/bb386947.aspx)或[對應 CLR 參數資料](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。

