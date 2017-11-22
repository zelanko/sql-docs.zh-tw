---
title: "STRelate (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- STRelate (geometry Data Type)
- STRelate_TSQL
dev_langs: TSQL
helpviewer_keywords: STRelate (geometry Data Type)
ms.assetid: 9dcb5f58-35ab-4bb3-86ee-2d29eefba6d3
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bbda0b7d41dcf979afd23dba651b20513ea1b193
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="strelate-geometry-data-type"></a>STRelate (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回 1，如果**幾何**執行個體與另一個**幾何**執行個體，其中的關聯性是由 Dimensionally Extended 9 Intersection Model (DE 9IM) 模式矩陣值所定義; 否則為會傳回 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STRelate ( other_geometry, intersection_pattern_matrix )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是另一個**幾何**比較所在之執行個體的執行個體`STRelate()`叫用。  
  
 *intersection_pattern_matrix*  
 這是類型的字串**nchar(9)**編碼可接受的值兩者之間 DE 9IM 模式矩陣裝置**幾何**執行個體。  
  
## <a name="remarks"></a>備註  
 如果這個方法永遠傳回 null 的空間參考識別碼 (Srid)**幾何**例項不相符。 這個方法會擲回**ArgumentException**如果矩陣不是語式正確。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**位元**  
  
 CLR 傳回類型： **SqlBoolean**  
  
## <a name="examples"></a>範例  
 下列範例會使用`STRelate()`來測試兩個**幾何**脫離空間使用明確的 DE 9IM 模式的執行個體。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(5 5)', 0);  
SELECT @g.STRelate(@h, 'FF*FF****');  
```  
  
## <a name="see-also"></a>請參閱＜  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
