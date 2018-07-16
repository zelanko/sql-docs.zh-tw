---
title: MultiLineString | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c340afc52dbd60f4accb1da7d3883e62d36974f6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37288524"
---
# <a name="multilinestring"></a>MultiLineString
  A`MultiLineString`是零或多個集合`geometry`或是**geographyLineString**執行個體。  
  
## <a name="multilinestring-instances"></a>MultiLineString 執行個體  
 下圖顯示的範例`MultiLineString`執行個體。  
  
 ![幾何 MultiLineString 執行個體的範例](../../database-engine/media/multilinestring.gif "幾何 MultiLineString 執行個體的範例")  
  
 如本圖所示：  
  
-   圖 1 是簡單`MultiLineString`執行個體，其界限是其兩個的四個端點`LineString`項目。  
  
-   圖 2 是簡單 `MultiLineString` 執行個體，因為只有 `LineString` 元素的端點才會相交。 界限是兩個非重疊的端點。  
  
-   圖 3 是非簡單的 `MultiLineString` 執行個體，因為它的其中一個 `LineString` 元素的內部會相交。 這個界限`MultiLineString`執行個體是四個端點。  
  
-   圖 4 是非簡單、 非封閉的`MultiLineString`執行個體。  
  
-   圖 5 是簡單、非封閉的 `MultiLineString`。 它未關閉，因為其`LineStrings`未關閉元素。 很容易因為都不相交的任一`LineStrings`執行個體相交。  
  
-   圖 6 是簡單、 關閉`MultiLineString`執行個體。 它是封閉的，因為它的所有元素都是封閉的。 因為它的所有元素在內部都不相交，所以它是簡單的。  
  
### <a name="accepted-instances"></a>已接受的執行個體  
 針對`MultiLineString`執行個體，以接受它必須是可為空白或組成只`LineString`則可接受。 如需有關已接受`LineString`執行個體，請參閱[LineString](../spatial/linestring.md)。 以下為可接受之 `MultiLineString` 執行個體的範例。  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
 下列範例會擲回`System.FormatException`因為第二個`LineString`執行個體無效。  
  
```  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>有效的執行個體  
 針對`MultiLineString`執行個體有效，它必須符合下列準則：  
  
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
  
 `@g4` 不是有效因為第二個`LineString`與第一個執行個體重疊`LineString`的時間間隔的執行個體。 兩者以無限點數接觸。  
  
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
  
  
