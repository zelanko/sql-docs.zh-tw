---
title: 使用嵌套資料表加入資料來源視圖（中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a14cd7f1-7a10-4ec6-af6a-f5f0676a0308
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 648b9d561ae340b67ed5e2d1aa878969e5a3bc47
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62822773"
---
# <a name="adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial"></a>加入具有巢狀資料表的資料來源檢視 (中繼資料採礦教學課程)
  若要建立購物籃模型，您必須使用支援關聯資料的資料來源檢視。 此資料來源檢視也會用於時序群集狀況。  
  
 此資料來源視圖與您可能已使用的其他人不同，因為它包含一個*嵌套的資料表*。 「*嵌套資料表*」是一個資料表，其中包含有關案例資料表中單一資料列的多個資料列資訊。 例如，如果您的模型分析客戶的購買行為，您通常會將每一個客戶具有唯一資料列的資料表做為案例資料表使用。 不過，每個客戶可能都會購買多個項目，而您可能想要分析購買的順序，或是通常會一起購買的產品。 若要以邏輯方式在模型中表示這些購買項目，您可以將另一個資料表加入到來源檢視中，其中會列出每個客戶的購買項目資料。  
  
 這個巢狀購買資料表與客戶資料表之間具有多對一的關聯性。 巢狀資料表可能包含每一個客戶的許多資料列，而每一個資料列都包含已購買的單一產品，可能還包含所下訂單的其他資訊、下訂單時的價格，或是任何適用的促銷。 您可以使用巢狀資料表中的資訊當做模型的輸入，或是當做可預測的屬性。  
  
 在這一課，您將進行下列工作：  
  
-   您可以將資料來源視圖加入至[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]資料來源。  
  
-   將案例和巢狀資料表加入至此檢視。  
  
-   指定案例與巢狀資料表之間的多對一關聯性。  
  
    > [!NOTE]  
    >  . 務必完全遵循所描述的程序，正確地指定案例資料表與巢狀資料表之間的關聯性，以避免在處理模型時發生錯誤。  
  
-   定義資料行如何在模型中使用。  
  
 如需使用案例和嵌套資料表以及如何選擇嵌套資料表索引鍵的詳細資訊，請參閱[&#40;Analysis Services 資料採礦&#41;的嵌套資料表](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)。  
  
### <a name="to-add-a-data-source-view"></a>若要加入資料來源檢視  
  
1.  在方案總管中，以滑鼠右鍵按一下 [**資料來源視圖**]，然後選取 [**新增資料來源視圖**]。  
  
     此時會開啟資料來源檢視精靈。  
  
2.  在 [歡迎使用資料來源檢視精靈]**** 頁面上，按 [下一步]****。  
  
3.  在 [**選取資料來源**] 頁面的 [**關聯式資料來源**] 底下， [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]選取您在「基本資料採礦」教學課程中建立的資料來源。 按 [下一步]  。  
  
4.  在 [**選取資料表和 Views** ] 頁面上，選取下列資料表，然後按一下向右箭號，將它們包含在 [新資料來源] 視圖中：  
  
    -   `vAssocSeqOrders`  
  
    -   `vAssocSeqLineItems`  
  
5.  按 [下一步]  。  
  
6.  在 [**正在完成嚮導]** 頁面上，預設會將 [資料來源[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]] 視圖命名為。 將 [名稱] `Orders`變更為，然後按一下 **[完成]**。  
  
     [資料來源視圖設計工具] `Orders`隨即開啟，並顯示 [資料來源] 視圖。  
  
### <a name="to-create-a-relationship-between-tables"></a>若要建立資料表之間的關聯性  
  
1.  在資料來源檢視設計師中，放置這兩個資料表，好讓它們水平對齊左邊的 vAssocSeqLineItems 資料表和右邊的 vAssocSeqOrders 資料表。  
  
2.  選取 [vAssocSeqLineItems] 資料表中的 [ **OrderNumber** ] 資料行。  
  
3.  將資料行拖曳至 [vAssocSeqOrders] 資料表，並將它放在 [ **OrderNumber** ] 資料行上。  
  
    > [!IMPORTANT]  
    >  請務必將 [ **OrderNumber** ] 資料行從 vAssocSeqLineItems 的 nested 資料表（代表聯結的許多端）拖曳至 vAssocSeqOrders 案例資料表（代表聯結的一端）。  
  
     VAssocSeqLineItems 和 vAssocSeqOrders 資料表之間現在有新的*多對一關聯*性。 如果您已經正確聯結這些資料表，資料來源檢視應顯示如下：  
  
     ![巢狀和案例資料表之間必須是多對一聯結](../../2014/tutorials/media/dsv-nestedjoin-illustration.gif "巢狀和案例資料表之間必須是多對一聯結")  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立購物籃結構和模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [元資料採礦教學課程 &#40;Analysis Services-資料採礦&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [&#40;Analysis Services 的採礦結構-資料採礦&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [採礦模型 &#40;Analysis Services - 資料採礦&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
