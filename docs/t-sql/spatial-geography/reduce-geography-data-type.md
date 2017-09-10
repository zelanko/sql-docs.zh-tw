---
title: "減少 (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c5b174f3f4b8daf99c402b110ba10d95345783d7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="reduce-geography-data-type-"></a>Reduce (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回的近似值給定**geography**所給定的容錯與執行個體上執行 Douglas-peucker 演算法產生的執行個體。  
  
 這**geography**資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>引數  
  
|||  
|-|-|  
|詞彙|定義|  
|*容錯*|類型的值**float**。 *容錯*是輸入到 Douglas-peucker 演算法的容錯。 *容錯*必須是正數。|  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 集合類型，此演算法會操作獨立每**geography**包含執行個體中。 此演算法不會修改**點**執行個體。  
  
 這個方法會嘗試保留的端點**LineString**例項，但是若要這樣做以維持有效的結果可能會失敗。  
  
 如果`Reduce()`會呼叫這個方法會產生含有負值， **ArgumentException**。 在 `Reduce()` 中使用的容錯必須是正數。  
  
 Douglas-peucker 演算法的運作在每個曲線或環形**geography**藉由移除起點和終點以外的所有點的執行個體。 移除每個點接著會新增回來，直到沒有點，從最外圍點，多個*容錯*結果。 若有必要，之後會將結果設為有效，因為此方法保證結果有效。  
  
 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，這個方法已擴充到**FullGlobe**執行個體。  
  
 這個方法並不精確。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 執行個體，並使用 `Reduce()` 來簡化此執行個體。  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
