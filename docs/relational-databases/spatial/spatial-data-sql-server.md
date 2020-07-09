---
title: 空間資料 (SQL Server) | Microsoft Docs
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 32014323cf9921cdbff9db6235e6625b4dc431ec
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725873"
---
# <a name="spatial-data-sql-server"></a>空間資料 (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  空間資料代表幾何物件的實體位置和圖形相關資訊。 這些物件可以是點位置或更複雜的物件，例如國家/地區、道路或湖泊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援兩種空間資料類型： **geometry** 資料類型和 **geography** 資料類型。  
  
-   **geometry** 類型代表 Euclidean (平面) 座標系統中的資料。  
  
-   **geography** 類型代表圓形表面座標系統中的資料。  
  
 這兩種資料類型都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中實作為 .NET Common Language Runtime (CLR) 資料類型。  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> 相關工作  
 [建立、建構及查詢幾何執行個體](../../relational-databases/spatial/create-construct-and-query-geometry-instances.md)  
 描述可以與 geometry 資料類型執行個體搭配使用的方法。  
  
 [建立、建構及查詢地理位置執行個體](../../relational-databases/spatial/create-construct-and-query-geography-instances.md)  
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
  
-   [Polygon](../../relational-databases/spatial/polygon.md)  
  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  
  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
  
-   [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  
  
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)  
 介紹空間索引並描述鑲嵌和鑲嵌式配置。  
  
  
