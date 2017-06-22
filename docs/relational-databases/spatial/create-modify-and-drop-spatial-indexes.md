---
title: "建立、修改及卸除空間索引 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexes [SQL Server], creating
- spatial indexes [SQL Server], dropping
- spatial indexes [SQL Server], creating
- indexes [SQL Server], dropping
- indexes [SQL Server], modifying
- spatial indexes [SQL Server], modifying
ms.assetid: 00c1b927-8ec5-44cf-87c2-c8de59745735
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 57aebfb8b20a0e6c751deb4b9914f8122b3c3cd3
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="create-modify-and-drop-spatial-indexes"></a>建立、修改及卸除空間索引
  空間索引可以更有效率地在 **geometry** 或 **geography** 資料類型的資料行 (「空間資料行」) 上執行某些作業。 可以在空間資料行上指定一個以上的空間索引。 這對於類似在單一資料行上為不同鑲嵌式參數建立索引會很有用處。  
  
 建立空間索引有一些限制。 如需詳細資訊，請參閱本主題中的 [空間索引的限制](#restrictions) 。  
  
> [!NOTE]  
>  如需空間索引與分割區和檔案群組之關聯性的資訊，請參閱 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)中的＜備註＞一節。  
  
##  <a name="creating"></a> 建立、修改和卸除空間索引  
  
###  <a name="create"></a> 建立空間索引  
 **使用 Transact-SQL 建立空間索引**  
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
  
 **使用 Management Studio 的 [新增索引] 對話方塊建立空間索引**  
 ##### <a name="to-create-a-spatial-index-in-management-studio"></a>若要在 Management Studio 中建立空間索引  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 [資料庫]，再展開含有指定索引之資料表所在的資料庫，然後展開 [資料表]。  
  
3.  展開您想要建立索引的資料表。  
  
4.  以滑鼠右鍵按一下 [索引]，然後選取 [新增索引]。  
  
5.  在 [索引名稱] 欄位中，輸入索引的名稱。  
  
6.  在 [索引類型] 下拉式清單中，選取 [空間]。  
  
7.  若要指定您要建立索引的空間資料行，請按一下 [加入]。  
  
8.  在 [從 *\<資料表名稱>* 選取資料行] 對話方塊中，選取對應的核取方塊來選取 **geometry** 或 **geography** 類型的資料行。 任何其他的空間資料行就會變成無法編輯。 如果您想要選取不同的空間資料行，就必須先清除目前選取的資料行。 完成後，請按一下 **[確定]**。  
  
9. 在 [索引鍵資料行] 方格中確認您的資料行選取。  
  
10. 在 [索引屬性] 對話方塊的 [選取頁面] 窗格中，按一下 [空間]。  
  
11. 在 [空間] 頁面上，指定您想要用於索引之空間屬性的值。  
  
     當您在 **geometry** 類型資料行上建立索引時，您必須指定週框方塊的 **(***X-min***,***Y-min***)** 和 **(***X-max***,***Y-max***)** 座標。 如果是 **geography** 類型資料行上的索引，在您指定**地理方格**鑲嵌式配置之後，週框方塊欄位會變成唯讀，因為地理方格鑲嵌式不會使用週框方塊。  
  
     您可以選擇性地針對 [每一物件的資料格] 欄位及鑲嵌式配置的任何方格密度等級指定非預設值。 每一物件的資料格預設數目為 16 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 或 8 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) 或更高，而預設方格密度是 [中] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)])。  
  
     您可以針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的鑲嵌式配置選取 GEOMETRY_AUTO_GRID 或 GEOGRAPHY_AUTO_GRID。 當您選取 GEOMETRY_AUTO_GRID 或 GEOGRAPHY_AUTO_GRID 時，就會停用 [層級 1]、[層級 2]、[層級 3] 和 [層級 4] 方格密度選項。  
  
     如需這些屬性的詳細資訊，請參閱 [索引屬性 F1 說明](../../relational-databases/indexes/index-properties-f1-help.md)。  
  
12. 按一下 **[確定]**。  
  
