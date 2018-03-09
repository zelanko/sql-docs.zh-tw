---
title: "減少 (geometry 資料類型) |Microsoft 文件"
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
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb6c4a66f3233620ef5d24506d41e7659fc3b82d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="reduce-geometry-data-type"></a>Reduce (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回的近似值給定**幾何**由給定的容錯與執行個體上執行 Douglas-peucker 演算法的延伸模組所產生的執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>引數  
 *tolerance*  
 類型的值**float**。 *容錯*是近似值演算法的輸入容錯。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 集合類型，此演算法會操作獨立每**幾何**包含執行個體中。  
  
 此演算法不會修改**點**執行個體。  
  
 在**LineString**， **CircularString**，和**CompoundCurve**執行個體，近似值演算法會保留原始起點和終點的執行個體，並反覆將備份點從原始執行個體的結果，直到沒有點的最大的偏差超過給定的容錯。  
  
 `Reduce()`傳回**LineString**， **CircularString**，或**CompoundCurve**例項而言**CircularString**執行個體。  `Reduce()`傳回**CompoundCurve**或**LineString**例項而言**CompoundCurve**執行個體。  
  
 在**多邊形**執行個體，近似值演算法會獨立套用到每一個環形。 則方法會產生`FormatException`如果傳回**多邊形**執行個體不是有效; 例如，無效**MultiPolygon**如果，則會建立執行個體`Reduce()`套用至每一個簡化在執行個體，且產生的環形重疊推出。  在**CurvePolygon**執行個體與外部環形和任何內部環形，`Reduce()`傳回**CurvePolygon**， **LineString**，或**點**執行個體。  如果**CurvePolygon**有內環則**CurvePolygon**或**MultiPoint**會傳回執行個體。  
  
 在遇到圓弧線段時，近似值演算法會檢查弧形是否可依據其弦在給定容錯的一半內求得近似值。  如果弦符合此準則，計算中弦會取代圓弧。 如果它不符合此準則，則會保留圓弧，而且近似值演算法會套用至剩餘的線段。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-reduce-to-simplify-a-linestring"></a>A. 使用 Reduce() 以簡化 LineString  
 下列範例會建立 `LineString` 執行個體，並使用 `Reduce()` 來簡化此執行個體。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0, 2 1, 3 0, 4 1)', 0);  
SELECT @g.Reduce(.75).ToString();  
```  
  
### <a name="b-using-reduce-with-varying-tolerance-levels-on-a-circularstring"></a>B. 在 CircularString 上使用 Reduce() 搭配不同的容錯層級  
 下列範例會使用`Reduce()`三個容錯層級上**CircularString**執行個體：  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0)'; 
 SELECT @g.Reduce(5).ToString(); 
 SELECT @g.Reduce(15).ToString(); 
 SELECT @g.Reduce(16).ToString();
 ```  
  
 這個範例會產生下列輸出：  
  
 ```
 CIRCULARSTRING (0 0, 8 8, 16 0, 20 -4, 24 0) 
 COMPOUNDCURVE (CIRCULARSTRING (0 0, 8 8, 16 0), (16 0, 24 0)) 
 LINESTRING (0 0, 24 0)
 ```  
  
 每個傳回的執行個體都會包含端點 (0 0) 和 (24 0)。  
  
### <a name="c-using-reduce-with-varying-tolerance-levels-on-a-compoundcurve"></a>C. 在 CompoundCurve 上使用 Reduce() 搭配不同的容錯層級  
 下列範例會使用`Reduce()`搭配兩個容錯層級上**CompoundCurve**執行個體：  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 在此範例中請注意，第二個**選取**陳述式會傳回**LineString**執行個體： `LineString(0 0, 16 0)`。  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>示範原始起點和終點遺失的範例  
 下列範例示範結果執行個體可能無法保留原始起點和終點的方式。 這是因為保留原始起點和終點會導致無效**LineString**執行個體。  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>另請參閱  
 [擴充的靜態幾何方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

