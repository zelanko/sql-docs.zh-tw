---
title: 建立、建構並查詢 geography 執行個體 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server]
- geodetic data type [SQL Server]
- geography data type [SQL Server], about geography data type
ms.assetid: b585851e-d15b-411f-adeb-aeabeb777c0b
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 5dde7575a3f657b89d29fefa0da52002bcd6af28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014300"
---
# <a name="create-construct-and-query-geography-instances"></a>建立、建構並查詢地理位置執行個體
  地理位置空間資料類型 (`geography`) 代表圓形表面座標系統中的資料。 這種類型在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中是實作為 .NET Common Language Runtime (CLR) 資料類型。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `geography` 資料類型會儲存橢圓體 (圓形表面) 資料，例如 GPS 經緯度座標。  
  
 
  `geography` 類型已預先定義，而且可在每一個資料庫中使用。 您可以建立 `geography` 類型的資料表資料行，並使用與其他系統提供之類型相同的方式來操作 `geography` 資料。  
  
##  <a name="creating"></a>建立或建立新的 geography 實例  
  
###  <a name="existing"></a>從現有的實例建立新的 geography 實例  
 
  `geography` 資料類型提供許多內建方法，您可以使用這些方法來根據現有執行個體建立新的 `geography` 執行個體。  
  
 **若要在地理位置周圍建立緩衝區**  
 [STBuffer &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stbuffer-geography-data-type)  
  
 **在地理位置周圍建立緩衝區，允許容錯**  
 [BufferWithTolerance &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/bufferwithtolerance-geography-data-type)  
  
 **從兩個 geography 實例的交集建立地理位置**  
 [STIntersection &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **從兩個 geography 實例的聯集建立地理位置**  
 [STUnion &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stunion-geography-data-type)  
  
 **從一個地理位置不重迭的點建立地理位置**  
 [STDifference &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
###  <a name="wkt"></a>從已知的文字輸入中，建立 geography 實例  
 
  `geography` 資料類型提供數種內建方法，可從開放式地理空間協會 (Open Geospatial Consortium，OGC) 的 WKT 表示法產生地理位置。 WKT 標準是一種文字字串，可允許使用文字格式交換地理位置資料。  
  
 **若要從 WKT 輸入中建立任何類型的 geography 實例**  
 [STGeomFromText &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)  
  
 [剖析 &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/parse-geography-data-type)  
  
 **若要從 WKT 輸入中建立地理位置 Point 實例**  
 [STPointFromText &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stpointfromtext-geography-data-type)  
  
 **若要從 WKT 輸入中建立地理 MultiPoint 實例**  
 [STMPointFromText &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stmpointfromtext-geography-data-type)  
  
 **若要從 WKT 輸入中建立地理位置 LineString 實例**  
 STLineFromText (geography 資料類型)  
  
 **若要從 WKT 輸入中建立地理位置 MultiLineString 實例**  
 [STMLineFromText &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stmlinefromtext-geography-data-type)  
  
 **若要從 WKT 輸入中建立地理多邊形實例**  
 [STPolyFromText &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stpolyfromtext-geography-data-type)  
  
 **若要從 WKT 輸入中建立地理位置 MultiPolygon 實例**  
 [STMPolyFromText &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stmpolyfromtext-geography-data-type)  
  
 **若要從 WKT 輸入中建立地理位置 GeometryCollection 實例**  
 [STGeomCollFromText &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stgeomcollfromtext-geography-data-type)  
  
###  <a name="wkb"></a>從已知的二進位輸入中，建立 geography 實例  
 WKB 是 OGC 指定的一種二進位格式，可允許在用戶端應用程式與 SQL 資料庫之間交換 `Geography` 資料。 下列函數可接受 WKB 輸入來建構地理位置執行個體：  
  
 **若要從 WKB 輸入中建立任何類型的 geography 實例**  
 [STGeomFromWKB &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stgeomfromwkb-geography-data-type)  
  
 **若要從 WKB 輸入中建立地理位置 Point 實例**  
 [STPointFromWKB &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stpointfromwkb-geography-data-type)  
  
 **若要從 WKB 輸入中建立地理 MultiPoint 實例**  
 [STMPointFromWKB &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stmpointfromwkb-geography-data-type)  
  
 **若要從 WKB 輸入中建立地理位置 LineString 實例**  
 [STLineFromWKB &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stlinefromwkb-geography-data-type)  
  
 **若要從 WKB 輸入中建立地理位置 MultiLineString 實例**  
 [STMLineFromWKB &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stmlinefromwkb-geography-data-type)  
  
 **若要從 WKB 輸入中建立地理多邊形實例**  
 [STPolyFromWKB &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stpolyfromwkb-geography-data-type)  
  
 **若要從 WKB 輸入中建立地理位置 MultiPolygon 實例**  
 [STMPolyFromWKB &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stmpolyfromwkb-geography-data-type)  
  
 **若要從 WKB 輸入中建立地理位置 GeometryCollection 實例**  
 [STGeomCollFromWKB &#40;Geography 資料類型&#41;](/sql/t-sql/spatial-geography/stgeomcollfromwkb-geography-data-type)STGeomCollFromWKB （geography 資料類型）  
  
###  <a name="gml"></a>從 GML 文字輸入中，建立 geography 實例  
 `geography`資料類型提供從 GML 產生`geography`實例的方法，這是`geography`實例的 XML 標記法。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可支援 GML 的子集。  
  
 如需地理標記語言的詳細資訊，請參閱 OGC 規格： [OGC 規格、地理標記語言](https://go.microsoft.com/fwlink/?LinkId=93629)。  
  
 **從 GML 輸入中建立任何類型的 geography 實例**  
 [GeomFromGML &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/geomfromgml-geography-data-type)  
  
##  <a name="returning"></a>從地理位置實例傳回已知的文字和已知的二進位格式  
 您可以使用下列方法傳回 WKT 或 WKB 格式的 `geography` 執行個體：  
  
 **傳回 geography 實例的 WKT 標記法**  
 [STAsText &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stastext-geography-data-type)  
  
 [ToString &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/tostring-geography-data-type)  
  
 **傳回 geography 實例的 WKT 標記法，包括任何 Z 和 M 值**  
 [AsTextZM &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/astextzm-geography-data-type)  
  
 **傳回 geography 實例的 WKB 標記法**  
 [STAsBinary &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stasbinary-geography-data-type)  
  
 **傳回 geography 實例的 GML 標記法**  
 [AsGml &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/asgml-geography-data-type)  
  
##  <a name="query"></a>查詢 geography 實例的屬性和行為  
 所有`geography`實例都有許多屬性，可以透過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供的方法來抓取。 下列主題定義地理位置類型的屬性和行為以及用來查詢每一個類型的方法。  
  
###  <a name="valid"></a>有效性、實例類型和 GeometryCollection 資訊  
 建構 `geography` 執行個體之後，您就可以使用下列方法來傳回執行個體類型，或者，如果它是 `GeometryCollection` 執行個體，就會傳回特定的 `geography` 執行個體。  
  
 **傳回地理位置的實例類型**  
 [STGeometryType &#40;geography 資料型別&#41;](/sql/t-sql/spatial-geography/stgeometrytype-geography-data-type)  
  
 **判斷 geography 是否為指定的實例類型**  
 [InstanceOf &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/instanceof-geography-data-type)  
  
 **判斷 geography 實例的實例類型是否格式正確**  
 [STNumGeometries &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stnumgeometries-geography-data-type)  
  
 **傳回 GeometryCollection 實例中的特定地理位置**  
 [STGeometryN &#40;Geography 資料類型&#41;](/sql/t-sql/spatial-geography/stgeometryn-geography-data-type)STGeometryN （geography 資料類型）  
  
###  <a name="number"></a>點數  
 所有非`geography`空的實例都是由*點*組成。 這些點代表 `geography` 執行個體繪製所在之地球的經緯度座標。 
  `geography` 資料類型提供了許多內建方法來查詢執行個體的點。  
  
 **傳回組成實例的點數目**  
 [STNumPoints &#40;geography 資料型別&#41;](/sql/t-sql/spatial-geography/stnumpoints-geography-data-type)  
  
 **傳回實例中的特定點**  
 [STPointN &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **傳回實例的起點**  
 [STStartPoint &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/ststartpoint-geography-data-type)  
  
 **傳回實例的結束點**  
 [STEndpoint &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stendpoint-geography-data-type)  
  
###  <a name="dimension"></a>大小  
 非空的 `geography` 執行個體可以是 0 維度、1 維度或 2 維度。 零維度`geography`的實例（例如`Point`和`MultiPoint`）沒有長度或區域。 一維度物件 (如 `LineString, CircularString`、`CompoundCurve` 和 `MultiLineString`) 具有長度。 二維度執行個體 (如 `Polygon, CurvePolygon` 和 `MultiPolygon`) 具有區域和長度。 空的執行個體會報告 -1 的維度，而 `GeometryCollection` 則會報告其內容的最大維度。  
  
 **傳回實例的維度**  
 [STDimension &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stdimension-geography-data-type)  
  
 **傳回實例的長度**  
 [STLength &#40;geography 資料型別&#41;](/sql/t-sql/spatial-geography/stlength-geography-data-type)  
  
 **傳回實例的區域**  
 [STArea &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/starea-geography-data-type)  
  
###  <a name="empty"></a>空  
 *空*`geography`的實例沒有任何點。 空的 `LineString, CircularString`、`CompoundCurve` 和 `MultiLineString` 執行個體的長度是 0。 空的 `Polygon, CurvePolygon` 和 `MultiPolygon` 執行個體的區域是 0。  
  
 **判斷實例是否為空的**  
 [STIsEmpty &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stisempty-geography-data-type)  
  
###  <a name="closure"></a>封閉  
 *封閉式*`geography`實例是起始點和結束點相同的圖形。 
  `Polygon` 執行個體視為封閉式。 
  `Point` 執行個體視為非封閉式。  
  
 環形是簡單、封閉的 `LineString` 執行個體。  
  
 **判斷實例是否已關閉**  
 [STIsClosed &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stisclosed-geography-data-type)  
  
 **傳回多邊形實例中的環形數**  
 [NumRings &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/numrings-geography-data-type)  
  
 **傳回 geography 實例的指定環形**  
 [RingN &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/ringn-geography-data-type)  
  
###  <a name="srid"></a>空間參考識別碼（SRID）  
 空間參考識別碼 (SRID) 是用來指定代表 `geography` 執行個體之橢圓體座標系統的識別碼。 具有不同 SRID 的兩個 `geography` 執行個體無法進行比較。  
  
 **若要設定或傳回實例的 SRID**  
 [STSrid &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stsrid-geography-data-type)  
  
 這個屬性可以修改。  
  
##  <a name="rel"></a>判斷地理位置實例之間的關聯性  
 
  `geography` 資料類型提供許多內建方法，您可以使用這些方法來判斷兩個 `geography` 執行個體之間的關聯性。  
  
 **判斷兩個實例是否組成相同的點集合**  
 [STEquals &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **判斷兩個實例是否不相交**  
 [STDisjoint &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **判斷兩個實例是否相交**  
 [STIntersects &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **判斷兩個實例相交的點**  
 [STIntersection &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **判斷兩個 geography 實例中的點之間的最短距離**  
 [STDistance &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
 **判斷兩個 geography 實例之間的點差異**  
 [STDifference &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
 **若要衍生一個 geography 實例與另一個實例相較之下的對稱差異或唯一點**  
 [STSymDifference &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stsymdifference-geography-data-type)  
  
##  <a name="supportedsrid"></a>地理位置實例必須使用支援的 SRID  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援以 EPSG 標準為根據的 SRID。 當執行計算或是搭配地理位置空間資料使用方法時，必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援之 `geography` 執行個體的 SRID。 SRID 必須符合 **sys.spatial_reference_systems** 目錄檢視中所顯示的其中一個 SRID。 如同之前所述，當您使用 `geography` 資料類型在您的空間資料上執行計算時，您的結果將會依據建立資料時使用哪一個橢圓體而定，因為每一個橢圓體都會指派一個特定的空間參考識別碼 (SRID)。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上使用方法時，`geography` 會使用預設 SRID 4326，此 SRID 會對應到 WGS 84 空間參考系統。 如果您使用 WGS 84 (或 SRID 4326) 以外之空間參考系統內的資料，您需要為您的地理位置空間資料決定特定的 SRID。  
  
##  <a name="examples"></a> 範例  
 下列範例示範如何加入及查詢地理位置資料。  
  
-   第一個範例會建立具有識別資料行及 `geography` 資料行 `GeogCol1`的資料表。 第三個資料行會將 `geography` 資料行轉譯成它的開放地理空間協會 (Open Geospatial Consortium，OGC) 已知的文字 (Well-Known Text，WKT) 表示法，並使用 `STAsText()` 方法。 然後會插入兩個資料列：一個資料列包含 `LineString` 的 `geography`執行個體，另一個資料列包含 `Polygon` 執行個體。  
  
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
    VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326));  
  
    INSERT INTO SpatialTable (GeogCol1)  
    VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
    GO  
    ```  
  
-   第二個範例使用 `STIntersection()` 方法傳回之前插入之兩個 `geography` 執行個體相交的點。  
  
    ```  
    DECLARE @geog1 geography;  
    DECLARE @geog2 geography;  
    DECLARE @result geography;  
  
    SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geog1.STIntersection(@geog2);  
    SELECT @result.STAsText();  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [空間資料 &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
