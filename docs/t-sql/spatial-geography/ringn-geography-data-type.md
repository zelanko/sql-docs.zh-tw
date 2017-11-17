---
title: "RingN (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RingN
- RingN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RingN method
ms.assetid: 30f47275-2727-4d22-bbec-c0c54bcb3ac2
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ddb30679406574a2f5f96687c4c04fae4c58f8e3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="ringn-geography-data-type"></a>RingN (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回的指定的環形**geography**執行個體： `1 ≤ n ≤ NumRings()`。  
  
## <a name="syntax"></a>語法  
  
```  
  
.RingN (expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 是**int**介於 1 到中的環數的運算式**多邊形**執行個體。  
  
## <a name="return-value"></a>傳回值  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 如果環形索引值 **n** 小於 1，這個方法會擲回**ArgumentOutOfRangeException。** 環形索引值必須大於或等於 1，而且應該小於或等於傳回的數字`NumRings()`。  
  
## <a name="examples"></a>範例  
 這個範例會建立具有兩個環形的 `Polygon` 例項，並傳回第二個環形。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.RingN(2).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [NumRings &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/numrings-geography-data-type.md)  
  
  

