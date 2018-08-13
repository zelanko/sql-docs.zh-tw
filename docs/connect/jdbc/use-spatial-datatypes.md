---
title: 使用空間資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc330f8d5dbc2a0f6c09adac0f61d4f603b4c02f
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662300"
---
# <a name="using-spatial-datatypes"></a>使用空間資料類型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

從 JDBC 驅動程式預覽版 6.5.0 支援空間資料類型 （Geometry 和 Geography）。 空間資料類型目前不支援使用預存程序、 資料表值參數 (TVP)、 大量複製，且一律會加密。 此頁面會顯示各種的 Geometry 和 Geography 資料類型的情況下使用 JDBC 驅動程式。 如需空間資料類型的概觀，請[空間資料類型概觀](https://docs.microsoft.com/en-us/sql/relational-databases/spatial/spatial-data-types-overview)頁面。

## <a name="creating-a-geometry--geography-object"></a>建立幾何 / 地理物件

有兩個主要的方式，建立幾何 / 地理物件-是轉換來自已知文字 (well-known text，WKT) 或已知二進位 (well-known binary，WKB)。

### <a name="creating-from-wkt"></a>建立從 well-known text，WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

這會使用 SRID 4326 建立 LINESTRING Geometry 物件與空間參考系統識別項 (SRID) 0 和地理位置物件。

### <a name="creating-from-wkb"></a>從 WKB 建立

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

這會建立幾何及地理位置的物件，相當於從 well-known text，WKT 先前建立的項目。

## <a name="working-with-a-geometry--geography-object"></a>使用幾何 / 地理物件

假設使用者具有類似下列的 SQL Server 上的資料表：

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

會插入一個幾何值的範例指令碼：

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

可以採取相同的地理對應中，使用地理資料行及**setGeography()** 方法。

若要讀取幾何 / 地理資料行：

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

可以採取相同的地理對應中，使用地理資料行及**getGeography()** 方法。

## <a name="newly-introduced-apis"></a>新引入的 Api

這些是新的公用 Api 與此新增功能，在類別中已引進**SQLServerPreparedStatement**， **SQLServerResultSet**， **Geometry**，和**Geography**。

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|方法|Description|
|:------|:----------|
|void setGeometry (int n，Geometry x)| 設定指定的參數來指定的 microsoft.sql.Geometry 類別物件。
|void setGeography (int n，地理位置 x)| 設定指定的參數來指定的 microsoft.sql.Geography 類別物件。

### <a name="sqlserverresultset"></a>SQLServerResultSet

|方法|Description|
|:------|:----------|
|幾何 getGeometry (int colunIndex)| 傳回這個結果集物件的目前資料列中的指定資料行的值來當做 Java 程式語言 com.microsoft.sqlserver.jdbc.Geometry 物件。
|幾何 getGeometry (字串 columnName)| 傳回這個結果集物件的目前資料列中的指定資料行的值來當做 Java 程式語言 com.microsoft.sqlserver.jdbc.Geometry 物件。
|Geography getGeography (int colunIndex)| 傳回這個結果集物件的目前資料列中的指定資料行的值來當做 Java 程式語言 com.microsoft.sqlserver.jdbc.Geography 物件。
|Geography getGeography (字串 columnName)| 傳回這個結果集物件的目前資料列中的指定資料行的值來當做 Java 程式語言 com.microsoft.sqlserver.jdbc.Geography 物件。

### <a name="geometry"></a>幾何

|方法|Description|
|:------|:----------|
|幾何 STGeomFromText (字串 well-known text，wkt，int SRID)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geometry 執行個體的建構函式，經由此執行個體夾帶的任何 Z (高度) 值和 M (測量) 值來擴充。
|幾何 STGeomFromWKB (byte [] well-known binary，wkb)| 從開放地理空間協會 (OGC) Well-Known Binary (WKB) 表示法傳回之 Geometry 執行個體的建構函式。
|幾何還原序列化 (byte [] well-known binary，wkb)| 從空間資料之內部 SQL Server 格式的 Geometry 執行個體的建構函式。
|幾何剖析 (字串 well-known text，wkt)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geometry 執行個體的建構函式。 空間參考識別碼被預設為 0。
|幾何點 （雙精度浮點數 x，雙重的 y 整數 SRID）| 表示 Point 執行個體根據其 X 和 Y 值與空間參考識別碼的 Geometry 執行個體的建構函式。
|字串 stastext （)| 傳回 Geometry 執行個體的開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法。 此文字將不會包含此執行個體所夾帶的任何 Z (高度) 或 M (測量) 值。
|byte [] stasbinary （)| 傳回 Geometry 執行個體的開放式地理空間協會 (OGC) Well-Known Binary (WKB) 表示法。 這個值將不會包含此執行個體所夾帶的任何 Z 或 M 值。
|byte [] serialize()| 傳回表示 Geometry 類型之內部 SQL Server 格式的位元組。
|布林 hasM()| 傳回物件是否包含 M （測量） 值。
|布林 hasZ()| 傳回物件是否包含 Z （高度） 值。
|Double getX()| 傳回 X 座標值。
|Double getY()| 傳回 Y 座標值。
|Double getM()| 傳回物件的 M （測量） 值。
|Double getZ()| 傳回物件的 Z （高度） 值。
|int getSrid()| 傳回的空間參考識別碼 (SRID) 的值。
|布林 Isnull| 傳回幾何物件是否為 null。
|int stnumpoints （)| 傳回幾何物件中的點數目。
|Stgeometrytype （字串)| 傳回幾何執行個體表示的開放式地理空間協會 (Open Geospatial Consortium，OGC) 類型名稱。
|字串 asTextZM()| 傳回幾何物件的已知文字 (well-known text，WKT) 表示。
|字串的 tostring （)| 傳回 Geometry 物件的字串表示法。

