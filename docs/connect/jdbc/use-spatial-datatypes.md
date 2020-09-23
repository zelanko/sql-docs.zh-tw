---
description: 使用空間資料類型
title: 使用空間資料類型 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0f4b01775e2c78c0cc8602539169a794eb476f92
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487958"
---
# <a name="using-spatial-datatypes"></a>使用空間資料類型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

從 JDBC Driver 預覽版本 6.5.0 開始支援空間資料類型 (Geometry 和 Geography)。 預存程序、資料表值參數 (TVP)、BulkCopy 和 Always Encrypted 目前不支援空間資料類型。 此頁面顯示 Geometry 和 Geography 資料類型搭配 JDBC Driver 的各種使用案例。 如需空間資料類型的概觀，請參閱[空間資料類型概觀](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview)頁面。

## <a name="creating-a-geometry--geography-object"></a>建立 Geometry / Geography 物件

建立 Geometry / Geography 物件的主要方式有兩種：從 Well-Known Text (WKT) 或內部 SQL Server 格式 (CLR) 轉換。

### <a name="creating-from-wkt"></a>從 WKT 建立

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

這將會建立空間參考系統識別碼 (SRID) 為 0 的 LINESTRING Geometry 物件，以及 SRID 為 4326 的 Geography 物件。

### <a name="creating-from-clr"></a>從 CLR 建立

```java
byte[] geomCLR = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogCLR = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomCLR);
Geography geogWKT = Geography.deserialize(geogCLR);
```

這將會建立與先前從 WKT 建立的 Geometry 和 Geography 物件相當的物件。

## <a name="working-with-a-geometry--geography-object"></a>使用 Geometry / Geography 物件

假設使用者在 SQL Server 上擁有如下的資料表：

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

以下為插入 Geometry 值的範例指令碼：

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

您可以使用 Geography 資料行和 **setGeography()** 方法，針對 Geography 對應項目完成相同的作業。

讀取 Geometry / Geography 資料行：

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

您可以使用 Geography 資料行和 **getGeography()** 方法，針對 Geography 對應項目完成相同的作業。

## <a name="newly-introduced-apis"></a>新引進的 API

這些是在類別 **SQLServerPreparedStatement**、**SQLServerResultSet**、**Geometry** 和 **Geography** 中，透過此新增功能引進的新公用 API。

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|方法|描述|
|:------|:----------|
|void setGeometry(int n, Geometry x)| 將指定參數設定為指定的 microsoft.sql.Geometry 類別物件。
|void setGeography(int n, Geography x)| 將指定參數設定為指定的 microsoft.sql.Geography 類別物件。

### <a name="sqlserverresultset"></a>SQLServerResultSet

|方法|描述|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| 使用 Java 程式設計語言，以 com.microsoft.sqlserver.jdbc.Geometry 物件形式，傳回這個 ResultSet 物件之目前資料列中指定資料行的值。
|Geometry getGeometry(String columnName)| 使用 Java 程式設計語言，以 com.microsoft.sqlserver.jdbc.Geometry 物件形式，傳回這個 ResultSet 物件之目前資料列中指定資料行的值。
|Geography getGeography(int colunIndex)| 使用 Java 程式設計語言，以 com.microsoft.sqlserver.jdbc.Geography 物件形式，傳回這個 ResultSet 物件之目前資料列中指定資料行的值。
|Geography getGeography(String columnName)| 使用 Java 程式設計語言，以 com.microsoft.sqlserver.jdbc.Geography 物件形式，傳回這個 ResultSet 物件之目前資料列中指定資料行的值。

### <a name="geometry"></a>幾何形狀

