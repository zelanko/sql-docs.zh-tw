---
title: "STNumCurves (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 26d949643c6af926b96ea1239f75226c470d5a08
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

這個方法會傳回中的曲線數目**幾何**一維空間資料類型執行個體時，執行個體。 一維空間資料類型包括**LineString**， **CircularString**，和**CompoundCurve**。 `STNumCurves`（） 只適用於簡單類型。不適用於**幾何**集合喜歡**MultiLineString**。
  
## <a name="syntax"></a>語法  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 空的一維**幾何**執行個體會傳回 0。 **NULL**時，會傳回**幾何**執行個體不是一維執行個體，或未初始化的執行個體。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. 在 CircularString 執行個體上使用 STNumCurves()  
 下列範例會顯示如何取得 `CircularString` 執行個體中的曲線數目：  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. 在 CompoundCurve 執行個體上使用 STNumCurves()  
 下列範例會使用 `STNumCurves()` 傳回 `CompoundCurve` 執行個體中的曲線數目。  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>請參閱＜  
 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

