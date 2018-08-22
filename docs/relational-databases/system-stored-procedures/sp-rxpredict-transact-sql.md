---
title: sp_rxPredict |Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: database-engine
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
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8f46403afef0e2f6cf967561a8fd24ec6409fe93
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/22/2018
ms.locfileid: "40434858"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

產生給定的輸入，機器學習模型以二進位格式儲存在 SQL Server 資料庫為基礎的預測的值。

提供在 R 和 Python 機器學習服務模型中近乎即時評分。 `sp_rxPredict` 提供的包裝函式的預存程序`rxPredict`中的 R 函式[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)並[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)，而[rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) Python 函式，在[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)並[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)。 它以 C + 撰寫，並已特別針對評分作業最佳化。

**本文適用於**:  
- SQL Server 2017  
- SQL Server 2016 R Services 搭配[升級 R 元件](https://docs.microsoft.com/sql/advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server)

## <a name="syntax"></a>語法

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>引數

**model**

預先定型的模型支援的格式。 

**input**

有效的 SQL 查詢

### <a name="return-values"></a>傳回值

則會傳回分數資料行，以及任何傳遞的資料行，從輸入的資料來源。
其他分數資料行，例如信賴區間，如果演算法所支援的這類值產生可傳回。

## <a name="remarks"></a>備註

若要啟用使用預存程序，必須在執行個體上已啟用 SQLCLR。

> [!NOTE]
> 啟用此選項之前，請考慮安全性隱含意義。

使用者需求`EXECUTE`資料庫的權限。

### <a name="supported-platforms"></a>支援的平台
 
- SQL Server 2017 Machine Learning 服務 （包括 R Server 9.2）  
- SQL Server 2017 Machine Learning 伺服器 （獨立式） 
- SQL Server R Services 2016 中，使用 R 伺服器 9.1.0 R Services 執行個體的升級或更新版本  

### <a name="supported-algorithms"></a>支援的演算法

如需支援的演算法的清單，請參閱 <<c0> [ 即時評分](../../advanced-analytics/real-time-scoring.md)。

下列模型類型所**不**支援：  
- 包含其他不受支援的 R 轉換類型的模型  
- 模型使用`rxGlm`或`rxNaiveBayes`RevoScaleR 中的演算法  
- PMML 模型  
- 使用其他的 R 程式庫，從 CRAN 或其他存放庫中建立的模型  
- 包含 R 轉換，此處所列以外的任何其他類型的模型  

## <a name="examples"></a>範例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

有效的 SQL 查詢，輸入資料中除了*@inputData*必須在預存的模型中包含資料行與資料行相容。

`sp_rxPredict` 僅支援下列.NET 資料行類型： double、 float、 short、 ushort、 long、 ulong 和字串。 您可能需要篩選出您的輸入資料中不支援的型別才能使用它進行即時評分。 

  如需對應的 SQL 類型的資訊，請參閱[SQL-CLR 類型對應](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或是[對應 CLR 參數資料](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。

