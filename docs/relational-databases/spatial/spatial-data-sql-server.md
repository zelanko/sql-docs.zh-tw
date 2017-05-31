---
title: "空間資料 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a7ed039271847202c8c84a03ec56d55a96593089
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="spatial-data-sql-server"></a>空間資料 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  空間資料代表有關幾何物件之實體位置與形狀的資訊。 這些物件可以是點位置或更為複雜的物件，例如鄉村、道路或湖泊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援兩種空間資料類型： **geometry** 資料類型和 **geography** 資料類型。  
  
-   **geometry** 類型代表 Euclidean (平面) 座標系統中的資料。  
  
-   **geography** 類型代表圓形表面座標系統中的資料。  
  
 這兩種資料類型都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中實作為 .NET Common Language Runtime (CLR) 資料類型。  
  
> [!IMPORTANT]  
>  如需 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引進之空間功能的詳細描述和範例，請下載技術白皮書： [New Spatial Features in SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407)(SQL Server 2012 的新空間功能)。  
  
##  <a name="reltasks"></a> 相關工作  
 [建立、建構及查詢幾何執行個體](../../relational-databases/spatial/create-construct-and-query-geometry-instances.md)  
 描述可以與 geometry 資料類型執行個體搭配使用的方法。  
  
 [建立、建構並查詢地理位置執行個體](../../relational-databases/spatial/create-construct-and-query-geography-instances.md)  
 描述可以與 geography 資料類型執行個體搭配使用的方法。  
  
 [查詢最接近像素的空間資料](../../relational-databases/spatial/query-spatial-data-for-nearest-neighbor.md)  
 描述用以尋找最接近特定空間物件之空間物件的一般查詢模式。  
  
 [建立、修改及卸除空間索引](../../relational-databases/spatial/create-modify-and-drop-spatial-indexes.md)  
 提供有關建立、改變及卸除空間索引的詳細資訊。  
  
## <a name="related-content"></a>相關內容  
 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)  
 介紹空間資料類型。  
  
-   [點](../../relational-databases/spatial/point.md)  
  
-   [LineString](../../relational-databases/spatial/linestring.md)  
  
-   [CircularString](../../relational-databases/spatial/circularstring.md)  
  
-   [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
  
-   [多邊形](../../relational-databases/spatial/polygon.md)  
  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  
  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
  
-   [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  
  
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)  
 介紹空間索引並描述鑲嵌和鑲嵌式配置。  
  
  
