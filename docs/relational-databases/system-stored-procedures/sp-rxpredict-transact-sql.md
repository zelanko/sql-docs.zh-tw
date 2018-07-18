---
title: sp_rxPredict |Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
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
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: ede8232f36f42cc2b9758bdee8f50457ebd58dfe
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036046"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

產生預存的模型為基礎的預測的值。

提供在中近乎即時的機器學習服務模型評分。 `sp_rxPredict` 提供的包裝函式的預存程序`rxPredict`函式中[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)並[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)。 它以 C + 撰寫，並已特別針對評分作業最佳化。 它支援這兩個 R 或 Python 機器學習模型。

**本主題適用於**:  
- SQL Server 2017  
- SQL Server 2016 R Services 升級至 Microsoft R Server  

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

需要下列版本的其中一個：  
- SQL Server 2017 Machine Learning 服務 （包括 Microsoft R Server 9.1.0）  
- Microsoft Machine Learning 伺服器  
- SQL Server R Services 2016 中，使用 Microsoft R Server 9.1.0 之 R Services 執行個體的升級或更新版本  

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

  如需對應的 SQL 類型的資訊，請參閱[SQL-CLR 類型對應](https://msdn.microsoft.com/library/bb386947.aspx)或是[對應 CLR 參數資料](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。