|方法|描述|
|:------|:----------|
|Geometry STGeomFromText(String wkt, int SRID)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geometry 執行個體的建構函式，經由此執行個體夾帶的任何 Z (高度) 值和 M (測量) 值來擴充。
|Geometry STGeomFromWKB(byte[] wkb)| 從開放地理空間協會 (OGC) Well-Known Binary (WKB) 表示法傳回之 Geometry 執行個體的建構函式。 注意:此方法目前會使用內部 SQL Server 格式 (CLR) 來建立 Geometry 執行個體，此為驅動程式中的已知問題，且已規劃於未來變更成改為接受 WKB 資料。 對於已經使用此方法的現有使用者，請考慮改為切換成 deserialize(byte)。
|Geometries deserialize(byte[] clr)| 針對空間資料從內部 SQL Server 格式取得 Geometry 執行個體的建構函式。
|Geometry parse(String wkt)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geometry 執行個體的建構函式。 空間參考識別碼預設為 0。
|Geometry point(double x, double y, int SRID)| Geometry 執行個體的建構函式，其會根據 Point 執行個體的 X 和 Y 值與空間參考識別碼來代表該執行個體。
|String STAsText()| 傳回 Geometry 執行個體的開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法。 此文字將不會包含此執行個體所夾帶的任何 Z (高度) 或 M (測量) 值。
|byte[] STAsBinary()| 傳回 Geometry 執行個體的內部 SQL Server 格式 (CLR) 表示法。 這個值將不會包含此執行個體所夾帶的任何 Z 或 M 值。
|byte[] serialize()| 傳回表示 Geometry 類型之內部 SQL Server 格式的位元組。
|boolean hasM()| 傳回物件是否包含 M (量值) 值。
|boolean hasZ()| 傳回物件是否包含 Z (海拔) 值。
|Double getX()| 傳回 X 座標值。
|Double getY()| 傳回 Y 座標值。
|Double getM()| 傳回物件的 M (量值) 值。
|Double getZ()| 傳回物件的 Z (海拔) 值。
|int getSrid()| 傳回空間參考識別碼 (SRID) 值。
|boolean isNull()| 傳回 Geometry 物件是否為 Null。
|int STNumPoints()| 傳回 Geometry 物件中的點數目。
|String STGeometryType()| 傳回幾何執行個體表示的開放式地理空間協會 (Open Geospatial Consortium，OGC) 類型名稱。
|String asTextZM()| 傳回 Geometry 物件的 Well-Known Text (WKT) 表示法。
|String toString()| 傳回 Geometry 物件的字串表示法。

### <a name="geography"></a>[地理位置]

|方法|描述|
|:------|:----------|
|Geography STGeomFromText(String wkt, int SRID)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geography 執行個體的建構函式，經由此執行個體夾帶的任何 Z (高度) 值和 M (測量) 值來擴充。
|Geography STGeomFromWKB(byte[] wkb)| 從開放地理空間協會 (OGC) Well-Known Binary (WKB) 表示法傳回之 Geography 執行個體的建構函式。 注意:此方法目前會使用內部 SQL Server 格式 (CLR) 來建立 Geometry 執行個體，但這在未來將會變更成改為接受 WKB 資料，因為此方法的 SQL Server 對應項目 (STGeomFromWKB) 是使用 WKB。 對於已經使用此方法的現有使用者，請考慮改為切換成 deserialize(byte)。
|Geography deserialize(byte[] clr)| 針對空間資料從內部 SQL Server 格式取得 Geography 執行個體的建構函式。
|Geography parse(String wkt)| 從開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法傳回之 Geography 執行個體的建構函式。 空間參考識別碼預設為 0。
|Geography point(double lon, double lat, int SRID)| 代表位置執行個體 (經緯度及空間參考識別碼) 之地理執行個體的建構函式。
|String STAsText()| 傳回 Geography 執行個體的開放地理空間協會 (OGC) Well-Known Text (WKT) 表示法。 此文字將不會包含此執行個體所夾帶的任何 Z (高度) 或 M (測量) 值。
|byte[] STAsBinary())| 傳回 Geography 執行個體的內部 SQL Server 格式 (CLR) 表示法。 這個值將不會包含此執行個體所夾帶的任何 Z 或 M 值。
|byte[] serialize()| 傳回表示 Geography 類型之內部 SQL Server 格式的位元組。
|boolean hasM()| 傳回物件是否包含 M (量值) 值。
|boolean hasZ()| 傳回物件是否包含 Z (海拔) 值。
|Double getLatitude()| 傳回緯度值。
|Double getLongitude()| 傳回經度值。
|Double getM()| 傳回物件的 M (量值) 值。
|Double getZ()| 傳回物件的 Z (海拔) 值。
|int getSrid()| 傳回空間參考識別碼 (SRID) 值。
|boolean isNull()| 傳回 Geography 物件是否為 Null。
|int STNumPoints()| 傳回 Geography 物件中的點數目。
|String STGeographyType()| 傳回 Geography 執行個體表示的開放式地理空間協會 (Open Geospatial Consortium，OGC) 類型名稱。
|String asTextZM()| 傳回 Geography 物件的 Well-Known Text (WKT) 表示法。
|String toString()| 傳回 Geography 物件的字串表示法。

## <a name="limitations-of-spatial-datatypes"></a>空間資料類型的限制

1. 僅從 SQL Server 2012 和更新版本開始支援 **CircularString**、**CompoundCurve**、**CurvePolygon** 及 **FullGlobe** 空間子資料類型。

2. Always Encrypted 無法與空間資料類型搭配使用。

3. 空間資料類型目前不支援預存程序、TVP 和 BulkCopy 作業。

## <a name="see-also"></a>另請參閱

[空間資料類型範例 (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
