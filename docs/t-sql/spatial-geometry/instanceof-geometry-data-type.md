---
title: InstanceOf (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 809a8147033c22f59e9dd39a850c2270c0352d9c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="instanceof-geometry-data-type"></a>InstanceOf (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

測試 **geometry** 執行個體是否與指定之型別相同的方法。 如果 **geometry** 執行個體的型別與指定的型別相同，或是指定的型別是此執行個體型別的上階，則會傳回 1，否則會傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
## <a name="arguments"></a>引數  
 *geometry_type*  
 這是 **nvarchar(4000)** 字串，它會指定在 **geometry** 型別階層內公開之 15 種型別的其中一種。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 方法的輸入必須是下列其中之一：**Geometry**、**Point**、**Curve**、**LineString**、**CircularString**、**CompoundCurve**、**Surface**、**Polygon**、**CurvePolygon**、**GeometryCollection**、**MultiSurface**、**MultiPolygon**、**MultiCurve**、**MultiLineString** 和 **MultiPoint**。 如果輸入有使用任何其他字串，這個方法會擲回 **ArgumentException**。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `MultiPoint` 例項，並使用 `InstanceOf()` 來查看此例項是否為 `GeometryCollection`。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

