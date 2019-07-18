---
title: 查詢最接近像素的空間資料 | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 7af4ad5d-484e-45b4-aa16-83c33b358bb6
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 099771b9900d4c39de40b176cde5c92fa0c95462
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014104"
---
# <a name="query-spatial-data-for-nearest-neighbor"></a>查詢最接近像素的空間資料
  最接近像素查詢是搭配空間資料使用的常見查詢。 最接近像素查詢是用來尋找最接近特定空間物件的空間物件。 例如，網站的商店定位器通常必須尋找最接近客戶位置的商店位置。  
  
 您可以用各種有效的查詢格式來撰寫最接近像素查詢，但是若要讓最接近像素查詢使用空間索引，則必須使用下列語法。  
  
## <a name="syntax"></a>語法  
  
```vb  
SELECT TOP ( number )  
        [ WITH TIES ]  
        [ * | expression ]   
        [, ...]  
    FROM spatial_table_reference, ...   
        [ WITH   
            (   
                [ INDEX ( index_ref ) ]   
                [ , SPATIAL_WINDOW_MAX_CELLS = <value>]   
                [ ,... ]   
            )   
        ]  
    WHERE   
        column_ref.STDistance ( @spatial_ object )   
            {   
                [ IS NOT NULL ] | [ < const ] | [ > const ]   
                | [ <= const ] | [ >= const ] | [ <> const ] ]   
            }  
            [ AND { other_predicate } ]   
    }  
    ORDER BY column_ref.STDistance ( @spatial_ object ) [ ,...n ]  
[ ; ]  
  
```  
  
## <a name="nearest-neighbor-query-and-spatial-indexes"></a>最接近像素查詢和空間索引  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，`TOP` 及 `ORDER BY` 子句是用來針對空間資料資料行執行最接近像素查詢。 `ORDER BY` 子句包含空間資料行資料類型的 `STDistance()` 方法呼叫。 `TOP` 子句會指出要針對查詢傳回的物件數目。  
  
 若要讓最接近像素查詢使用空間索引，您必須符合下列需求：  
  
1.  空間索引必須存在其中一個空間資料行上，而且 `STDistance()` 方法必須在 `WHERE` 和 `ORDER BY` 子句中使用該資料行。  
  
2.  `TOP` 子句不得包含 `PERCENT` 陳述式。  
  
3.  `WHERE` 子句必須包含 `STDistance()` 方法。  
  
4.  如果 `WHERE` 子句中存在多個述詞，則包含 `STDistance()` 方法的述詞就必須透過 `AND` 結合連接至其他述詞。 `STDistance()` 方法不得位於 `WHERE` 子句的選擇性部分中。  
  
5.  `ORDER BY` 子句中的第一個運算式必須使用 `STDistance()` 方法。  
  
6.  `ORDER BY` 子句中第一個 `STDistance()` 運算式的排序次序必須是 `ASC`。  
  
7.  `STDistance` 傳回 `NULL` 的所有資料列都必須篩選出來。  
  
> [!WARNING]  
>  如果 `geography` 或 `geometry` 資料類型的 SRID 不相同，則接受這些類型做為引數的方法就會傳回 `NULL`。  
  
 建議您針對最接近像素查詢中使用的索引使用新的空間索引鑲嵌。 如需空間索引鑲嵌的詳細資訊，請參閱 [空間資料 &#40;SQL Server&#41;](spatial-data-sql-server.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例會顯示可使用空間索引的最接近像素查詢。 此範例會使用 `Person.Address` 資料庫中的 `AdventureWorks2012` 資料表。  
  
```  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
WHERE SpatialLocation.STDistance(@g) IS NOT NULL  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 您可以針對 SpatialLocation 資料行建立空間索引，以便查看最接近像素查詢如何使用空間索引。 如需建立空間索引的詳細資訊，請參閱 [建立、修改及卸除空間索引](create-modify-and-drop-spatial-indexes.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例會顯示無法使用空間索引的最接近像素查詢。  
  
```  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 這個查詢缺少按照語法區段中指定之格式使用 `STDistance()` 的 `WHERE` 子句，因此這個查詢無法使用空間索引。  
  
## <a name="see-also"></a>另請參閱  
 [空間資料 &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
