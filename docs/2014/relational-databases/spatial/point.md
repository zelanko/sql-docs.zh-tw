---
title: 點 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- dbe-spatial
ms.topic: conceptual
helpviewer_keywords:
- Point geometry subtype [SQL Server]
- geometry data type [SQL Server], spatial data
ms.assetid: 2a596ec4-8b2f-4962-bcb4-e5c8f77edad5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c74251c9c1224dbbd376b57d81d5d180d03cb9c1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48146868"
---
# <a name="point"></a>點
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]空間資料，`Point`是一個代表單一位置的 0 維度物件，並可包含 Z （高度） 和 M （測量） 值。  
  
## <a name="geography-data-type"></a>Geography 資料類型  
 geography 資料類型的 Point 類型代表單一位置，其中 *Lat* 和 *Long* 分別表示緯度和經度。 緯度和經度值會以度數測量。 緯度的值一定會在 [-90, 90] 間隔內，在這個範圍之外輸入的值將會擲回例外狀況。 經度的值一定會在 [-180, 180] 間隔內，在這個範圍之外的輸入值會折返，以配合這個範圍。 例如，如果輸入 190 當作經度，則它會折返到 -170 值。 *SRID* 表示要傳回之 **geography** 例項的空間參考識別碼。  
  
## <a name="geometry-data-type"></a>Geometry 資料類型  
 geometry 資料類型的 Point 類型代表單一位置，其中 *X* 代表正在產生之 Point 的 X 座標， *Y* 則代表正在產生之 Point 的 Y 座標。 *SRID* 表示要傳回之 **geometry** 例項的空間參考識別碼。  
  
## <a name="examples"></a>範例  
 下列範例會建立代表 SRID 為 0 之 (3, 4) 點的 `geometry Point`執行個體。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT (3 4)', 0);  
```  
  
 下一個範例會建立 `geometry``Point` 執行個體，它代表 Z (高度) 值為 7 且 M (測量) 值為 2.5 的 (3, 4) 點，而且預設 SRID 為 0。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 7 2.5)');  
```  
  
 最後一個範例會傳回 `geometry``Point` 執行個體的 X、Y、Z 和 M 值。  
  
```  
SELECT @g.STX;  
SELECT @g.STY;  
SELECT @g.Z;  
SELECT @g.M;  
```  
  
 Z 和 M 值可明確指定為 NULL，如下列範例所示。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 NULL NULL)');  
```  
  
## <a name="see-also"></a>另請參閱  
 [MultiPoint](multipoint.md)   
 [STX &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stx-geometry-data-type)   
 [STY &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/sty-geometry-data-type)   
 [空間資料 &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
