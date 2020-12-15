---
description: CompoundCurve
title: CompoundCurve | Microsoft Docs
ms.date: 07/16/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: ae357f9b-e3e2-4cdf-af02-012acda2e466
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 919e71894dbf01ce015bed8eb3cc801bbad29c4a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97415961"
---
# <a name="compoundcurve"></a>CompoundCurve
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  **CompoundCurve** 是零個或多個屬於 geometry 或 geography 類型之連續 **CircularString** 或 **LineString** 執行個體的集合。  
  
您可以具現化空的 **CompoundCurve** 執行個體，但是若要讓 **CompoundCurve** 有效，它就必須符合下列準則：  
  
1.  它必須包含至少一個 **CircularString** 或 **LineString** 執行個體。  
  
2.  這序列的 **CircularString** 或 **LineString** 執行個體必須是連續的。  

如果 **CompoundCurve** 包含多個 **CircularString** 和 **LineString** 執行個體的序列，每個執行個體的結束端點 (最後一個執行個體除外) 都必須是序列中下一個執行個體的開始端點。 這表示，如果序列中前一個執行個體的結束點為 (4 3 7 2)，則序列中下一個執行個體的開始點就必須是 (4 3 7 2)。 請注意，點的 Z (高度) 和 M (測量) 值也必須相同。 如果兩個點存在差異，就會擲回 `System.FormatException` 。 **CircularString** 中的點不需要具有 Z 或 M 值。 如果沒有針對前一個執行個體的結束點給定 Z 或 M 值，下一個執行個體的開始點就不得包括 Z 或 M 值。 如果前一個序列的結束點為 (4 3)，下一個序列的開始點就必須是 (4 3)，不得為 (4 3 7 2)。 **CompoundCurve** 執行個體中的所有點都必須沒有 Z 值或具有相同的 Z 值。  
  
## <a name="compoundcurve-instances"></a>CompoundCurve 執行個體  
下圖顯示有效的 **CompoundCurve** 類型。  
  
![CompoundCurve 範例](../../relational-databases/spatial/media/f278742e-b861-4555-8b51-3d972b7602bf.gif)  
 
### <a name="accepted-instances"></a>已接受的執行個體  
 如果 **CompoundCurve** 執行個體是空的執行個體或符合下列準則，系統就會接受此執行個體。  
  
1.  **CompoundCurve** 執行個體所包含的所有執行個體都是已接受的圓弧線段執行個體。 如需已接受之圓弧線段執行個體的詳細資訊，請參閱 [LineString](../../relational-databases/spatial/linestring.md) 和 [CircularString](../../relational-databases/spatial/circularstring.md)。  
  
2.  **CompoundCurve** 執行個體中的所有圓弧線段都已連接。 每個後續圓弧線段的第一個點都與前一個圓弧線段的最後一個點相同。  
  
    > [!NOTE]  
    > 這包括 Z 和 M 座標。 因此，X、Y、Z 和 M 這四個座標都必須相同。  
  
3.  所有包含的執行個體都不是空的執行個體。  
  
下列範例會顯示已接受的 **CompoundCurve** 執行個體。  
  
```sql  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
```  
  
下列範例會顯示無法接受的 **CompoundCurve** 執行個體。 這些執行個體會擲回 `System.FormatException`。  
  
```sql  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING EMPTY)';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (1 0, 2 0))';  
```  
  
### <a name="valid-instances"></a>有效的執行個體  
 如果 **CompoundCurve** 執行個體符合下列準則，它就是有效的執行個體。  
  
1.  系統已接受 **CompoundCurve** 執行個體。  
  
2.  **CompoundCurve** 執行個體所包含的所有圓弧線段執行個體都是有效的執行個體。  
  
下列範例會顯示已接受的 **CompoundCurve** 執行個體。  
  
