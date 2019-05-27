---
title: 定義事實關聯性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4b49a078-6848-4286-bc71-cf4862d29064
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 726b5fa4295d68c5b74d4fb3cac711126a8e570b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66078567"
---
# <a name="defining-a-fact-relationship"></a>定義事實關聯性
  使用者有時候想要按事實資料表中的資料項目建立量值維度，或查詢事實資料表中的其他特定相關資訊，例如與特定銷售事實相關的發票號碼或訂單號碼。 當您依據這樣的事實資料表項目來定義維度時，這種維度稱為「事實維度」。 事實維度也稱為變質維度。 事實維度對於將相關事實資料表資料列 (例如，與特定發票號碼相關的所有資料列) 分組很有幫助。 雖然您可以將這項資訊放在關聯式資料庫的個別維度資料表中，但為這項資訊建立個別的維度資料表並無好處，因為維度資料表與事實資料表的成長速率一樣，只會建立重複資料和產生不必要的複雜性而已。  
  
 在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中，您可以決定是否要在 MOLAP 維度結構中重複事實維度資料來增加查詢效能，或是否要將事實維度定義成 ROLAP 維度，以犧牲查詢效能的代價來節省儲存空間。 當您以 MOLAP 儲存模式來儲存維度時，所有維度成員除了儲存在量值群組的資料分割外，還會以高度壓縮的 MOLAP 結構而儲存在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體。 當您儲存的維度使用 ROLAP 儲存模式時，只有維度定義會儲存在 MOLAP 結構的維度成員本身都會進行查詢，從基礎關聯式事實資料表查詢時間。 您可以依據事實維度查詢的頻率、一般查詢傳回的資料列數、查詢的效能和處理成本，來決定適當的儲存模式。 將維度定義為 ROLAP 並不需要所有使用該維度的 Cube 都以 ROLAP 儲存模式來儲存。 每個維度的儲存模式可獨立設定。  
  
 當您定義事實維度時，可在事實維度和量值群組之間定義事實關聯性。 下列條件約束適用於事實關聯性：  
  
-   資料粒度屬性必須是維度的索引鍵資料行，它會在維度和事實資料表的事實之間建立一對一關聯性。  
  
-   維度只能與單一量值群組之間有事實關聯性。  
  
> [!NOTE]  
>  另外，事實維度在每次更新到事實關聯性參考的量值群組之後必須累加更新。  
  
 如需詳細資訊，請參閱[維度關聯性](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)和[定義事實關聯性及事實關聯性屬性](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)。  
  
 在本主題的工作中，您會依據 [FactInternetSales] 事實資料表中的 [CustomerPONumber] 資料行來加入新的 Cube 維度。 接著會將這個新的 Cube 維度和 [網際網路銷售] 量值群組之間的關聯性定義為事實關聯性。  
  
## <a name="defining-the-internet-sales-orders-fact-dimension"></a>定義網際網路銷售訂單事實維度  
  
1.  在方案總管中，以滑鼠右鍵按一下 [維度]，然後按一下 [新增維度]。  
  
2.  在 [歡迎使用維度精靈] 頁面上，按一下 [下一步]。  
  
3.  在 [選取建立方法] 頁面上，確認已選取 [使用現有的資料表] 選項，然後按一下 [下一步]。  
  
4.  在 [指定來源資訊] 頁面上，確認已選取 [Adventure Works DW 2012] 資料來源檢視。  
  
5.  在 [主資料表] 清單中，選取 [InternetSales]。  
  
6.  在 [索引鍵資料行] 清單中，確認已列出 [SalesOrderNumber] 和 [SalesOrderLineNumber]。  
  
7.  在 [名稱資料行] 清單中，選取 [SalesOrderLineNumber]。  
  
8.  按一下 [下一步] 。  
  
9. 在 [選取相關資料表] 頁面上，清除所有資料表旁的核取方塊，然後按一下 [下一步]。  
  
10. 在 [選取維度屬性] 頁面上，按兩次標頭中的核取方塊，以便清除所有核取方塊。 [銷售訂單號碼] 屬性會維持選取狀態，因為它是索引鍵屬性。  
  
11. 選取 [客戶採購單號碼] 屬性，然後按一下 [下一步]。  
  
12. 在 [正在完成精靈] 頁面上，將名稱變更為 [網際網路銷售訂單的詳細資料]，然後按一下 [完成] 完成精靈。  
  
13. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
14. 在**屬性**窗格中的 維度設計師**Internet Sales Order Details**維度，並選取**Sales Order Number**，然後變更**名稱**到 屬性 視窗中的屬性 `Item Description.`  
  
