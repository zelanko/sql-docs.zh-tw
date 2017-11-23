---
title: "STCrosses (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STCrosses (geometry Data Type)
- STCrosses_TSQL
dev_langs: TSQL
helpviewer_keywords: STCrosses (geometry Data Type)
ms.assetid: 3e3fc065-555a-4bee-8b71-e92f3dc62a4f
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c1da1525e2ae021478390fcec8ba6bc2ad87b291
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stcrosses-geometry-data-type"></a>STCrosses (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回 1，如果**幾何**執行個體會穿過另一個**幾何**執行個體。 如果不是則傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.STCrosses ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是另一個**幾何**比較所在之執行個體的執行個體`STCrosses()`叫用。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**位元**  
  
 CLR 傳回類型： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 兩個**幾何**兩個下列條件成立時，跨執行個體：  
  
-   兩個交集**幾何**結果中維度的來源的最大維度小於 geometry 執行個體**幾何**執行個體。  
  
-   交集位於兩個來源的內部**幾何**執行個體。  
  
 如果這個方法永遠傳回 null 的空間參考識別碼 (Srid)**幾何**例項不相符。  
  
## <a name="examples"></a>範例  
 下列範例使用 `STCrosses()` 來測試兩個 `geometry` 例項是否相交。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0)', 0);  
SET @h = geometry::STGeomFromText('LINESTRING(0 0, 2 2)', 0);  
SELECT @g.STCrosses(@h);  
```  
  
## <a name="see-also"></a>請參閱＜  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

