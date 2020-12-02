---
description: STRelate (geometry 資料類型)
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
ms.openlocfilehash: e427ca859bf6e1e861ed58bb7fdc4ab2dc869fc1
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88444970"
---
# <a name="strelate-geometry-data-type"></a>STRelate (geometry 資料類型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  如果 **geometry** 執行個體與另一個 **geometry** 執行個體有關 (關聯性是由 Dimensionally Extended 9 Intersection Model (DE-9IM) 模式矩陣值所定義)，便傳回 1；否則會傳回 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STRelate ( other_geometry, intersection_pattern_matrix )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *other_geometry*  
 這是要與叫用 `STRelate()` 所在之執行個體相比較的另一個 **geometry** 執行個體。  
  
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
  
  
