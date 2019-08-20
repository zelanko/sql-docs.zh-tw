---
title: 使用空間資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f133fa066ef2c486cf7bb40c5b653c99e077bc46
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026939"
---
# <a name="using-spatial-datatypes"></a>使用空間資料類型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

從 JDBC Driver preview 版本6.5.0 開始支援空間資料類型 (Geometry 和 Geography)。 預存程式、資料表值參數 (TVP)、BulkCopy 和 Always Encrypted 目前不支援空間資料類型。 此頁面會顯示 Geometry 和 Geography 資料類型與 JDBC 驅動程式的各種使用案例。 如需空間資料類型的總覽, 請參閱[空間資料類型總覽](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview)頁面。

## <a name="creating-a-geometry--geography-object"></a>建立 geometry/geography 物件

建立 Geometry/Geography 物件的主要方式有兩種: 從已知的文字 (WKT) 或已知的二進位 (WKB) 轉換。

### <a name="creating-from-wkt"></a>從 WKT 建立

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

這會建立具有空間參考系統識別碼 (SRID) 0 的 LINESTRING Geometry 物件, 以及具有 SRID 4326 的 Geography 物件。

### <a name="creating-from-wkb"></a>從 WKB 建立

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

這會建立與先前從 WKT 建立的 Geometry 和 Geography 物件。

## <a name="working-with-a-geometry--geography-object"></a>使用 Geometry/Geography 物件

假設使用者在 SQL Server 上有一個資料表, 如下所示:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

插入 Geometry 值的範例腳本如下:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

您可以使用 Geography 資料行和**setGeography ()** 方法, 針對 geography 對應來完成相同的作業。

若要讀取幾何/地理位置資料行:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

您可以使用 Geography 資料行和**getGeography ()** 方法, 針對 geography 對應來完成相同的作業。

## <a name="newly-introduced-apis"></a>新引進的 Api

這些是在類別**SQLServerPreparedStatement**、 **SQLServerResultSet**、 **Geometry**和**Geography**中引進的新公用 api。

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|方法|描述|
|:------|:----------|
|void setGeometry(int n, Geometry x)| 將指定的參數設定為指定的 microsoft .sql 類別物件。
|void setGeography(int n, Geography x)| 將指定的參數設定為指定的 microsoft .sql 類別物件。

### <a name="sqlserverresultset"></a>SQLServerResultSet

|方法|描述|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| 使用 JAVA 程式設計語言, 傳回這個 ResultSet 物件中目前資料列內所指定資料行的值來當做 .com 物件。
|Geometry getGeometry (字串 columnName)| 使用 JAVA 程式設計語言, 傳回這個 ResultSet 物件中目前資料列內所指定資料行的值來當做 .com 物件。
|Geography getGeography(int colunIndex)| 使用 JAVA 程式設計語言, 傳回這個 ResultSet 物件中目前資料列內所指定資料行的值來當做 .com 物件。
|Geography getGeography (字串 columnName)| 使用 JAVA 程式設計語言, 傳回這個 ResultSet 物件中目前資料列內所指定資料行的值來當做 .com 物件。

### <a name="geometry"></a>幾何

