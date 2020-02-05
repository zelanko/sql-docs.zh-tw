---
title: STIntersects (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIntersects (geometry Data Type)
- STIntersects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersects (geometry Data Type)
ms.assetid: 7c18f5be-5a29-422e-8ca7-d8a5f38e03f5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 8a01a4ee58b4bca80cba9bfc9a1a094f575c5154
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67950122"
---
# <a name="stintersects-geometry-data-type"></a>STIntersects (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

如果 **geometry** 執行個體與另一個 **geometry** 執行個體相交，則會傳回 1。 如果不是則傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.STIntersects ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是要與叫用 **所在之執行個體相比較的另一個**geometry`STIntersects()` 執行個體。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>備註  
 如果 **geometry** 執行個體的空間參考識別碼 (SRID) 不相符，這個方法一律會傳回 Null。  
  
## <a name="examples"></a>範例  
 下列範例使用 `STIntersects()` 來判斷兩個 `geometry` 執行個體是否相交。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STIntersects(@h);  
```  
  
## <a name="see-also"></a>另請參閱  
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

