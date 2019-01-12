---
title: 空間索引概觀 | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- spatial indexes [SQL Server]
ms.assetid: b1ae7b78-182a-459e-ab28-f743e43f8293
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 229674b624913c08b35637a106d9ced7e88e855d
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100883"
---
# <a name="spatial-indexes-overview"></a>空間索引概觀
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援空間資料和空間索引。 *「空間索引」* (Spatial Index) 是一種類型的擴充索引，可讓您建立空間資料行的索引。 空間資料行是包含空間資料類型資料的資料表資料行，例如 `geometry` 或 `geography`。  
  
> [!IMPORTANT]  
>  如需 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中導入的空間功能 (包括影響空間索引的功能) 的詳細描述和範例，請下載技術白皮書： [SQL Server 2012 中的新空間功能](https://go.microsoft.com/fwlink/?LinkId=226407)。  
  
##  <a name="about"></a> 關於空間索引  
  
###  <a name="decompose"></a> 將索引空間分解為方格階層  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，空間索引是使用 B 型樹狀結構所建立，這表示這些索引必須代表 B 型樹狀結構線性順序中的 2 維度空間資料。 因此，將資料讀入空間索引之前， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會實作空間的階層式統一分解。 索引建立程序會將空間 *「分解」* (Decompose) 成四層的 *「方格階層」*(Grid Hierarchy)。 這些層級稱為 *「層級 1」* (Level 1) (最上層)、 *「層級 2」*(Level 2)、 *「層級 3」*(Level 3) 和 *「層級 4」*(Level 4)。  
  
 每一個後續的層級都會進一步分解其上的層級，因此，每一個上層資料格都包含了下一層上的完整方格。 在給定的層級上，所有的方格沿著兩個座標軸會有相同的資料格數目 (例如 4x4 或 8x8)，而資料格都是同一大小。  
  
 下圖說明如何將方格階層之每一層上的右上方資料格分解成 4x4 方格。 事實上，所有的資料格都會以這個方式分解。 例如，將空間分解成四層的 4x4 方格實際上一共會產生 65,536 個層級四方格。  
  
 ![四個層級的遞迴鑲嵌](../../database-engine/media/spndx-recursive-levels-telescoped.gif "四個層級的遞迴鑲嵌")  
  
> [!NOTE]  
>  空間索引的空間分解與應用程式資料使用的度量單位無關。  
  
 方格階層資料格會以線性方式編號 (使用希伯特空間填滿曲線的變化)。 但是，為了說明起見，本討論內容會使用簡單的資料列取向編號，而不是希伯特曲線實際產生的編號。 在下圖中，代表建築物的幾個多邊形及代表街道的線條已經放到 4x4、層級 1 方格內。 層級 1 方格的編號是從 1 到 16 (從左上資料格開始)。  
  
 ![將多邊形和線條放到 4x4 層級 1 方格內](../../database-engine/media/spndx-level-1-objects.gif "將多邊形和線條放到 4x4 層級 1 方格內")  
  
#### <a name="grid-density"></a>方格密度  
 沿著方格座標軸的資料格數目會決定它的 *「密度」*(Density)：數目越大，方格的密度就越高。 例如，8x8 方格 (會產生 64 個資料格) 的密度大於 4x4 方格 (會產生 16 個資料格)。 方格密度是依照每個層級而定義。  
  
 [CREATE SPATIAL INDEX](/sql/t-sql/statements/create-spatial-index-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式支援 GRIDS 子句，該子句可讓您在不同的層級上指定不同的方格密度。 給定層級的方格密度是使用下列其中一個關鍵字所指定。  
  
|關鍵字|方格組態|資料格數目|  
|-------------|------------------------|---------------------|  
|LOW|4X4|16|  
|MEDIUM|8X8|64|  
|HIGH|16X16|256|  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，當資料庫相容性層級設定為 100 以下時，所有層級的預設值都是 MEDIUM。 當資料庫相容性層級設定為 110 以上時，預設值則為自動方格配置。  
  
 您可以藉由指定非預設的方格密度來控制分解程序。 例如，不同層級上的不同方格密度，對於微調以索引空間大小為根據的索引及空間資料行中的物件，可能會非常實用。  
  
> [!NOTE]  
>  當資料庫相容性層級設定為 100 以下時，空間索引的方格密度會顯示在 [sys.spatial_index_tessellations](/sql/relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql) 目錄檢視的 level_1_grid、level_2_grid、level_3_grid 和 level_4_grid 資料行中。 `GEOMETRY_AUTO_GRID` / `GEOGRAPHY_AUTO_GRID`鑲嵌式配置選項不會填入這些資料行。 sys.spatial_index_tessellations 目錄檢視具有`NULL`使用自動方格選項時，這些資料行值。  
  
###  <a name="tessellation"></a> 鑲嵌  
 將索引空間分解成方格階層之後，空間索引會從空間資料行讀取資料 (逐列讀取)。 在讀取空間物件 (或執行個體) 的資料之後，空間索引會針對該物件執行 *「鑲嵌程序」* (Tessellation Process)。 鑲嵌程序會將此物件納入方格階層中，方式是將此物件與它所接觸的一組方格資料格 (*「接觸的資料格」*(touched cell)) 產生關聯。 從方格階層的層級 1 開始，鑲嵌程序就會跨越此層級繼續進行 *「廣度優先」* (Breadth First)。 此程序可能繼續到所有的四個層級 (一次一個層級)。  
  
 鑲嵌程序的輸出是一組接觸的資料格，這些資料格會記錄在物件的空間索引內。 藉由參考這些記錄的資料格，空間索引就可以在同時儲存於索引內的空間資料行中，在相對於其他物件的空間內找出此物件。  
  
#### <a name="tessellation-rules"></a>鑲嵌規則  
 為了限制針對物件記錄之接觸的資料格數目，鑲嵌程序會套用數個鑲嵌規則。 這些規則會決定鑲嵌程序的深度，以及哪些接觸的資料格會記錄在索引內。  
  
 這些規則如下：  
  
-   涵蓋規則  
  
     如果此物件完全覆蓋資料格，則表示該資料格由該物件所 *「涵蓋」* (Cover)。 涵蓋的資料格會計算在內，而且不會加以鑲嵌。 這項規則會套用到方格階層的所有層級。 涵蓋規則簡化了鑲嵌程序，也減少了空間索引記錄的資料數量。  
  
-   每一物件的資料格規則  
  
     此規則會強制實施 *「每個物件的資料格限制」*(Cells-Per-Object Limit)，此限制可決定為每一個物件所計算的資料格數目 (除了層級 1 以外)。 在較低的層級上，每個物件的資料格規則會控制可記錄之物件相關的資訊數量。  
  
-   最深的資料格規則  
  
     最深的資料格規則會產生最近似的物件，其方式是只記錄已為該物件鑲嵌之最底層的資料格。 父資料格不算在每個物件的資料格計數內，所以不會記錄在索引內。  
  
 這些鑲嵌規則會遞迴地套用在每一個方格層級上。 本章節的其餘部分將更詳細地說明鑲嵌規則。  
  
#### <a name="covering-rule"></a>涵蓋規則  
 如果物件完全覆蓋資料格，則表示該資料格由該物件所 *「涵蓋」* (Cover)。 例如在下圖中，其中一個第二層資料格 15.11 完全被八邊形的中間部分所覆蓋。  
  
 ![涵蓋最佳化](../../database-engine/media/spndx-opt-covering.gif "涵蓋最佳化")  
  
 被覆蓋的資料格會計算及記錄在索引中，而且此資料格不會進一步加以鑲嵌。  
  
#### <a name="cells-per-object-rule"></a>每個物件的資料格規則  
 每個物件的鑲嵌範圍主要取決於空間索引的 *「每個物件的資料格限制」* (Cells-Per-Object Limit)。 這項限制定義了每個物件可以計算之鑲嵌的資料格最大數目。 但是請注意，每個物件的資料格規則不會強制對層級 1 實施，所以超出這個限制是有可能的。 如果到達層級 1 計數或是超出每個物件的資料格限制，則較低層級上不會發生進一步的鑲嵌。  
  
 只要此計數小於每個物件的資料格限制，鑲嵌程序就會繼續。 從數字最小的接觸資料格 (例如，上圖中的資料格 15.6) 開始，此程序會測試每一個資料格，以評估是否要計算它或是將它鑲嵌。 如果鑲嵌資料格將超出每個物件的資料格限制，此資料格就會計算在內且不會鑲嵌。 否則會鑲嵌此資料格，而且物件所接觸到的較低層資料格也會計算在內。 鑲嵌程序會繼續以這個方式橫跨層級來進行 (廣度取向)。 鑲嵌資料格之較低層的方格會遞迴重複這個程序，直到到達此限制或是不再計算其他資料格為止。  
  
 例如，以上圖為例，圖中顯示一個八邊形完全納入層級 1 方格的資料格 15。 在此圖中，已經鑲嵌資料格 15，將此八邊形分解成九個層級 2 的資料格。 這個圖假設每個物件的資料格限制為 9 以上 (含)。 但是，如果每個物件的資料格限制為 8 以下 (含)，將不會鑲嵌資料格 15，而且此物件只會計算該資料格 15。  
  
 根據預設，每一物件的資料格限制為 16 個資料格，這會在大多數空間索引的空間和精確度之間提供令人滿意的取捨。 不過， [CREATE SPATIAL INDEX](/sql/t-sql/statements/create-spatial-index-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式支援 CELLS_PER_OBJECT`=`*n*子句，可讓您指定 1 和 8192 之間，每個物件的資料格限制（含)。  
  
> [!NOTE]  
>  空間索引的 **cells_per_object** 設定可以在 [sys.spatial_index_tessellations](/sql/relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql) 目錄檢視中看到。  
  
#### <a name="deepest-cell-rule"></a>最深的資料格規則  
 最深的資料格規則利用了每一個較低層資料格都屬於其上方之資料格的事實：層級 4 資料格屬於層級 3 資料格、層級 3 資料格屬於層級 2 資料格，而層級 2 資料格則屬於層級 1 資料格。 例如，屬於資料格 1.1.1.1 的物件也屬於資料格 1.1.1、資料格 1.1 和資料格 1。 這類資料格階層關聯性的知識會內建在查詢處理器中。 因此，只有最深層的資料格才需要記錄在索引中，讓索引需要儲存的資訊減至最少。  
  
 下圖中會鑲嵌相對較小的鑽石形多邊形。 此索引會使用每個物件的資料格預設限制 16，這個小型物件未達到這個限制。 因此，鑲嵌會繼續往下到層級 4。 此多邊形位於下列層級 1 到層級 3 的資料格內：4、4.4、4.4.10 和 4.4.14。 但是使用了最深的資料格規則時，鑲嵌只會計算十二個層級 4 資料格：4.4.10.13-15 及 4.4.14.1-3、4.4.14.5-7 和 4.4.14.9-11。  
  
 ![最深的資料格最佳化](../../database-engine/media/spndx-opt-deepest-cell.gif "最深的資料格最佳化")  
  
###  <a name="schemes"></a> 鑲嵌式配置  
 空間索引的行為部分取決於它的 *「鑲嵌式配置」*(Tessellation Scheme)。 鑲嵌式配置是資料類型所特有。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，空間索引支援兩個鑲嵌式配置：  
  
-   *幾何方格鑲嵌*，這是配置`geometry`資料型別。  
  
-   *地理位置方格鑲嵌*，這會套用到的資料行`geography`資料型別。  
  
> [!NOTE]  
>  空間索引的 **tessellation_scheme** 設定可以在 [sys.spatial_index_tessellations](/sql/relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql) 目錄檢視中看到。  
  
#### <a name="geometry-grid-tessellation-scheme"></a>幾何方格鑲嵌式配置  
 GEOMETRY_AUTO_GRID 鑲嵌是 `geometry` 和更新版本之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型的預設鑲嵌式配置。  GEOMETRY_GRID 鑲嵌是唯一適用於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中 geometry 資料類型的鑲嵌式配置。 本章節討論與處理空間索引相關之幾何方格鑲嵌的層面：支援的方法及週框方塊。  
  
> [!NOTE]  
>  您可以使用 [CREATE SPATIAL INDEX](/sql/t-sql/statements/create-spatial-index-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的 USING (GEOMETRY_AUTO_GRID/GEOMETRY_GRID) 子句來明確指定這個鑲嵌式配置。  
  
##### <a name="the-bounding-box"></a>週框方塊  
 幾何資料會佔據可以是無限的平面。 但是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，空間索引需要有限的空間。 若要建立要分解的有限空間，幾何方格鑲嵌式配置需要矩形 *「週框方塊」*(Bounding Box)。 週框方塊由四個座標定義`(` _x 最小_**，**_y-最小值_`)`並`(` _x-最大值_**，**_y-最大值_`)`，這些會儲存為空間索引的屬性。 這些座標表示以下項目：  
  
-   *x-min* 是週框方塊左下角的 X 座標。  
  
-   *y-min* 是左下角的 Y 座標。  
  
-   *x-max* 是右上角的 X 座標。  
  
-   *y-max* 是右上角的 Y 座標。  
  
> [!NOTE]  
>  這些座標是由 [CREATE SPATIAL INDEX](/sql/t-sql/statements/create-spatial-index-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的 BOUNDING_BOX 子句所指定。  
  
 `(` _X-min_**，**_y-min_ `)`並`(` _x-max_**，** _y 最大_`)`座標可決定的位置和維度的週框方塊。 週框方塊外面的空間會視為編號 0 的單一資料格。  
  
 空間索引會分解週框方塊內的空間。 方格階層的層級 1 方格會填滿此週框方塊。 若要將幾何物件放在方格階層中，空間索引會將此物件的座標與週框方塊座標相比較。  
  
 下圖顯示所定義的點`(` _x 最小_**，**_y 最小_`)`並`(` _x-最大值_ **，**_y 最大_`)`週框方塊座標。 方格階層的最上層會顯示為 4x4 方格。 為了說明起見，較低的層級會予以忽略。 週框方塊外面的空間是由零 (0) 所指示。 請注意，物件 'A' 有一部分延伸到方塊外面，而物件 'B' 則完全位於資料格 0 的方塊內。  
  
 ![顯示座標和資料格 0 的週框方塊。](../../database-engine/media/spndx-bb-4x4-objects.gif "顯示座標和資料格 0 的週框方塊。")  
  
 週框方塊會對應到應用程式空間資料的某個部分。 不論索引的週框方塊是否完整包含空間資料行內所儲存的資料，或是只包含一部分，這都取決於應用程式。 只有在完全位於週框方塊內之物件上的運算才會從空間索引獲益。 因此，若要從 `geometry` 資料行上的空間索引獲得最大的好處，您便需要指定包含所有或大多數物件的週框方塊。  
  
> [!NOTE]  
>  空間索引的方格密度可以在 [sys.spatial_index_tessellations](/sql/relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql) 目錄檢視的 bounding_box_xmin、bounding_box_ymin、bounding_box_xmax 和 bounding_box_ymax 資料行中看到。  
  
#### <a name="the-geography-grid-tessellation-scheme"></a>地理位置方格鑲嵌式配置  
 此鑲嵌式配置只會套用到 `geography` 資料行。 本章節摘要說明地理位置方格鑲嵌式配置所支援的方法，並討論測量的空間如何投射到平面上，然後將其分解成方格階層。  
  
> [!NOTE]  
>  您可以使用 [CREATE SPATIAL INDEX](/sql/t-sql/statements/create-spatial-index-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的 USING (GEOGRAPHY_AUTO_GRID/GEOGRAPHY_GRID) 子句來明確指定這個鑲嵌式配置。  
  
##### <a name="projection-of-the-geodetic-space-onto-a-plane"></a>將測量空間投射到平面上  
 `geography` 執行個體 (物件) 上的計算會將包含物件的空間視為測量的橢圓體。 若要分解此空間，地理位置方格鑲嵌式配置會將橢圓體的表面分成上半球和下半球，然後執行下列步驟：  
  
1.  將每一個半球投射到四邊形金字塔的 Facet。  
  
2.  將兩個金字塔扁平化。  
  
3.  聯結扁平化的金字塔，以形成非 Euclidean 平面。  
  
 下圖顯示三個步驟之分解程序的圖解檢視。 在金字塔中，點狀的線條代表每一個金字塔之四個 Facet 的界限。 步驟 1 和 2 說明此測量的橢圓體，使用綠色水平線來表示赤道經線，並使用一系列的綠色垂直線來表示幾條緯線。 步驟 1 顯示投射到兩個半球上的金字塔。 步驟 2 顯示扁平化的金字塔。 步驟 3 說明扁平化的金字塔在經過組合之後會形成一個平面，顯示投射的經線數目。 請注意，這些投射的線條會變直，而且長度會視其落於金字塔上的位置而有所不同。  
  
 ![將橢圓體投射到平面上](../../database-engine/media/spndx-geodetic-projection.gif "將橢圓體投射到平面上")  
  
 一旦空間投射到平面上，此平面就會分解成四層級的方格階層。 不同層級可使用不同的方格密度。 下圖顯示分解成 4x4 層級 1 方格之後的平面。 為了說明起見，方格階層的較低層級會予以忽略。 事實上，此平面會完整分解成四層的方格階層。 在分解程序完成之後，系統會從地理位置資料行逐列讀取地理位置資料，接著會針對每一個物件執行鑲嵌程序。  
  
 ![層級 1 地理位置方格](../../database-engine/media/spndx-geodetic-level1grid.gif "層級 1 地理位置方格")  
  
##  <a name="methods"></a> 空間索引支援的方法  
  
###  <a name="geometry"></a> 空間索引支援的幾何方法  
 在某些條件下，空間索引可支援下列集合導向的幾何方法：Stcontains （）、 stdistance （）、 stequals （）、 stintersects （）、 stoverlaps （）、 sttouches （） 和 stwithin （）。 為了獲得空間索引的支援，這些方法必須在查詢的 WHERE 或 JOIN ON 子句中使用，而且必須在下列一般形式的述詞內發生：  
  
 *geometry1*.*method_name*(*geometry2*)*comparison_operator**valid_number*  
  
 若要傳回非 null 結果， *geometry1* 和 *geometry2* 必須有相同的 [空間參考識別碼 (SRID)](../spatial/spatial-reference-identifiers-srids.md)。 否則，此方法會傳回 NULL。  
  
 空間索引支援下列述詞形式：  
  
-   *geometry1*.[STContains](/sql/t-sql/spatial-geometry/stcontains-geometry-data-type)(*geometry2*) = 1  
  
-   *geometry1*.[STDistance](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)(*geometry2*) < *number*  
  
-   *geometry1*.[STDistance](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)(*geometry2*) <= *number*  
  
-   *geometry1*.[STEquals](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)(*geometry2*)= 1  
  
-   *geometry1*.[STIntersects](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)(*geometry2*)= 1  
  
-   *geometry1.* [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type) *(geometry2) = 1*  
  
-   *geometry1*.[STTouches](/sql/t-sql/spatial-geometry/sttouches-geometry-data-type)(*geometry2*) = 1  
  
-   *geometry1*.[STWithin](/sql/t-sql/spatial-geometry/stwithin-geometry-data-type)(*geometry2*)= 1  
  
###  <a name="geography"></a> 空間索引支援的地理位置方法  
 在某些條件下，空間索引可支援下列集合導向的地理位置方法：STIntersects(),STEquals() 和 stdistance （）。 為了獲得空間索引的支援，這些方法必須在查詢的 WHERE 子句中使用，而且必須在下列一般形式的述詞內發生：  
  
 *geography1*.*method_name*(*geography2*)*comparison_operator**valid_number*  
  
 若要傳回非 null 結果， *geography1* 和 *geography2* 必須有相同的 [空間參考識別碼 (SRID)](../spatial/spatial-reference-identifiers-srids.md)。 否則，此方法會傳回 NULL。  
  
 空間索引支援下列述詞形式：  
  
-   *geography1*.[STIntersects](/sql/t-sql/spatial-geography/stintersects-geography-data-type)(*geography2*)= 1  
  
-   *geography1*.[STEquals](/sql/t-sql/spatial-geography/stequals-geography-data-type)(*geography2*)= 1  
  
-   *geography1*.[STDistance](/sql/t-sql/spatial-geography/stdistance-geography-data-type)(*geography2*) < *number*  
  
-   *geography1*.[STDistance](/sql/t-sql/spatial-geography/stdistance-geography-data-type)(*geography2*) <= *number*  
  
### <a name="queries-that-use-spatial-indexes"></a>使用空間索引的查詢  
 空間索引只有在 `WHERE` 子句中包含索引空間運算子的查詢中才受到支援。 例如，類似以下的語法：  
  
```  
[spatial object].SpatialMethod([reference spatial object]) [ = | < ] [const literal or variable]  
```  
  
 查詢最佳化工具了解空間運算的交換性 ( `@a.STIntersects(@b) = @b.STInterestcs(@a)` )。 但是，如果比較開頭未包含空間運算子，將不會使用空間索引 (例如 `WHERE 1 = spatial op` 將不會使用空間索引)。 若要使用空間索引，請重寫比較 (例如 `WHERE spatial op = 1`)。  
  
 就如同其他任何索引，當空間索引受支援時，將會根據成本選擇使用空間索引，這樣一來，查詢最佳化工具可能不會選擇使用空間索引，即便符合使用它的所有要求也是一樣。 使用執行程序表來了解是否使用了空間索引，並視需要提供強制使用所需之查詢計劃的查詢提示。  
  
 但是，只有在撰寫特定查詢語法時，最接近的查詢類型也才會支援空間索引。 適當的語法為：  
  
```  
SELECT TOP(K) [WITH TIES] *   
FROM <Table> AS T [WITH(INDEX(<SpatialIndex>))]  
WHERE <SpatialColumn>.STDistance(@reference_object) IS NOT NULL  
ORDER BY <SpatialColumn>.STDistance(@reference_object) [;]  
```  
  
## <a name="see-also"></a>另請參閱  
 [空間資料 &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
