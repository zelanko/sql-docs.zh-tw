---
title: geometry (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- geometry
dev_langs:
- TSQL
helpviewer_keywords:
- spatial data types [SQL Server]
- geometry data type [SQL Server], Transact-SQL
ms.assetid: 3fefdf7b-f931-404c-821c-82c0375eaf51
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a2b65decea6d737801ef1b0b37e44b0c8ae028af
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68101009"
---
# <a name="spatial-types---geometry-transact-sql"></a>空間類型 - geometry (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  平面空間資料類型 **geometry** 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中是實作為通用語言執行平台 (CLR) 資料類型。 此類型代表以 Euclidean (平面) 座標系統表示的資料。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援一組 **geometry** 空間資料類型方法。 這些方法包括「開放地理空間協會」(OGC) 標準及該標準的一組 **延伸模組所定義的**geometry[!INCLUDE[msCoName](../../includes/msconame-md.md)] 相關方法。  
 
 geometry 方法的誤差容許範圍可以大到 1.0e-7 *。 範圍指的是 **geometry** 物件的點之間大致的最大距離。
  
## <a name="registering-the-geometry-type"></a>註冊 geometry 類型  
 **geometry** 類型已預先定義，而且可在每一個資料庫中使用。 您可以建立 **geometry** 類型的資料表資料行，並使用與其他 CLR 類型相同的方式來操作 **geometry** 資料。 可用於保存和非保存計算資料行。  
  
## <a name="examples"></a>範例  
  
### <a name="a-showing-how-to-add-and-query-geometry-data"></a>A. 示範如何加入及查詢幾何資料  
 下列兩個範例示範如何加入及查詢幾何資料。 第一個範例會建立具有識別資料行及 `geometry` 資料行 `GeomCol1` 的資料表。 第三個資料行會將 `geometry` 資料行轉譯成它的開放地理空間協會 (Open Geospatial Consortium，OGC) 已知的文字 (Well-Known Text，WKT) 表示法，並使用 `STAsText()` 方法。 然後會插入兩個資料列：一個資料列包含 `LineString` 的 `geometry`執行個體，另一個資料列包含 `Polygon` 執行個體。  
  
```sql 
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeomCol1 geometry,   
    GeomCol2 AS GeomCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geometry-instances"></a>B. 傳回兩個幾何執行個體的交集  
 第二個範例使用 `STIntersection()` 方法傳回之前插入之兩個 `geometry` 執行個體相交的點。  
  
```sql  
DECLARE @geom1 geometry;  
DECLARE @geom2 geometry;  
DECLARE @result geometry;  
  
SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geom1.STIntersection(@geom2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geometry-in-a-computed-column"></a>C. 在計算資料行中使用幾何  
 下列範例會使用 **geometry** 類型來建立含有保存之計算資料行的資料表。  
  
```sql  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geometry,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>另請參閱  
  [空間資料 &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
