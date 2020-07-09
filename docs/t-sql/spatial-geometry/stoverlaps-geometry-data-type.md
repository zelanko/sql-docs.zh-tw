---
title: STOverlaps (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STOverlaps (geometry Data Type)
- STOverlaps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STOverlaps (geometry Data Type)
ms.assetid: 1813cba1-5780-456a-9489-6b40a79569b3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5de112961599421eb7ce2d85d8152f1aa1339e0c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762251"
---
# <a name="stoverlaps-geometry-data-type"></a>STOverlaps (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

如果 **geometry** 執行個體與另一個 **geometry** 執行個體重疊，便傳回 1。 如果不是則傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.STOverlaps ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是要與叫用 `STOverlaps()` 所在之執行個體相比較的另一個 **geometry** 執行個體。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>備註  
 兩個 **geometry** 執行個體重疊的條件是：代表其交集的區域與這兩個執行個體的維度相同，而且區域不等於任一個執行個體。  
  
 如果 **geometry** 執行個體相交的點不是相同的維度，`STOverlaps()` 一律會傳回 0。  
  
 如果 **geometry** 執行個體的空間參考識別碼 (SRID) 不相符，這個方法一律會傳回 Null。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STOverlaps()` 來測試兩個 **geometry** 執行個體是否重疊。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STOverlaps(@h);  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

