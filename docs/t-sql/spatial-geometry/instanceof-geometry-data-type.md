---
description: InstanceOf (geometry 資料類型)
title: InstanceOf (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5b79e0d67f11258afb8cf7aeebbfc4d52b9f4907
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88497041"
---
# <a name="instanceof-geometry-data-type"></a>InstanceOf (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

測試 **geometry** 執行個體是否與指定之型別相同的方法。 如果 **geometry** 執行個體類型與指定的類型相同，則傳回 1。 如果所指定類型是執行個體類型的上階項目，則這個方法也會傳回 1。 否則，這個方法會傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
*geometry_type*  
**nvarchar(4000)** 字串，它會指定在 **geometry** 類型階層內公開的 15 種類型其中之一。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>備註  
 此方法的輸入必須是下列其中一種類型：**Geometry**、**Point**、**Curve**、**LineString**、**CircularString**、**CompoundCurve**、**Surface**、**Polygon**、**CurvePolygon**、**GeometryCollection**、**MultiSurface**、**MultiPolygon**、**MultiCurve**、**MultiLineString** 和 **MultiPoint**。 如果輸入有使用任何其他字串，這個方法會擲回 **ArgumentException**。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `MultiPoint` 例項，並使用 `InstanceOf()` 來查看此例項是否為 `GeometryCollection`。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

