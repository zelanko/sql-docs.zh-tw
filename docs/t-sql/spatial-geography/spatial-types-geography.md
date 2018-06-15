---
title: geography (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- geography
dev_langs:
- TSQL
helpviewer_keywords:
- geography data type [SQL Server], Transact-SQL
- spatial data types [SQL Server]
ms.assetid: d9e4952a-1841-4465-a64b-11e9288dba1d
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 03fa1c2b82196d119e69d5073e34de8f7be43234
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33062227"
---
# <a name="spatial-types---geography"></a>空間類型 - geography
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  地理空間資料型別 **geography** 會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中實作為 .NET Common Language Runtime (CLR) 資料型別。 此類型代表圓形地球座標系統中的資料。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** 資料類型會儲存橢圓體 (圓形地球) 資料，例如 GPS 經緯度座標。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 **geography** 空間資料型別的一組方法。 其中包括開放地理空間協會 (OGC) 標準所定義的 **geography** 方法以及該標準的一組 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 擴充。  
 
 **geography** 方法容許的誤差範圍可以高達 1.0e-7 *。 範圍指的是 **geography** 物件的點之間最大近似距離。
  

## <a name="registering-the-geography-type"></a>註冊 geography 類型  
 **geography** 類型已預先定義，而且可在每一個資料庫中使用。 您可以建立 **geography** 類型的資料表資料行，並使用與其他系統提供之類型相同的方式來操作 **geography** 資料。 可用於保存和非保存計算資料行。  
  
## <a name="examples"></a>範例  
  
### <a name="a-showing-how-to-add-and-query-geography-data"></a>A. 示範如何加入及查詢地理資料  
 下列範例示範如何加入及查詢地理位置資料。 第一個範例會建立具有識別資料行及 `geography` 資料行 `GeogCol1` 的資料表。 第三個資料行會將 `geography` 資料行轉譯成它的開放地理空間協會 (Open Geospatial Consortium，OGC) 已知的文字 (Well-Known Text，WKT) 表示法，並使用 `STAsText()` 方法。 然後會插入兩個資料列：一個資料列包含 `LineString` 的 `geography`執行個體，另一個資料列包含 `Polygon` 執行個體。  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeogCol1 geography,   
    GeogCol2 AS GeogCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656 )', 4326));  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653 , -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geography-instances"></a>B. 傳回兩個地理位置執行個體的交集  
 下列範例使用 `STIntersection()` 方法傳回之前插入之兩個 `geography` 執行個體相交的點。  
  
```  
DECLARE @geog1 geography;  
DECLARE @geog2 geography;  
DECLARE @result geography;  
  
SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geog1.STIntersection(@geog2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geography-in-a-computed-column"></a>C. 在計算資料行中使用地理  
 下列範例會以使用 **geography** 型別的保存計算資料行來建立資料表。  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geography,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>另請參閱  
 [空間資料 &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   

  
  