> [!NOTE]  
>  若要在相同或不同空間資料行上建立另一個空間索引，請重複上述步驟。  
  
  
 **使用 Management Studio 的資料表設計工具建立空間索引**  
 ##### <a name="to-create-a-spatial-index-in-table-designer"></a>在資料表設計工具中建立空間索引  
  
1.  在物件總管中，以滑鼠右鍵按一下要建立空間索引的資料表，然後按一下 [設計]。  
  
     資料表會在 [資料表設計工具] 中開啟。  
  
2.  為此索引選取 **geometry** 或 **geography** 資料行。  
  
3.  從 [資料表設計工具] 功能表中，按一下 [空間索引]。  
  
4.  在 [空間索引] 對話方塊中，按一下 [加入]。  
  
5.  在 [Selected Spatial Index (選取的空間索引)] 清單中選取新的索引，並在右邊方格中設定此空間索引的屬性。 如需這些屬性的資訊，請參閱[空間索引對話方塊 &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/4d84239a-68c7-4aa2-8602-2b51dd07260f)。  
  
  
###  <a name="alter"></a> 改變空間索引  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
    > [!IMPORTANT]  
    >  若要變更空間索引特定的選項 (例如 BOUNDING_BOX 或 GRID)，您可以使用指定 DROP_EXISTING = ON 的 CREATE SPATIAL INDEX 陳述式，或是卸除此空間索引並建立新的索引。 如需範例，請參閱 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)中的＜備註＞一節。  
  
-   [修改索引](../../relational-databases/indexes/modify-an-index.md)  
  
-   [將現有的索引移至不同的檔案群組](../../relational-databases/indexes/move-an-existing-index-to-a-different-filegroup.md)  
  
  
###  <a name="drop"></a> 卸除空間索引  
 **使用 Transact-SQL 卸除空間索引**  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 **若要使用 Management Studio 卸除索引**  
 [刪除索引](../../relational-databases/indexes/delete-an-index.md)  
  
 **使用 Management Studio 的資料表設計工具卸除空間索引**  
 ##### <a name="to-drop-a-spatial-index-in-table-designer"></a>在資料表設計工具中卸除空間索引  
  
1.  在物件總管中，以滑鼠右鍵按一下具有您要刪除之空間索引的資料表，然後按一下 [設計]。  
  
     資料表會在 [資料表設計工具] 中開啟。  
  
2.  從 [資料表設計工具] 功能表中，按一下 [空間索引]。  
  
     [空間索引] 對話方塊隨即開啟。  
  
3.  在 [Selected Spatial Index (選取的空間索引)] 資料行中，按一下要刪除的索引。  
  
4.  按一下 **[刪除]**。  
  
  
##  <a name="restrictions"></a> 空間索引的限制  
 空間索引只能建立在 **geometry** 或 **geography**類型的資料行上。  
  
### <a name="table-and-view-restrictions"></a>資料表和檢視表限制  
 空間索引只能定義在具有主索引鍵的資料表上。 資料表上主索引鍵資料行的最大數目是 15。  
  
 索引鍵記錄大小的最大值是 895 個位元組。 較大的值會引發錯誤。  
  
> [!NOTE]  
>  當空間索引定義於資料表上時，將無法變更主索引鍵中繼資料。  
  
 不能在索引檢視表上指定空間索引。  
  
### <a name="multiple-spatial-index-restrictions"></a>多個空間索引的限制  
 在支援之資料表的任何空間資料行上最多可以建立 249 個空間索引。 例如，要針對單一資料行中的不同鑲嵌式參數建立索引時，在相同空間資料行上建立一個以上的空間索引可能會很有用處。  
  
 您一次只能建立一個空間索引。  
  
### <a name="spatial-indexes-and-process-parallelism"></a>空間索引和處理序平行處理原則  
 索引建立可以使用可用的處理序平行處理原則。  
  
### <a name="version-restrictions"></a>版本限制  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中所導入的空間鑲嵌無法複寫至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。 您必須在需要與 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 資料庫進行回溯相容性時，使用空間索引的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 空間鑲嵌式。  
  
  
## <a name="see-also"></a>另請參閱  
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
