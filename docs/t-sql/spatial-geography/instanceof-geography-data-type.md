---
title: "InstanceOf (geography 資料類型) |Microsoft 文件"
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
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0edbebbb6754fd09ff834e4ffe8d453853b6f240
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="instanceof-geography-data-type"></a>InstanceOf (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  測試如果**geography**執行個體是指定的型別相同。  
  
## <a name="syntax"></a>語法  
  
```  
  
.InstanceOf ( 'geography_type')  
```  
  
## <a name="arguments"></a>引數  
 *geography_type*  
 是**nvarchar （4000)**字串，指定其中一個 16 的類型中公開**geography**型別階層架構。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**位元**  
  
 CLR 傳回類型： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 如果傳回 1 的型別**geography**執行個體與指定的型別相同，或指定的型別是上的階型別的執行個體; 否則傳回 0。  
  
 這**geography**資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。  
  
 方法的輸入必須是下列其中一項： Geometry、 點、 曲線、 LineString、 CircularString、 介面、 Polygon、 CurvePolygon、 **GeometryCollection**， **MultiSurface**， **MultiPolygon、 MultiCurve、 MultiLineString**， **MultiPoint**，或**FullGlobe**。  
  
 如果輸入有使用任何其他字串，這個方法會擲回 `ArgumentException`。  
  
 這個方法並不精確。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `MultiPoint` 執行個體，並使用 `InstanceOf()` 來查看此執行個體是否為 `GeometryCollection`。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
