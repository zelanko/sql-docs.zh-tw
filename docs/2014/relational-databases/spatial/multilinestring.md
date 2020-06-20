---
title: MultiLineString | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fdd093d99d055df8e15fc22e3e570e6805e35d6e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003310"
---
# <a name="multilinestring"></a>MultiLineString
  `MultiLineString`是零個或多個 `geometry` 或**geographyLineString**實例的集合。  
  
## <a name="multilinestring-instances"></a>MultiLineString 執行個體  
 下圖顯示 `MultiLineString` 執行個體的範例。  
  
 ![幾何 MultiLineString 執行個體的範例](../../database-engine/media/multilinestring.gif "幾何 MultiLineString 執行個體的範例")  
  
 如本圖所示：  
  
-   [圖 1] 是一個簡單的 `MultiLineString` 實例，其界限是其兩個元素的四個端點 `LineString` 。  
  
-   圖 2 是簡單 `MultiLineString` 執行個體，因為只有 `LineString` 元素的端點才會相交。 界限是兩個非重疊的端點。  
  
-   圖 3 是非簡單的 `MultiLineString` 執行個體，因為它的其中一個 `LineString` 元素的內部會相交。 此 `MultiLineString` 執行個體的界限是這四個端點。  
  
-   圖 4 是非簡單、非封閉的 `MultiLineString` 執行個體。  
  
-   圖 5 是簡單、非封閉的 `MultiLineString`。 它不會關閉，因為它的 `LineStrings` 元素不會關閉。 因為任何 `LineStrings` 執行個體的內部都不相交，所以它是簡單的。  
  
-   圖 6 是簡單、封閉的 `MultiLineString` 執行個體。 它是封閉的，因為它的所有元素都是封閉的。 因為它的所有元素在內部都不相交，所以它是簡單的。  
  
### <a name="accepted-instances"></a>已接受的執行個體  
 若要接受 `MultiLineString`執行個體，則該執行個體必須是空的，或是僅由可接受的 `LineString` 執行個體組成。 如需已接受之實例的詳細資訊 `LineString` ，請參閱[LineString](../spatial/linestring.md)。 以下為可接受之 `MultiLineString` 執行個體的範例。  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
 下列範例會擲回 `System.FormatException`，因為第二個 `LineString` 執行個體無效。  
  
```  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>有效的執行個體  
 `MultiLineString` 執行個體必須符合下列準則，才會是有效的：  
  
1.  組成 `MultiLineString` 執行個體的所有執行個體必須都是有效的 `LineString` 執行個體。  
  
2.  組成 `LineString` 執行個體的任兩個 `MultiLineString` 執行個體都不可在間隔上重疊。 `LineString` 執行個體只能在有限的點數內彼此交集或接觸，或是接觸其他 `LineString` 執行個體。  
  
 下列範例示範三個有效的 `MultiLineString` 執行個體和一個無效的 `MultiLineString` 執行個體。  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` 無效，因為第二個 `LineString` 執行個體與第一個 `LineString` 執行個體於間隔處重疊。 兩者以無限點數接觸。  
  
## <a name="examples"></a>範例  
 下列範例會建立包含兩個具有 SRID 0 之 `geometry``MultiLineString` 元素的簡單 `LineString` 執行個體。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
```  
  
 若要使用不同的 SRID 來具現化這個執行個體，請使用 `STGeomFromText()` 或 `STMLineStringFromText()`。 您也可以使用 `Parse()` ，然後修改 SRID，如下列範例所示。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
SET @g.STSrid = 13;  
```  
  
## <a name="see-also"></a>另請參閱  
 [STLength &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STIsClosed &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [LineString](../spatial/linestring.md)   
 [空間資料 &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
