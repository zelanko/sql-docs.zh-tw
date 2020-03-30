---
title: STRelate (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRelate (geometry Data Type)
- STRelate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRelate (geometry Data Type)
ms.assetid: 9dcb5f58-35ab-4bb3-86ee-2d29eefba6d3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1e50ca09fc8ac7c9c61c17227448deebe8c69bc8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68066315"
---
# <a name="strelate-geometry-data-type"></a>STRelate (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果 **geometry** 執行個體與另一個 **geometry** 執行個體有關 (關聯性是由 Dimensionally Extended 9 Intersection Model (DE-9IM) 模式矩陣值所定義)，便傳回 1；否則會傳回 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STRelate ( other_geometry, intersection_pattern_matrix )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是要與叫用 **所在之執行個體相比較的另一個**geometry`STRelate()` 執行個體。  
  
 *intersection_pattern_matrix*  
 這是兩個 **geometry** 執行個體之間 DE-9IM 模式矩陣裝置的 **nchar(9)** 類型編碼可接受值字串。  
  
## <a name="remarks"></a>備註  
 如果 **geometry** 執行個體的空間參考識別碼 (SRID) 不相符，這個方法一律會傳回 Null。 如果矩陣的格式不正確，這個方法將會擲回 **ArgumentException**。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STRelate()`，利用明確的 DE-9IM 模式測試兩個 **geometry** 執行個體是否在空間上不相鄰。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(5 5)', 0);  
SELECT @g.STRelate(@h, 'FF*FF****');  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
