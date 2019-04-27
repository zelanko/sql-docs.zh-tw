---
title: 定義多對多關聯性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 7bebb174-148c-4cbb-a285-2f6d536a16d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2c05e45f5641c2d325c5e7d05472e3881ee7c807
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728764"
---
# <a name="defining-a-many-to-many-relationship"></a>定義多對多關聯性
  定義維度時，通常每一個事實只聯結到一個維度成員，而單一維度成員可以與許多不同事實相關聯。 例如，每個客戶可以有許多張訂單，但是每張訂單只會屬於單一客戶。 在關聯式資料庫詞彙中，這稱為「一對多關聯性」。 不過，有時候單一事實可聯結到多個維度成員。 在關聯式資料庫詞彙中，這稱為「多對多關聯性」。 例如，客戶進行採購有許多原因，而採購原因可能與多個採購相關聯。 聯結資料表是用來定義與每項採購相關的銷售原因。 從這樣的關聯性建構的 [銷售原因] 維度會有多個成員與單一銷售交易有關。 當維度與事實資料表無直接相關時，多對多維度會將維度模型可擴展到典型星形結構描述之外，來支援複雜分析。  
  
 在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中，您會透過指定一個聯結到維度資料表的中繼事實資料表，在維度和量值群組之間定義多對多關聯性。 中繼事實資料表再聯結到該事實資料表所聯結的中繼維度資料表。 中繼事實資料表與關聯性中維度資料表之間的多對多關聯性，以及中繼事實資料表與中繼維度之間的多對多關聯性，會在主要維度成員與關聯性所指定之量值群組的量值之間建立多對多關聯性。 若要透過中繼量值群組在維度與量值群組之間定義多對多關聯性，中繼量值群組必須和原始量值群組共用一或多個維度。  
  
 多對多維度的值是相異加總，也就是說，這些值最多只會彙總一次到 [所有成員] 中。  
  
> [!NOTE]  
>  為了支援多對多維度關聯性，必須定義主索引鍵-外部索引鍵關聯性中涉及的所有資料表之間的資料來源檢視。 否則，當您在 [Cube 設計師] 的 [維度使用方式] 索引標籤中建立關聯性時，將無法選取正確的中繼量值群組。  
  
 如需詳細資訊，請參閱[維度關聯性](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)和[定義多對多關聯性及多對多關聯性屬性](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)。  
  
 在這個主題的工作中，您會定義 [銷售原因] 維度和 [銷售原因] 量值群組，而且會在 [銷售原因] 維度和 [網際網路銷售] 量值群組之間透過 [銷售原因] 量值群組來定義多對多關聯性。  
  
## <a name="adding-required-tables-to-the-data-source-view"></a>將必要資料表加入資料來源檢視中  
  
1.  請針對 **Adventure Works DW 2012** 資料來源檢視，開啟資料來源檢視設計師。  
  
2.  以滑鼠右鍵按一下任何一處**圖表組合管理**窗格中，按一下**新圖表**，並指定`Internet Sales Order Reasons`做為新圖表的名稱。  
  
3.  將 [InternetSales] 資料表從 [資料表] 窗格拖曳至 [圖表] 窗格。  
  
4.  以滑鼠右鍵按一下 [圖表] 窗格中的任何位置，然後按一下 [新增/移除資料表]。  
  
5.  在 [新增/移除資料表] 對話方塊中，將 [DimSalesReason] 資料表和 [FactInternetSalesReason] 資料表新增至 [包含的物件] 清單，然後按一下 [確定]。  
  
     請注意，因為基礎關聯式資料庫中定義這些關聯性主索引鍵-外部索引鍵之間的關聯性相關的資料表會自動建立。 如果這些關聯性未定義在基礎關聯式資料庫中，您必須在資料來源檢視中定義它們。  
  
6.  在 [格式] 功能表上，指向 [自動配置]，然後按一下 [圖表]。  
  
7.  在 [屬性] 視窗中，變更**FriendlyName**屬性**DimSalesReason**資料表`SalesReason`，然後變更**FriendlyName**屬性**FactInternetSalesReason**資料表`InternetSalesReason`。  
  
8.  在 [資料表] 窗格中，展開 [InternetSalesReason (dbo.FactInternetSalesReason)]，並按一下 [SalesOrderNumber]，然後在 [屬性] 視窗中檢閱這個資料行的 [DataType] 屬性。  
  
     請注意， **SalesOrderNumber** 資料行的資料類型是字串資料類型。  
  