```sql  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
`@g3` 有效，因為 **CircularString** 執行個體有效。 如需 **CircularString** 執行個體有效性的詳細資訊，請參閱 [CircularString](../../relational-databases/spatial/circularstring.md)。  
  
下列範例會顯示無效的 **CompoundCurve** 執行個體。  
  
```sql  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4, 3 5))';  
DECLARE @g2 geometry = 'COMPOUNDCURVE((1 1, 1 1))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 2 3, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
`@g1` 無效，因為第二個執行個體不是有效的 LineString 執行個體。 `@g2` 無效，因為 **LineString** 執行個體無效。 `@g3` 無效，因為 **CircularString** 執行個體無效。 如需有效 **CircularString** 和 **LineString** 執行個體的詳細資訊，請參閱 [CircularString](../../relational-databases/spatial/circularstring.md) 和 [LineString](../../relational-databases/spatial/linestring.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-compooundcurve"></a>A. 使用空的 CompooundCurve 來具現化 geometry 執行個體  
 下列範例會示範如何建立空的 `CompoundCurve` 執行個體：  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-using-a-compoundcurve-in-the-same-statement"></a>B. 在相同的陳述式中使用 CompoundCurve 來宣告和具現化 geometry 執行個體  
 下列範例會示範如何在相同的陳述式中使用 `geometry` 來宣告和初始化 `CompoundCurve`執行個體：  
  
```sql  
DECLARE @g geometry = 'COMPOUNDCURVE ((2 2, 0 0),CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-compoundcurve"></a>C. 使用 CompoundCurve 來具現化 geography 執行個體  
 下列範例會示範如何使用 **來宣告和初始化** geography `CompoundCurve`執行個體：  
  
```sql  
DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-square-in-a-compoundcurve-instance"></a>D. 將正方形儲存在 CompoundCurve 執行個體中  
 下列範例會以兩種不同的方式使用 `CompoundCurve` 執行個體來儲存正方形。  
  
```sql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3), (1 3, 3 3),(3 3, 3 1), (3 1, 1 1))');  
SET @g2 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3, 3 3, 3 1, 1 1))');  
SELECT @g1.STLength(), @g2.STLength();  
```  
  
 `@g1` 和 `@g2` 的長度都相同。 在此範例中，請注意 **CompoundCurve** 執行個體可以儲存一個或多個 `LineString`執行個體。  
  
### <a name="e-instantiating-a-geometry-instance-using-a-compoundcurve-with-multiple-circularstrings"></a>E. 使用 CompoundCurve 搭配多個 CircularString 來具現化 geometry 執行個體  
 下列範例會示範如何使用兩個不同的 `CircularString` 執行個體來初始化 `CompoundCurve`執行個體。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT @g.STLength();  
```  
  
這會產生輸出 `12.5663706143592`，其相當於 4?。 在此範例中， `CompoundCurve` 執行個體會儲存半徑為 2 的圓形。 前兩個程式碼範例都不需要使用 `CompoundCurve`。 在第一個範例中， `LineString` 執行個體已經簡化了，而在第二個範例中， `CircularString` 執行個體也已經簡化了。 不過，下一個範例會顯示 `CompoundCurve` 提供較佳替代方式之處。  
  
### <a name="f-using-a-compoundcurve-to-store-a-semicircle"></a>F. 使用 CompoundCurve 來儲存半圓形  
 下列範例會使用 `CompoundCurve` 執行個體來儲存半圓形。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))');  
SELECT @g.STLength();  
```  
  
### <a name="g-storing-multiple-circularstring-and-linestring-instances-in-a-compoundcurve"></a>G. 將多個 CircularString 和 LineString 執行個體儲存在 CompoundCurve 中  
 下列範例會示範如何使用 `CircularString` 來儲存多個 `LineString` 和 `CompoundCurve`執行個體。  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::Parse('COMPOUNDCURVE((3 5, 3 3), CIRCULARSTRING(3 3, 5 1, 7 3), (7 3, 7 5), CIRCULARSTRING(7 5, 5 7, 3 5))');  
SELECT @g.STLength();  
```  
  
### <a name="h-storing-instances-with-z-and-m-values"></a>H. 儲存具有 Z 和 M 值的執行個體  
 下列範例會示範如何使用 `CompoundCurve` 執行個體來儲存具有 Z 和 M 值的 `CircularString` 和 `LineString` 執行個體序列。  
  
```sql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(7 5 4 2, 5 7 4 2, 3 5 4 2), (3 5 4 2, 8 7 4 2))');  
```  
  
### <a name="i-illustrating-why-circularstring-instances-must-be-explicitly-declared"></a>I. 說明必須明確宣告 CircularString 執行個體的原因  
 下列範例會顯示必須明確宣告 `CircularString` 執行個體的原因。 程式設計人員正嘗試將圓形儲存在 `CompoundCurve` 執行個體中。  
  
```sql  
DECLARE @g1 geometry;    
DECLARE @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 2 4, 0 2))');  
SELECT 'Circle One', @g1.STLength() AS Perimeter;  -- gives an inaccurate amount  
SET @g2 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT 'Circle Two', @g2.STLength() AS Perimeter;  -- now we get an accurate amount  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Circle One11.940039...  
Circle Two12.566370...  
```  
  
Circle Two 的圓周約為 4?，這是圓周的實際值。 不過，Circle One 的圓周則明顯不精確。 Circle One 的 `CompoundCurve` 執行個體會儲存一個圓弧線段 (ABC) 和兩個直線線段 (CD, DA)。 `CompoundCurve` 執行個體必須儲存兩個圓弧線段 (ABC, CDA) 才能定義圓形。 `LineString` 執行個體會在 Circle One 的 `CompoundCurve` 執行個體中定義第二組點 (4 2, 2 4, 0 2)。 您必須在 `CircularString` 內部明確宣告 `CompoundCurve`執行個體。  
  
## <a name="see-also"></a>另請參閱  
 [STIsValid &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [STLength &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STStartPoint &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)   
 [STEndpoint &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)   
 [CircularString](../../relational-databases/spatial/circularstring.md)   
 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [點](../../relational-databases/spatial/point.md)  
  
