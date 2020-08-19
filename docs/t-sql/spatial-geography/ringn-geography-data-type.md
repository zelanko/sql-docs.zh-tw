---
description: RingN (geography 資料類型)
title: RingN (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RingN
- RingN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RingN method
ms.assetid: 30f47275-2727-4d22-bbec-c0c54bcb3ac2
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 58325135db25b79d7c38fb3447f6b7e5bfd8c89a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417014"
---
# <a name="ringn-geography-data-type"></a>RingN (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回 **geography** 執行個體的指定環形：`1 ≤ n ≤ NumRings()`。  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
.RingN (expression )
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *expression*  
 這是介於 1 和 **polygon** 執行個體中環形數之間的 **int** 運算式。  
  
## <a name="return-value"></a>傳回值  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>備註  
 如果環形索引 **n** 的值小於 1，則這個方法會擲回 **ArgumentOutOfRangeException**。 環形索引值必須大於或等於 1，而且應該要小於或等於 `NumRings()` 傳回的數字。  
  
## <a name="examples"></a>範例  
 這個範例會建立具有兩個環形的 `Polygon` 例項，並傳回第二個環形。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.RingN(2).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理執行個體上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [NumRings &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/numrings-geography-data-type.md)  
  
  