### <a name="geography"></a>Geography

|方法|Description|
|:------|:----------|
|Geography STGeomFromText (字串 well-known text，wkt，int SRID)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geography 執行個體的建構函式，經由此執行個體夾帶的任何 Z (高度) 值和 M (測量) 值來擴充。
|Geography STGeomFromWKB (byte [] well-known binary，wkb)| 從開放地理空間協會 (OGC) Well-Known Binary (WKB) 表示法傳回之 Geography 執行個體的建構函式。
|地理還原序列化 (byte [] well-known binary，wkb)| 從空間資料之內部 SQL Server 格式的地理位置執行個體的建構函式。
|Geography 剖析 (字串 well-known text，wkt)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geography 執行個體的建構函式。 空間參考識別碼被預設為 0。
|地理點 （雙 int SRID，double lon，lat）| Geography 執行個體的建構函式，其會根據 Point 執行個體的緯度和經度值與空間參考識別碼 (SRID) 來表示 Point 執行個體。
|字串 stastext （)| 傳回 Geography 執行個體的開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法。 此文字將不會包含此執行個體所夾帶的任何 Z (高度) 或 M (測量) 值。
|byte [] STAsBinary())| 傳回 Geography 執行個體的開放地理空間協會 (OGC) Well-Known Binary (WKB) 表示法。 這個值將不會包含此執行個體所夾帶的任何 Z 或 M 值。
|byte [] serialize()| 傳回表示 Geography 類型之內部 SQL Server 格式的位元組。
|布林 hasM()| 傳回物件是否包含 M （測量） 值。
|布林 hasZ()| 傳回物件是否包含 Z （高度） 值。
|Double getLatitude()| 傳回的緯度值。
|Double getLongitude()| 傳回的經度值。
|Double getM()| 傳回物件的 M （測量） 值。
|Double getZ()| 傳回物件的 Z （高度） 值。
|int getSrid()| 傳回的空間參考識別碼 (SRID) 的值。
|布林 Isnull| 傳回 Geography 物件是否為 null。
|int stnumpoints （)| 傳回 Geography 物件中的點數目。
|字串 STGeographyType()| 傳回 Geography 執行個體表示的開放式地理空間協會 (Open Geospatial Consortium，OGC) 類型名稱。
|字串 asTextZM()| 傳回的已知文字 (well-known text，WKT) 表示的地理物件。
|字串的 tostring （)| 傳回 Geography 物件的字串表示法。

## <a name="limitations-of-spatial-datatypes"></a>空間資料類型的限制

1. 空間的子資料類型**CircularString**， **CompoundCurve**， **CurvePolygon**，以及**FullGlobe**版本才支援從 SQL Server 2012 和更新版本。

2. Always Encrypted 無法搭配空間資料類型。

3. 預存程序、 TVP，以及大量複製作業目前不支援使用空間資料類型。

## <a name="see-also"></a>另請參閱

[空間資料類型範例 (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
