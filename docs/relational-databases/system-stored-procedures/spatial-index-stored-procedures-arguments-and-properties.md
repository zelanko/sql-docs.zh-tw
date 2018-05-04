---
title: 引數和屬性的空間索引預存程序 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], stored procedures
ms.assetid: ee26082b-c0ed-40ff-b5ad-f5f6b00f0475
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6c95b04711d4fd370058e2ca9e785cd25665050c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spatial-index-stored-procedures---arguments-and-properties"></a>空間索引預存程序的引數和屬性
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  此空間記錄空間索引預存程序的引數和屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
 如需特定空間索引預存程序的語法，請參閱下列主題：  
  
-   [sp_help_spatial_geometry_index &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="arguments"></a>引數  
 [  **@tabname =**] **'***tabname***'**  
 這是已指定空間索引之資料表的限定或非限定名稱。  
  
 只有在指定限定資料表時，才會用到引號。 如果提供其中包括資料庫名稱的完整名稱，資料庫名稱就必須是目前資料庫的名稱。 *tabname*是**nvarchar**(776)，沒有預設值。  
  
 [  **@indexname =** ] **'***indexname***'**  
 這是所指定空間索引的名稱。 *indexname*是**sysname**沒有預設值。  
  
 [  **@verboseoutput =** ] **'***verboseoutput***'**  
 這是要傳回之屬性名稱和值的範圍。  
  
 0 = 核心屬性  
  
 \>0 = 所有屬性  
  
 *verboseoutput*是**tinyint**沒有預設值。  
  
 [  **@query_sample =** ] **'***query_sample***'**  
 這是可用來測試索引有用性的代表查詢範例。 可能是代表物件或查詢視窗。 *query_sample*是**幾何**沒有預設值。  
  
 [  **@xml_output =** ] **'***xml_output***'**  
 這是以 XML 片段傳回結果集的輸出參數。 *xml_output*是**xml**沒有預設值。  
  
## <a name="properties"></a>屬性  
 設定**@verboseoutput** = 0 以傳回核心屬性，如顯示在下表中。**@verboseoutput** > 0 以傳回空間索引的所有屬性。  
  
 **Base_Table_Rows**  
 基底資料表中的資料列數。 值是**bigint**。  
  
 **Bounding_Box_xmin**  
 X-min 週框方塊屬性之空間索引的**幾何**型別。 這個屬性值是 NULL **geography**型別。 值是**float**。  
  
 **Bounding_Box_ymin**  
 Y-min 週框方塊屬性之空間索引的**幾何**型別。 這個屬性值是 NULL **geography**型別。 值是**float**。  
  
 **Bounding_Box_xmax**  
 X-max 週框方塊屬性之空間索引的**幾何**型別。 這個屬性值是 NULL **geography**型別。 值是**float**。  
  
 **Bounding_Box_ymax**  
 Y-max 週框方塊屬性之空間索引的**幾何**型別。 這個屬性值是 NULL **geography**型別。 值是**float**。  
  
 **Grid_Size_Level_1**  
 空間索引的層級 1 方格密度：  
  
 16 為 LOW  
  
 64 為 MEDIUM  
  
 256 為 HIGH  
  
 值是**int**。  
  
 **Grid_Size_Level_2**  
 空間索引的層級 2 方格密度：  
  
 16 為 LOW  
  
 64 為 MEDIUM  
  
 256 為 HIGH  
  
 值是**int**。  
  
 **Grid_Size_Level_3**  
 空間索引的層級 3 方格密度：  
  
 16 為 LOW  
  
 64 為 MEDIUM  
  
 256 為 HIGH  
  
 值是**int**。  
  
 **Grid_Size_Level_4**  
 空間索引的層級 4 方格密度：  
  
 16 為 LOW  
  
 64 為 MEDIUM  
  
 256 為 HIGH  
  
 值是**int**。  
  
 **Cells_Per_Object**  
 每個物件 (索引屬性) 的資料格數目。 值是**int**。  
  
 **Total_Primary_Index_Rows**  
 索引中資料列的數目。 值是**bigint**。  
  
 **Total_Primary_Index_Pages**  
 索引中頁面的數目。 值是**bigint**。  
  
 **Average_Number_Of_Index_Rows_Per_Base_Row**  
 索引資料列的數目 / 基底資料表資料列的數目。 值是**bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**  
 指出代表查詢範例是否落的週框方塊外面**幾何**索引到根資料格 （層級 0 資料格）。 這可能是 0 (不在層級 0 資料格中) 或 1。 如果是在層級 0 資料格中，則調查的索引不是查詢範例的適當索引。 這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level0_In_Index**  
 資料格的索引物件的鑲嵌於層級 0 的執行個體數目 (的週框方塊外的根資料格，**幾何**)。 這是核心屬性。 值是**bigint**。  
  
 如**幾何**索引，這會是因為索引的週框方塊小於資料網域。 次要的篩選條件，如果查詢視窗部分落外部週框方塊，而且會降低索引效能，可能需要大量的層級 0 物件 (例如， **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**為 1)。 如果查詢視窗落在週框方塊內，則層級 0 的物件數目如果很多，反而可能會改善索引的效能。  
  
 NULL 和空白的執行個體會計算層級 0 的數目，但不會影響效能。 層級 0 的資料格會與基底資料表的 NULL 和空白執行個體一樣多。 如**geography**層級 0 的索引，會有許多儲存格以 NULL 和空白執行個體 + 1 資料格，，因為查詢範例會計算為 1。  
  
 **Total_Number_Of_ObjectCells_In_Level1_In_Index**  
 資料格執行個體的索引物件的鑲嵌為層級 1 的有效位數的數目。 這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level2_In_Index**  
 資料格執行個體的索引物件的鑲嵌為層級 2 的有效位數的數目。 這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level3_In_Index**  
 資料格執行個體的索引物件的鑲嵌為層級 3 的有效位數的數目。 這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level4_In_Index**  
 鑲嵌為層級 4 精度的索引物件的資料格執行個體數目。 這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level1_In_Index**  
 完全涵蓋了在鑲嵌層級 1 物件，因此對於是該物件內部的資料格數目。 （Cell_attributevalue 是 2）。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level2_In_Index**  
 完全涵蓋了在鑲嵌層級 2 物件，因此對於是該物件內部的資料格數目。 （Cell_attribute 值是 2）。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level3_In_Index**  
 完全涵蓋了在鑲嵌層級 3 的物件，因此對於是該物件內部的資料格數目。 （Cell_attribute 值是 2）。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level4_In_Index**  
 在鑲嵌層級 4 由物件完全涵蓋 (因此屬於該物件內部) 的資料格數目  （Cell_attribute 值是 2）。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level1_In_Index**  
 在鑲嵌層級 1 物件所會交集的資料格數目。 （Cell_attribute 值是 1）。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level2_In_Index**  
 在鑲嵌層級 2 物件所會交集的資料格數目。 （Cell_attribute 值是 1）。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level3_In_Index**  
 會透過物件鑲嵌層級 3 交集的資料格數目。 （Cell_attribute 值是 1）。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level4_In_Index**  
 與鑲嵌層級 4 的物件交叉的資料格數目  （Cell_attribute 值是 1）。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_For_QuerySample**  
 指出查詢範例是否落在週框方塊外的根資料格 0 中，但觸及該方塊。 這是核心屬性。 值是**bigint**。  
  
> [!NOTE]  
>  這項資訊僅適用於判斷是否有週框方塊剛好略過的物件。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_In_Index**  
 觸及週框方塊的層級 0 物件數目  (Cell_attribute 值是 0)。值是**bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level1_In_Index**  
 觸及鑲嵌層級 1 方格資料格界限的物件資料格數目。 (Cell_attribute 值是 0)。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level2_In_Index**  
 觸及鑲嵌層級 2 方格資料格界限的物件資料格數目。 (Cell_attribute 值是 0)。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level3_In_Index**  
 觸及鑲嵌層級 3 方格資料格界限的物件資料格數目。 (Cell_attribute 值是 0)。這是核心屬性。 值是**bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level4_In_Index**  
 觸及鑲嵌層級 4 的方格資料格界限的物件資料格數目  (Cell_attribute 值是 0)。這是核心屬性。 值是**bigint**。  
  
 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 方格總區域 (分葉資料格總計) 的百分比，此方格包含物件所涵蓋的分葉資料格。  
  
 例如，某物件鑲嵌於 4 個不同方格層級的 10 個資料格，涵蓋區域相當於 100 個分葉資料格的總計。 假設此物件完全涵蓋了三個內部資料格， 這 3 個內部資料格所涵蓋的範圍相當於 42 個分葉資料格。 因此，所涵蓋區域的百分比為 42%。 這是用來測量索引中物件切割程度的好方法。  
  
 值是**float**。  
  
 **Intersecting_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 與相同**Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**，但這些是部分涵蓋的資料格。 值是**float**。  
  
 **Border_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 與相同**Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage** ，但這些是框線資料格。 值是**float**。  
  
 **Average_Cells_Per_Object_Normalized_To_Leaf_Grid**  
 每個物件正規化為分葉資料格的平均資料格數。 這可以提供物件空間大小或者物件大小的指示。 值是**float**。  
  
 **Average_Objects_PerLeaf_GridCell**  
 索引的疏鬆性。 每個分葉儲存格的平均物件數目。 值是**float**。  
  
 **Number_Of_SRIDs_Found**  
 在索引和資料行中的唯一 SRID 數目。 值是**int**。  
  
 因為資料行可以包含一個以上的 SRID，而且不同 SRID 的物件絕不會交叉，所以 SRID 的數目代表索引選擇性。  
  
 **Width_Of_Cell_In_Level1**  
 索引方格中資料格的寬度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Width_Of_Cell_In_Level2**  
 索引方格中資料格的寬度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Width_Of_Cell_In_Level3**  
 索引方格中資料格的寬度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Width_Of_Cell_In_Level4**  
 索引方格中資料格的寬度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Height_Of_Cell_In_Level1**  
 索引方格中資料格的高度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Height_Of_Cell_In_Level2**  
 索引方格中資料格的高度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Height_Of_Cell_In_Level3**  
 索引方格中資料格的高度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Height_Of_Cell_In_Level4**  
 索引方格中資料格的高度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Area_Of_Cell_In_Level1**  
 索引方格中資料格的區域屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Area_Of_Cell_In_Level2**  
 索引方格中資料格的區域屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Area_Of_Cell_In_Level3**  
 索引方格中資料格的區域屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **Area_Of_Cell_In_Level4**  
 索引方格中資料格的區域屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值是**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level1**  
 週框方塊的層級 1 資料格的涵蓋範圍的百分比。 值是**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level2**  
 週框方塊的層級 2 資料格的涵蓋範圍的百分比。 值是**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level3**  
 週框方塊的層級 3 資料格的涵蓋範圍的百分比。 值是**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level4**  
 層級 4 資料格之週框方塊的涵蓋百分比。 值是**float**。  
  
 **Number_Of_Rows_Selected_By_Primary_Filter**  
 主要篩選所選取的資料列數目。 這是核心屬性。 值是**bigint。**  
  
 **Number_Of_Rows_Selected_By_Internal_Filter**  
 內部篩選所選取的資料列數目。 這些資料列不會呼叫次要篩選。 這是核心屬性。 值是**bigint。**  
  
 傳回的數字只是適用於**STintersects**。  
  
 **Number_Of_Times_Secondary_Filter_Is_Called**  
 呼叫次要篩選的次數。 這是核心屬性。 值是**bigint。**  
  
 **Percentage_Of_Rows_NotSelected_By_Primary_Filter**  
 如果基底資料表中有 N 個資料列，而主要篩選選取了 P 個資料列，則這會傳回 (N-P)/N 做為百分比。 這是核心屬性。 值是**浮點數。**  
  
 **Percentage_Of_Primary_Filter_Rows_Selected_By_internal_Filter**  
 如果主要篩選選取了 P 個資料列，而內部篩選選取了 S 個資料列，則這會傳回 S/P 做為百分比。 百分比愈高，索引愈能避免較耗費效能的次要篩選。 這是核心屬性。 值是**浮點數。**  
  
 **Number_Of_Rows_Output**  
 由查詢輸出的資料列數目。 這是核心屬性。 值是**bigint。**  
  
 **Internal_Filter_Efficiency**  
 如果 O 為輸出的資料列數目，則這會傳回 S/O 做為百分比。 這是核心屬性。 值是**浮點數。**  
  
 **Primary_Filter_Efficiency**  
 如果 P 的資料列會選取主要篩選和 O 為輸出資料列數目，此 returnsO/P 以百分比表示。 主要篩選的效率愈高，次要篩選必須處理的誤判愈少。 這是核心屬性。 值是**浮點數。**  
  
## <a name="permissions"></a>Permissions  
 使用者必須是成員**公用**角色。 需要在伺服器和物件上具有 READ ACCESS 權限。 這適用於所有空間索引預存程序。  
  
## <a name="remarks"></a>備註  
 包含 NULL 值的屬性不會包含在傳回集合中。  
  
## <a name="examples"></a>範例  
 如需範例，請參閱下列主題：  
  
-   [sp_help_spatial_geometry_index &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="requirements"></a>需求  
  
## <a name="see-also"></a>另請參閱  
 [空間索引預存程序&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [XQuery 基本概念](../../xquery/xquery-basics.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
