---
title: "InstanceOf (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c53e66f85d614b79e51312dc4404fd19acd69fed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="instanceof-geometry-data-type"></a>InstanceOf (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

測試方法**幾何**執行個體是指定的型別相同。 如果傳回 1 的型別**幾何**執行個體與指定的型別相同，或指定的型別是上的階型別的執行個體; 否則傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
## <a name="arguments"></a>引數  
 *geometry_type*  
 是**nvarchar （4000)** 15 種類型中公開的其中一個指定字串**幾何**型別階層架構。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**位元**  
  
 CLR 傳回類型： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 方法的輸入必須是下列其中之一：**幾何**，**點**，**曲線**， **LineString**， **CircularString**， **CompoundCurve**，**介面**，**多邊形**， **CurvePolygon**， **GeometryCollection**， **MultiSurface**， **MultiPolygon**， **MultiCurve**， **MultiLineString**，和**MultiPoint**。 這個方法會擲回**ArgumentException**如果輸入有使用任何其他字串。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `MultiPoint` 例項，並使用 `InstanceOf()` 來查看此例項是否為 `GeometryCollection`。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

