---
title: 空間資料 (SQL Server) | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f18e84ac46d4647c3bcd884b98196faf58bef636
ms.sourcegitcommit: 87f29b23d5ab174248dab5d558830eeca2a6a0a4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2018
ms.locfileid: "51018093"
---
# <a name="spatial-data-sql-server"></a>空間資料 (SQL Server)
  空間資料代表有關幾何物件之實體位置與形狀的資訊。 這些物件可以是點位置或更為複雜的物件，例如鄉村、道路或湖泊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援兩種空間資料類型：`geometry` 資料類型和 `geography` 資料類型。  
  
-   `geometry` 類型代表 Euclidean (平面) 座標系統中的資料。  
  
-   `geography` 類型代表圓形表面座標系統中的資料。  
  
 這兩種資料類型都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中實作為 .NET Common Language Runtime (CLR) 資料類型。  
  
> [!IMPORTANT]  
>  如需 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引進之空間功能的詳細描述和範例，請下載技術白皮書： [New Spatial Features in SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407)(SQL Server 2012 的新空間功能)。  
  
##  <a name="reltasks"></a> 相關工作  
 [建立、建構及查詢幾何執行個體](create-construct-and-query-geometry-instances.md)  
 描述可以與 geometry 資料類型執行個體搭配使用的方法。  
  
 [建立、建構並查詢地理位置執行個體](create-construct-and-query-geography-instances.md)  
 描述可以與 geography 資料類型執行個體搭配使用的方法。  
  
 [查詢最接近像素的空間資料](query-spatial-data-for-nearest-neighbor.md)  
 描述用以尋找最接近特定空間物件之空間物件的一般查詢模式。  
  
 [建立、修改及卸除空間索引](create-modify-and-drop-spatial-indexes.md)  
 提供有關建立、改變及卸除空間索引的詳細資訊。  
  
## <a name="related-content"></a>相關內容  
 [空間資料類型概觀](spatial-data-types-overview.md)  
 介紹空間資料類型。  
  
-   [點](point.md)  
  
-   [LineString](linestring.md)  
  
-   [CircularString](circularstring.md)  
  
-   [CompoundCurve](compoundcurve.md)  
  
-   [多邊形](polygon.md)  
  
-   [CurvePolygon](curvepolygon.md)  
  
-   [MultiPoint](multipoint.md)  
  
-   [MultiLineString](multilinestring.md)  
  
-   [MultiPolygon](multipolygon.md)  
  
-   [GeometryCollection](geometrycollection.md)  
  
 [空間索引概觀](spatial-indexes-overview.md)  
 介紹空間索引並描述鑲嵌和鑲嵌式配置。  
  
  
