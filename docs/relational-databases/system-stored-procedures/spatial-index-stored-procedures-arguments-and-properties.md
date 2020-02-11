---
title: 空間索引預存程式的引數和屬性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], stored procedures
ms.assetid: ee26082b-c0ed-40ff-b5ad-f5f6b00f0475
author: stevestein
ms.author: sstein
ms.openlocfilehash: 82b906be4568b15a18c55247532bf35b6cd939a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "69028900"
---
# <a name="spatial-index-stored-procedures---arguments-and-properties"></a>空間索引預存程式-引數和屬性
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  此空間記錄空間索引預存程序的引數和屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
 如需特定空間索引預存程序的語法，請參閱下列主題：  
  
-   [sp_help_spatial_geometry_index &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="arguments"></a>引數  
`[ @tabname = ] 'tabname'`這是已指定空間索引之資料表的完整或非限定名稱。  
  
 只有在指定限定資料表時，才會用到引號。 如果提供其中包括資料庫名稱的完整名稱，資料庫名稱就必須是目前資料庫的名稱。 *tabname*是**Nvarchar**（776），沒有預設值。  
  
`[ @indexname = ] 'indexname'`這是所指定空間索引的名稱。 *indexname*是**sysname** ，沒有預設值。  
  
`[ @verboseoutput = ] 'verboseoutput'`這是要傳回之屬性名稱和值的範圍。  
  
 0 = 核心屬性  
  
 \>0 = 所有屬性  
  
 *verboseoutput*是**Tinyint** ，沒有預設值。  
  
`[ @query_sample = ] 'query_sample'`是可用於測試索引實用性的代表性查詢範例。 可能是代表物件或查詢視窗。 *query_sample*是沒有預設值的**geometry** 。  
  
`[ @xml_output = ] 'xml_output'`這是在 XML 片段中傳回結果集的輸出參數。 *xml_output*是沒有預設值的**xml** 。  
  
## <a name="properties"></a>屬性  
 設定** \@verboseoutput** = 0 以傳回核心屬性，如下表所示：verboseoutput > 0，以傳回空間索引的所有屬性。 ** \@ **  
  
 **Base_Table_Rows**  
 基底資料表中的資料列數。 值為**Bigint**。  
  
 **Bounding_Box_xmin**  
 **Geometry**類型之空間索引的 X 最小周框方塊屬性。 **Geography**類型的這個屬性值是 Null。 值為**float**。  
  
 **Bounding_Box_ymin**  
 **Geometry**類型的空間索引的 Y 最小周框方塊屬性。 **Geography**類型的這個屬性值是 Null。 值為**float**。  
  
 **Bounding_Box_xmax**  
 **Geometry**類型空間索引的 X-最大周框方塊屬性。 **Geography**類型的這個屬性值是 Null。 值為**float**。  
  
 **Bounding_Box_ymax**  
 **Geometry**類型的空間索引的 Y-最大周框方塊屬性。 **Geography**類型的這個屬性值是 Null。 值為**float**。  
  
 **Grid_Size_Level_1**  
 空間索引的層級1方格密度：  
  
 16 為 LOW  
  
 64 為 MEDIUM  
  
 256 為 HIGH  
  
 值為**int**。  
  
 **Grid_Size_Level_2**  
 空間索引的層級2格線密度：  
  
 16 為 LOW  
  
 64 為 MEDIUM  
  
 256 為 HIGH  
  
 值為**int**。  
  
 **Grid_Size_Level_3**  
 空間索引的層級3方格密度：  
  
 16 為 LOW  
  
 64 為 MEDIUM  
  
 256 為 HIGH  
  
 值為**int**。  
  
 **Grid_Size_Level_4**  
 空間索引的層級 4 方格密度：  
  
 16 為 LOW  
  
 64 為 MEDIUM  
  
 256 為 HIGH  
  
 值為**int**。  
  
 **Cells_Per_Object**  
 每個物件 (索引屬性) 的資料格數目。 值為**int**。  
  
 **Total_Primary_Index_Rows**  
 索引中資料列的數目。 值為**Bigint**。  
  
 **Total_Primary_Index_Pages**  
 索引中頁面的數目。 值為**Bigint**。  
  
 **Average_Number_Of_Index_Rows_Per_Base_Row**  
 索引資料列的數目 / 基底資料表資料列的數目。 值為**Bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**  
 指出代表查詢範例是否落在**幾何**索引的周框方塊之外，以及根資料格（層級0資料格）。 這可能是 0 (不在層級 0 資料格中) 或 1。 如果是在層級 0 資料格中，則調查的索引不是查詢範例的適當索引。 這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level0_In_Index**  
 在層級0中鑲嵌之索引物件的資料格實例數目（**幾何**的周框方塊外的根資料格）。 這是核心屬性。 值為**Bigint**。  
  
 對於**幾何**索引，如果索引的周框方塊小於資料網域，就會發生這種情況。 如果查詢視窗的部分超出周框方塊之外，層級0中的物件數量可能會需要次要篩選，而且會降低索引效能（例如， **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**為1）。 如果查詢視窗落在週框方塊內，則層級 0 的物件數目如果很多，反而可能會改善索引的效能。  
  
 NULL 和空白的執行個體會計算層級 0 的數目，但不會影響效能。 層級 0 的資料格會與基底資料表的 NULL 和空白執行個體一樣多。 對於**地理位置**索引，層級0的資料格數目會與 Null 和空的實例 + 1 個數據格相同，因為查詢範例會計算為1。  
  
 **Total_Number_Of_ObjectCells_In_Level1_In_Index**  
 以層級1精確度鑲嵌之索引物件的資料格實例數目。 這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level2_In_Index**  
 以層級2精確度鑲嵌之索引物件的資料格實例數目。 這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level3_In_Index**  
 以層級3精確度鑲嵌之索引物件的資料格實例數目。 這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level4_In_Index**  
 鑲嵌為層級 4 精度的索引物件的資料格執行個體數目。 這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level1_In_Index**  
 在鑲嵌層級1的物件完全涵蓋的資料格數目，因此是物件的內部。 （Cell_attributevalue 是2）。這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level2_In_Index**  
 在鑲嵌層級2的物件完全涵蓋的資料格數目，因此是物件的內部。 （Cell_attribute 值是2）。這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level3_In_Index**  
 在鑲嵌層級3的物件完全涵蓋的資料格數目，因此是物件的內部。 （Cell_attribute 值是2）。這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level4_In_Index**  
 在鑲嵌層級 4 由物件完全涵蓋 (因此屬於該物件內部) 的資料格數目  （Cell_attribute 值是2）。這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level1_In_Index**  
 鑲嵌層級1的物件所交集的資料格數目。 （Cell_attribute 值是1）。這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level2_In_Index**  
 在鑲嵌層級2與物件相交的資料格數目。 （Cell_attribute 值是1）。這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level3_In_Index**  
 在鑲嵌層級3與物件相交的資料格數目。 （Cell_attribute 值是1）。這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level4_In_Index**  
 與鑲嵌層級 4 的物件交叉的資料格數目  （Cell_attribute 值是1）。這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_For_QuerySample**  
 指出查詢範例是否落在週框方塊外的根資料格 0 中，但觸及該方塊。 這是核心屬性。 值為**Bigint**。  
  
> [!NOTE]  
>  這項資訊僅適用於判斷是否有週框方塊剛好略過的物件。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_In_Index**  
 觸及週框方塊的層級 0 物件數目  （Cell_attribute 值為0。） 值為**Bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level1_In_Index**  
 觸及鑲嵌層級1之方格資料格界限的物件資料格數目。 （Cell_attribute 值為0。）這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level2_In_Index**  
 觸及鑲嵌層級2之方格資料格界限的物件資料格數目。 （Cell_attribute 值為0。）這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level3_In_Index**  
 觸及鑲嵌層級3之方格資料格界限的物件資料格數目。 （Cell_attribute 值為0。）這是核心屬性。 值為**Bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level4_In_Index**  
 觸及鑲嵌層級 4 的方格資料格界限的物件資料格數目  （Cell_attribute 值為0。）這是核心屬性。 值為**Bigint**。  
  
 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 方格總區域 (分葉資料格總計) 的百分比，此方格包含物件所涵蓋的分葉資料格。  
  
 例如，某物件鑲嵌於 4 個不同方格層級的 10 個資料格，涵蓋區域相當於 100 個分葉資料格的總計。 假設此物件完全涵蓋了三個內部資料格， 這 3 個內部資料格所涵蓋的範圍相當於 42 個分葉資料格。 因此，所涵蓋區域的百分比為 42%。 這是用來測量索引中物件切割程度的好方法。  
  
 值為**float**。  
  
 **Intersecting_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 與**Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**相同，不同之處在于這些是部分涵蓋的資料格。 值為**float**。  
  
 **Border_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 與**Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**相同，不同之處在于這些是框線儲存格。 值為**float**。  
  
 **Average_Cells_Per_Object_Normalized_To_Leaf_Grid**  
 每個物件正規化為分葉資料格的平均資料格數。 這可以提供物件空間大小或者物件大小的指示。 值為**float**。  
  
 **Average_Objects_PerLeaf_GridCell**  
 索引的疏鬆性。 每個分葉儲存格的平均物件數目。 值為**float**。  
  
 **Number_Of_SRIDs_Found**  
 在索引和資料行中的唯一 SRID 數目。 值為**int**。  
  
 因為資料行可以包含一個以上的 SRID，而且不同 SRID 的物件絕不會交叉，所以 SRID 的數目代表索引選擇性。  
  
 **Width_Of_Cell_In_Level1**  
 索引方格中資料格的寬度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Width_Of_Cell_In_Level2**  
 索引方格中資料格的寬度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Width_Of_Cell_In_Level3**  
 索引方格中資料格的寬度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Width_Of_Cell_In_Level4**  
 索引方格中資料格的寬度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Height_Of_Cell_In_Level1**  
 索引方格中資料格的高度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Height_Of_Cell_In_Level2**  
 索引方格中資料格的高度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Height_Of_Cell_In_Level3**  
 索引方格中資料格的高度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Height_Of_Cell_In_Level4**  
 索引方格中資料格的高度屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Area_Of_Cell_In_Level1**  
 索引方格中資料格的區域屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Area_Of_Cell_In_Level2**  
 索引方格中資料格的區域屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Area_Of_Cell_In_Level3**  
 索引方格中資料格的區域屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **Area_Of_Cell_In_Level4**  
 索引方格中資料格的區域屬性。 度量單位是由索引提供，而且相依於索引資料的 SRID。 值為**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level1**  
 層級1資料格的周框方塊涵蓋範圍百分比。 值為**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level2**  
 層級2資料格的周框方塊涵蓋範圍百分比。 值為**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level3**  
 由層級3資料格涵蓋周框方塊的百分比。 值為**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level4**  
 層級 4 資料格之週框方塊的涵蓋百分比。 值為**float**。  
  
 **Number_Of_Rows_Selected_By_Primary_Filter**  
 主要篩選所選取的資料列數目。 這是核心屬性。 值為**Bigint。**  
  
 **Number_Of_Rows_Selected_By_Internal_Filter**  
 內部篩選所選取的資料列數目。 這些資料列不會呼叫次要篩選。 這是核心屬性。 值為**Bigint。**  
  
 傳回的數位僅適用于**STintersects**。  
  
 **Number_Of_Times_Secondary_Filter_Is_Called**  
 呼叫次要篩選的次數。 這是核心屬性。 值為**Bigint。**  
  
 **Percentage_Of_Rows_NotSelected_By_Primary_Filter**  
 如果基底資料表中有 N 個資料列，而主要篩選選取了 P 個資料列，則這會傳回 (N-P)/N 做為百分比。 這是核心屬性。 值為**float。**  
  
 **Percentage_Of_Primary_Filter_Rows_Selected_By_internal_Filter**  
 如果主要篩選選取了 P 個資料列，而內部篩選選取了 S 個資料列，則這會傳回 S/P 做為百分比。 百分比愈高，索引愈能避免較耗費效能的次要篩選。 這是核心屬性。 值為**float。**  
  
 **Number_Of_Rows_Output**  
 由查詢輸出的資料列數目。 這是核心屬性。 值為**Bigint。**  
  
 **Internal_Filter_Efficiency**  
 如果 O 為輸出的資料列數目，則這會傳回 S/O 做為百分比。 這是核心屬性。 值為**float。**  
  
 **Primary_Filter_Efficiency**  
 如果主要篩選選取了 P 個數據列，而 O 是輸出的資料列數目，則此 returnsO/P 會以百分比表示。 主要篩選的效率愈高，次要篩選必須處理的誤判愈少。 這是核心屬性。 值為**float。**  
  
## <a name="permissions"></a>權限  
 使用者必須是**public**角色的成員。 需要在伺服器和物件上具有 READ ACCESS 權限。 這適用於所有空間索引預存程序。  
  
## <a name="remarks"></a>備註  
 包含 NULL 值的屬性不會包含在傳回集合中。  
  
## <a name="examples"></a>範例  
 如需範例，請參閱下列主題：  
  
-   [sp_help_spatial_geometry_index &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="requirements"></a>需求  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的空間索引預存程式](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [XQuery 基本概念](../../xquery/xquery-basics.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