9. 檢閱中的其他資料行的資料類型`InternetSalesReason`資料表。  
  
     請注意，這份資料表的其他兩個資料行的資料類型是數值資料類型。  
  
10. 在 [資料表] 窗格中，以滑鼠右鍵按一下 [InternetSalesReason (dbo.FactInternetSalesReason)]，然後按一下 [瀏覽資料]。  
  
     請注意，每一份訂單內的每一個行號，都有一個索引鍵值來識別行項目的採構原因，如下圖所示。  
  
     ![若要找出用於購買產品的銷售原因索引鍵值](../../2014/tutorials/media/l5-many-to-many-1.gif "機碼值來識別用於購買產品的銷售原因")  
  
## <a name="defining-the-intermediate-measure-group"></a>定義中繼量值群組  
  
1.  請針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube，切換到 [Cube 設計師]，然後按一下 [Cube 結構] 索引標籤。  
  
2.  以滑鼠右鍵按一下 [量值] 窗格中的任何位置，然後按一下 [新增量值群組]。 如需詳細資訊，請參閱 [在多維度模型中建立量值和量值群組](multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)。  
  
3.  在 **新的量值群組**對話方塊中，選取`InternetSalesReason`中**從資料來源檢視中選取資料表**清單，然後再按**確定**。  
  
     請注意，[網際網路銷售原因] 量值群組現在出現在 [量值] 窗格中。  
  
4.  展開 [網際網路銷售原因] 量值群組。  
  
     請注意，對這個新量值群組只定義了單一量值，即 [網際網路銷售原因計數] 量值。  
  
5.  選取 [網際網路銷售原因計數]，並在 [屬性] 視窗中檢閱這個量值的屬性。  
  
     請注意，這個量值的 [AggregateFunction] 屬性是定義為 [計數] 而不是 [總和]。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 選擇**計數**因為基礎資料類型是字串資料類型。 基礎事實資料表中的其他兩個資料行並未選取做為量值，因為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 偵測到它們是數值索引鍵而不是實際量值。 如需詳細資訊，請參閱[定義局部加總行為](multidimensional-models/define-semiadditive-behavior.md)。  
  
6.  在 [屬性] 視窗中，將 [網際網路銷售原因計數] 量值的 [可見] 屬性變更為 **False**。  
  
     這個量值的唯一作用是將您接下來要定義的 [銷售原因] 維度聯結到 [網際網路銷售] 量值群組。 使用者不會直接瀏覽這個量值。  
  
     下圖顯示 [網際網路銷售原因計數] 量值的屬性。  
  
     ![網際網路銷售原因計數 量值的屬性](../../2014/tutorials/media/l5-many-to-many-2.gif "網際網路銷售原因計數 量值的屬性")  
  
## <a name="defining-the-many-to-many-dimension"></a>定義多對多維度  
  
1.  在方案總管中，以滑鼠右鍵按一下 [維度]，然後按一下 [新增維度]。  
  
2.  在 [歡迎使用維度精靈] 頁面上，按一下 [下一步]。  
  
3.  在 [選取建立方法] 頁面上，確認已選取 [使用現有的資料表] 選項，然後按一下 [下一步]。  
  
4.  在 [指定來源資訊] 頁面上，確認已選取 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012 資料來源檢視。  
  
5.  在 **主資料表**清單中，選取`SalesReason`。  
  
6.  在 [索引鍵資料行] 清單中，確認已列出 [SalesReasonKey]。  
  
7.  在 [名稱資料行] 清單中，選取 [SalesReasonName]。  
  
8.  按一下 [下一步] 。  
  
9. 在 [選取維度屬性] 頁面上，系統會自動選取 [銷售原因索引鍵] 屬性，因為它是索引鍵屬性。 選取旁邊的核取方塊**銷售原因類型**屬性，其名稱變更成`Sales Reason Type`，然後按一下**下一步**。  
  
10. 在 [正在完成精靈] 頁面上，按一下 [完成] 建立 [銷售原因] 維度。  
  
11. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
12. 在 **屬性**窗格的 維度設計師**銷售原因**維度，並選取**銷售原因索引鍵**，然後變更**名稱**在 屬性 視窗中的屬性 `Sales Reason.`  
  