15. 在  **NameColumn**屬性資料格中，按一下瀏覽按鈕 **（...）**.從 名稱資料行 對話方塊的 來源資料表 清單中，選取 Product、針對 來源資料行 選取 EnglishProductName，然後按一下 確定。  
  
16. 將 [SalesOrderNumber] 資料行從 [資料來源檢視] 窗格中的 [InternetSales] 資料表拖曳到 [屬性] 窗格，以這個方式將 [銷售訂單號碼] 屬性加入維度。  
  
17. 變更**名稱**屬性的新**Sales Order Number**屬性設定為`Order Number`，並將變更**OrderBy**屬性設**金鑰**.  
  
18. 在 [**階層**] 窗格中，建立**網際網路銷售訂單**使用者階層，其中包含`Order Number`和**項目描述**層級，並依此順序。  
  
19. 在 [屬性] 窗格，選取 [網際網路銷售訂單的詳細資料]，然後在 [屬性] 視窗中檢閱 [StorageMode] 屬性的值。  
  
     請注意，依預設，這個維度是儲存為 MOLAP 維度。 雖然將儲存模式變更為 ROLAP 可節省處理時間和儲存空間，但卻是以犧牲查詢效能為代價。 基於這個教學課程的目的，您將使用 MOLAP 做為儲存模式。  
  
20. 若要將新建立的維度加入 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 當作 Cube 維度，請切換至 [Cube 設計師]。 在 [Cube 結構] 索引標籤上，以滑鼠右鍵按一下 [維度] 窗格，然後選取 [加入 Cube 維度]。  
  
21. 在 [加入 Cube 維度] 對話方塊中，選取 [網際網路銷售訂單的詳細資料]，然後按一下 [確定]。  
  
## <a name="defining-a-fact-relationship-for-the-fact-dimension"></a>定義 Fact 維度的事實關聯性  
  
1.  在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 的 [Cube 設計師] 中，按一下 [維度使用方式] 索引標籤。  
  
     請注意，[網際網路銷售訂單的詳細資料] Cube 維度會自動設定為具有事實關聯性，正如其唯一圖示所示。  
  
2.  按一下 瀏覽按鈕 (**...**) 中**項目描述**交集處的資料格**網際網路銷售**量值群組和**Internet Sales Order Details**維度，為檢閱事實關聯性屬性。  
  
     此時會開啟 [定義關聯性] 對話方塊。 請注意，您不能設定任何這些屬性。  
  
     下圖顯示 [定義關聯性] 對話方塊中的事實關聯性屬性。  
  
     ![定義關聯性 對話方塊](../../2014/tutorials/media/l5-factrelationship-2.gif "定義關聯性對話方塊")  
  
3.  按一下 [取消]。  
  
## <a name="browsing-the-cube-by-using-the-fact-dimension"></a>使用 Fact 維度來瀏覽 Cube  
  
1.  在 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]，將所做的變更部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體及處理資料庫。  
  
2.  順利完成部署之後，針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube，按一下 [Cube 設計師] 的 [瀏覽器] 索引標籤，然後按一下 [重新連接] 按鈕。  
  
3.  從 [資料] 窗格中清除所有量值和階層，然後將 [網際網路銷售 - 銷售量] 量值加入 [資料] 窗格的資料區域。  
  
4.  在 [中繼資料] 窗格中，依序展開 [客戶]、[位置]、[客戶地理位置]、[成員]、[所有客戶]、[澳大利亞]、[昆士蘭]、[布里斯本]、[4000]，以滑鼠右鍵按一下 [Adam Powell]，然後按一下 [加入至篩選]。  
  
     以篩選方式限制傳回給單一客戶的銷售訂單，可讓使用者向下鑽研大型事實資料表的基礎詳細資料，而不致使查詢效能有重大損失。  
  
5.  將 [網際網路銷售訂單的詳細資料] 維度中的 [網際網路銷售訂單] 使用者定義階層加入 [資料] 窗格的資料列區域。  
  
     請注意，銷售訂單號碼和 Adam Powell 對應的網際網路銷售量會出現在 [資料] 窗格中。  
  
     下圖顯示先前步驟所產生的結果。  
  
     ![維度的網際網路銷售-銷售量](../../2014/tutorials/media/l5-factrelationship-3.gif "維度的網際網路銷售-銷售量")  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [定義多對多關聯性](../analysis-services/lesson-5-3-defining-a-many-to-many-relationship.md)  
  
## <a name="see-also"></a>另請參閱  
 [維度關聯性](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [定義事實關聯性及事實關聯性屬性](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)  
  
  
