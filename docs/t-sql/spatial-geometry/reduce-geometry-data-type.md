---
title: Reduce (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b3706237fdd673e4bcf42fbcc5e611e094fd1ebf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47805616"
---
# <a name="reduce-geometry-data-type"></a>Reduce (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回在指定之 **geometry** 執行個體上執行 Douglas-Peucker 演算法延伸模組 (搭配指定的容錯) 所產生的該執行個體近似值。
  
## <a name="syntax"></a>語法  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>引數  
 *tolerance*  
 這是 **float** 類型的值。 *tolerance* 是近似值演算法的輸入容錯。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 就集合類型而言，此演算法會在執行個體所含的每個 **geometry** 上獨立運作。  
  
 此演算法不會修改 **Point** 執行個體。  
  
 在 **LineString****CircularString**及 **CompoundCurve** 執行個體上，近似值演算法會保留此執行個體的原始起點和終點，並反覆將原始執行個體中與結果偏差最大的點加回來，直到沒有任何點的偏差超過指定的容錯為止。  
  
 `Reduce()` 會傳回 **CircularString** 執行個體的 **LineString**、**CircularString**或 **CompoundCurve** 執行個體。  `Reduce()` 會傳回 **CompoundCurve** 執行個體的 **CompoundCurve** 或 **LineString** 執行個體。  
  
 在 **Polygon** 執行個體上，近似值演算法會獨立套用到每一個環形。 如果傳回的 **Polygon** 執行個體無效，此方法將會產生 `FormatException`；例如，如果套用 `Reduce()` 來簡化執行個體中的每一個環形，而產生的環形發生重疊，就會建立無效的 **MultiPolygon** 執行個體。  在具有外環但沒有內環的 **CurvePolygon** 執行個體上，`Reduce()` 會傳回 **CurvePolygon**、**LineString** 或 **Point** 執行個體。  如果 **CurvePolygon** 具有內環，則會傳回 **CurvePolygon** 或 **MultiPoint** 執行個體。  
  
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
 下列範例會在 **CircularString** 執行個體上使用 `Reduce()`搭配三個容錯層級：  
  
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
 下列範例會在 **CompoundCurve** 執行個體上使用 `Reduce()` 搭配兩個容錯層級：  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 在這個範例中，請注意，第二個 **SELECT** 陳述式會傳回 **LineString**執行個體：`LineString(0 0, 16 0)`。  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>示範原始起點和終點遺失的範例  
 下列範例示範結果執行個體可能無法保留原始起點和終點的方式。 因為保留原始起點和終點會導致產生無效的 **LineString** 執行個體，所以會發生此狀況。  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>另請參閱  
 [擴充的靜態幾何方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