13. 在 **階層**窗格中的 維度設計師 中，建立**銷售原因**使用者階層，其中包含`Sales Reason Type`層級和**銷售原因**層級，請在此順序。  
  
14. 在 屬性 視窗中，定義`All Sales Reasons`做為值**AllMemberName**的銷售原因 階層的屬性。  
  
15. 定義`All Sales Reasons`做為值**AttributeAllMemberName**的銷售原因 維度的屬性。  
  
16. 若要將新建立的維度新增至 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 當成 Cube 維度，請切換至 [Cube 設計師]。 在 [Cube 結構] 索引標籤上，以滑鼠右鍵按一下 [維度] 窗格，然後選取 [新增 Cube 維度]。  
  
17. 在 [新增 Cube 維度] 對話方塊中，選取 [銷售原因]，然後按一下 [確定]。  
  
18. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="defining-the-many-to-many-relationship"></a>定義多對多關聯性  
  
1.  請針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube，切換到 [Cube 設計師]，然後按一下 [維度使用方式] 索引標籤。  
  
     請注意，[銷售原因] 維度與 [網際網路銷售原因] 量值群組之間有定義一般關聯性，但是與 [網際網路銷售] 或 [轉售商銷售] 量值群組之間則沒有定義任何關聯性。 也請注意，[網際網路銷售訂單的詳細資料] 維度與 [網際網路銷售原因] 維度之間有定義一般關聯性，而後者又與 [網際網路銷售] 量值群組具有「事實關聯性」。 如果這個維度不存在 (或是另一個同時與 [網際網路銷售原因] 和 [網際網路銷售] 量值群組具有關聯性的維度不存在)，您就無法定義多對多關聯性。  
  
2.  在 [網際網路銷售] 量值群組和 [銷售原因] 維度的交集處，按一下資料格，然後按一下瀏覽按鈕 (**…**)。  
  
3.  在 [定義關聯性] 對話方塊中，選取 [選取關聯性類型] 清單中的 [多對多]。  
  
     您必須定義連接 [銷售原因] 維度與 [網際網路銷售] 量值群組的中繼量值群組。  
  
4.  在 [中繼量值群組] 清單中，選取 [網際網路銷售原因]。  
  
     下圖顯示 [定義關聯性] 對話方塊中的變更。  
  
     ![定義關聯性 對話方塊](../../2014/tutorials/media/l5-many-to-many-3.gif "定義關聯性對話方塊")  
  
5.  按一下 [確定] 。  
  
     請注意代表 [銷售原因] 維度和 [網際網路銷售] 量值群組之間關聯性的多對多圖示。  
  
## <a name="browsing-the-cube-and-the-many-to-many-dimension"></a>瀏覽 Cube 與多對多維度  
  
1.  在 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
2.  順利完成部署之後，針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube，切換到 [Cube 設計師] 的 [瀏覽器] 索引標籤，然後按一下 [重新連接]。  
  
3.  將 [網際網路銷售 - 銷售量] 量值新增至 [資料] 窗格的資料區域。  
  
4.  將 [銷售原因] 維度中的 [銷售原因] 使用者定義階層新增至 [資料] 窗格的資料列區域。  
  
5.  在 [中繼資料] 窗格中，依序展開 [客戶]、[位置]、[客戶地理位置]、[成員]、[所有客戶] 和 [澳大利亞]，並以滑鼠右鍵按一下 [昆士蘭]，然後按一下 [新增至篩選]。  
  
6.  展開每個成員`Sales Reason Type`層級，以檢閱幣值與 Queensland 中的客戶採購每一個原因相關聯[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)]在網際網路上的產品。  
  
     請注意，與每一個銷售原因有關聯的總計累加超過總銷售量。 這是因為有些客戶針對其採購引用了多個原因。  
  
     下圖顯示 [Cube 設計師] 的 [篩選] 窗格和 [資料] 窗格。  
  
     ![篩選和資料窗格的 Cube 設計師](../../2014/tutorials/media/l5-many-to-many-5.gif "Cube 設計師 的篩選和資料窗格")  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [在量值群組內定義維度資料粒度](../analysis-services/lesson-5-4-defining-dimension-granularity-within-a-measure-group.md)  
  
## <a name="see-also"></a>另請參閱  
 [在資料來源檢視設計工具中使用圖表 &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [維度關聯性](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [定義多對多關聯性及多對多關聯性屬性](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)  
  
  
