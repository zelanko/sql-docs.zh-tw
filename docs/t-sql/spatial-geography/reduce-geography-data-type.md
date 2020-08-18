---
description: Reduce (geography 資料類型)
title: Reduce (geography 資料類型)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ab2f24276cb3f151adf4e1418fd141180171a633
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88359874"
---
# <a name="reduce-geography-data-type-"></a>Reduce (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回在給定 **geography** 執行個體上執行 Douglas-Peucker 演算法 (具有給定的容錯) 所產生之該執行個體的近似值。  
  
 這個 **geography** 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.Reduce ( tolerance )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數

|詞彙|定義|
|----|----------|
|*tolerance*|這是 **float** 類型的值。 *tolerance* 是輸入到 Douglas-Peucker 演算法的容錯。 *tolerance* 必須是正數。|  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>備註  
 如果是集合類型，這個演算法會在此執行個體包含的每一個 **geography** 上獨立運作。 此演算法不會修改 **Point** 執行個體。  
  
 這個方法會嘗試保留 **LineString** 執行個體的端點，但為了保留有效的結果，這項嘗試可能會失敗。  
  
 如果使用負值呼叫 `Reduce()`，這個方法會產生 **ArgumentException**。 在 `Reduce()` 中使用的容錯必須是正數。  
  
 Douglas-Peucker 演算法可作用於 **geography** 執行個體中的每個曲線或環形，且會移除起點和終點以外的所有點。 接著會從最外圍的點開始加回每個移除的點，直到沒有點超出結果的 *tolerance*。 若有必要，之後會將結果設為有效，因為此方法保證結果有效。  
  
 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，這個方法已擴充到 **FullGlobe** 執行個體。  
  
 這個方法並不精確。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 執行個體，並使用 `Reduce()` 來簡化此執行個體。  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