|方法|描述|
|:------|:----------|
|Geometry STGeomFromText(String wkt, int SRID)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geometry 執行個體的建構函式，經由此執行個體夾帶的任何 Z (高度) 值和 M (測量) 值來擴充。
|Geometry STGeomFromWKB(byte[] wkb)| 從開放地理空間協會 (OGC) Well-Known Binary (WKB) 表示法傳回之 Geometry 執行個體的建構函式。
|幾何還原序列化 (byte [] wkb)| 適用于空間資料之內部 SQL Server 格式之 Geometry 實例的構造函式。
|Geometry parse (字串 wkt)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geometry 執行個體的建構函式。 空間參考識別碼預設為0。
|Geometry point (double x, double y, int SRID)| Geometry 實例的函式, 表示來自其 X 和 Y 值的 Point 實例, 以及空間參考識別碼。
|String STAsText ()| 傳回 Geometry 執行個體的開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法。 此文字將不會包含此執行個體所夾帶的任何 Z (高度) 或 M (測量) 值。
|byte[] STAsBinary()| 傳回 Geometry 執行個體的開放式地理空間協會 (OGC) Well-Known Binary (WKB) 表示法。 這個值將不會包含此執行個體所夾帶的任何 Z 或 M 值。
|byte[] serialize()| 傳回表示 Geometry 類型之內部 SQL Server 格式的位元組。
|布林值 hasM ()| 如果物件包含 M (measure) 值, 則傳回。
|布林值 hasZ ()| 如果物件包含 Z (高度) 值, 則傳回。
|Double getX()| 傳回 X 座標值。
|Double getY()| 傳回 Y 座標值。
|Double getM()| 傳回物件的 M (量值) 值。
|Double getZ()| 傳回物件的 Z (高度) 值。
|int getSrid()| 傳回空間參考識別碼 (SRID) 值。
|boolean isNull()| 如果 Geometry 物件為 null, 則傳回。
|int STNumPoints ()| 傳回 Geometry 物件中的點數目。
|String STGeometryType()| 傳回幾何執行個體表示的開放式地理空間協會 (Open Geospatial Consortium，OGC) 類型名稱。
|String asTextZM()| 傳回 Geometry 物件的已知文字 (WKT) 標記法。
|字串 toString ()| 傳回 Geometry 物件的字串表示法。

### <a name="geography"></a>Geography

|方法|描述|
|:------|:----------|
|Geography STGeomFromText(String wkt, int SRID)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geography 執行個體的建構函式，經由此執行個體夾帶的任何 Z (高度) 值和 M (測量) 值來擴充。
|Geography STGeomFromWKB(byte[] wkb)| 從開放地理空間協會 (OGC) Well-Known Binary (WKB) 表示法傳回之 Geography 執行個體的建構函式。
|Geography 還原序列化 (byte [] wkb)| 地理位置實例的函式, 來自內部 SQL Server 格式的空間資料。
|地理剖析 (字串 wkt)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geography 執行個體的建構函式。 空間參考識別碼預設為0。
|地理點 (雙 lon、雙 lat、int SRID)| 代表位置執行個體 (經緯度及空間參考識別碼) 之地理執行個體的建構函式。
|String STAsText ()| 傳回 Geography 執行個體的開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法。 此文字將不會包含此執行個體所夾帶的任何 Z (高度) 或 M (測量) 值。
|byte[] STAsBinary())| 傳回 Geography 執行個體的開放地理空間協會 (OGC) Well-Known Binary (WKB) 表示法。 這個值將不會包含此執行個體所夾帶的任何 Z 或 M 值。
|byte[] serialize()| 傳回表示 Geography 類型之內部 SQL Server 格式的位元組。
|布林值 hasM ()| 如果物件包含 M (measure) 值, 則傳回。
|布林值 hasZ ()| 如果物件包含 Z (高度) 值, 則傳回。
|Double getLatitude()| 傳回緯度值。
|Double getLongitude()| 傳回經度值。
|Double getM()| 傳回物件的 M (量值) 值。
|Double getZ()| 傳回物件的 Z (高度) 值。
|int getSrid()| 傳回空間參考識別碼 (SRID) 值。
|boolean isNull()| 如果 Geography 物件為 null, 則傳回。
|int STNumPoints ()| 傳回 Geography 物件中的點數目。
|String STGeographyType()| 傳回 Geography 執行個體表示的開放式地理空間協會 (Open Geospatial Consortium，OGC) 類型名稱。
|String asTextZM()| 傳回 Geography 物件的已知文字 (WKT) 標記法。
|字串 toString ()| 傳回 Geography 物件的字串表示法。

## <a name="limitations-of-spatial-datatypes"></a>空間資料類型的限制

1. 只有從 SQL Server 2012 和更新版本開始才支援空間子資料類型**CircularString**、 **CompoundCurve**、 **CurvePolygon**和**FullGlobe** 。

2. Always Encrypted 不能與空間資料類型搭配使用。

3. 空間資料類型目前不支援預存程式、TVP 和 BulkCopy 作業。

## <a name="see-also"></a>另請參閱

[空間資料類型範例 (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
