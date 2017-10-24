---
title: "STDistance (geometry 資料類型) |Microsoft 文件"
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
- STDistance_TSQL
- STDistance (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDistance (geometry Data Type)
ms.assetid: ac815bc7-5342-4cc4-af40-c80a1c4c8b68
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ddb0d02f5bf4655acd97ba83484ac1d902420d9a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stdistance-geometry-data-type"></a>STDistance (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回中點之間的最短距離**幾何**執行個體和另一個點**幾何**執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STDistance ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是另一個**幾何**執行個體，用來測量所在之執行個體之間的距離`STDistance()`叫用。 如果*other_geometry*是空的集合，`STDistance()`會傳回 null。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **float**  
  
 CLR 傳回類型： **SqlDouble**  
  
## <a name="remarks"></a>備註  
 `STDistance()`一律傳回 null 如果的空間參考識別碼 (Srid)**幾何**例項不相符。  
  
## <a name="examples"></a>範例  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POINT(10 10)', 0);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>另請參閱  
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

