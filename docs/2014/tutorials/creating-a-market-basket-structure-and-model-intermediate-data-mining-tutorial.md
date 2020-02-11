---
title: 建立購物籃結構和模型（元資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 659b7a4e-f687-44d9-a60a-86490ccbf90f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 207d82f740b7b5ff174e220e647d67d5bac7f9ea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63190819"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>建立購物籃結構和模型 (中繼資料採礦教學課程)
  現在您已經建立了資料來源檢視，接著要使用資料採礦精靈建立新的採礦結構。 在這項工作中，您將根據 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯分析演算法建立一個採礦結構和一個採礦模型。  
  
> [!NOTE]  
>  如果出現 vAssocSeqLineItems 無法當做巢狀資料表使用的錯誤訊息，請返回本課程的上一個工作，並務必從 vAssocSeqLineItems 資料表 (多方) 拖曳至 vAssocSeqOrders 資料表 (一方)，藉以建立多對一聯結。 您也可以用滑鼠右鍵按一下聯結線，編輯資料表之間的關聯性。  
  
### <a name="to-create-an-association-mining-structure"></a>若要建立關聯採礦結構  
  
1.  在的方案總管[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，以滑鼠右鍵按一下 [**採礦結構**]，然後選取 [新增] [**採礦結構**] 以開啟 [資料採礦嚮導]。  
  
2.  在 **[歡迎使用資料採礦精靈]** 頁面上，按 **[下一步]**。  
  
3.  在 [**選取定義方法**] 頁面上，確認已選取 [**從現有的關係資料庫或資料倉儲**]，然後按 **[下一步]**。  
  
4.  在 [**建立資料採礦結構**] 頁面上，于 [**您要使用哪一項資料採礦技術？**] 下，從清單中選取 [ **Microsoft 關聯規則**]，然後按 **[下一步]**。 [**選取資料來源視圖**] 頁面隨即出現。  
  
5.  在 [**可用的資料來源視圖**] 底下選取**訂單**，然後按 **[下一步]**。  
  
6.  在 [**指定資料表類型**] 頁面的 [vAssocSeqLineItems] 資料表的資料列中，選取 [**嵌套**] 核取方塊，然後在 [嵌套資料表 vAssocSeqOrders] 的資料列中選取 [**案例**] 核取方塊。 按 [下一步]  。  
  
7.  在 [**指定定型資料**] 頁面上，清除任何可能已核取的方塊。 選取 [OrderNumber] 旁的 [索引**鍵**] 核取方塊，以設定案例資料表的索引鍵（vAssocSeqOrders）。  
  
     因為購物籃分析的目的是要判斷哪些產品包含在單一交易中，所以您不需要使用**CustomerKey**欄位。  
  
8.  選取 [模型] 旁的 [索引**鍵**] 核取方塊，以設定 vAssocSeqLineItems 嵌套資料表的索引鍵。 當您執行此動作時，也會自動選取 [**輸入**] 核取方塊。 也請選取 [**可預測**] 核取方塊`Model` 。  
  
     在購物籃模型中，您不在意購物籃中的產品順序，因此您不應該將**LineNumber**納入為嵌套資料表的索引鍵。 在序列很重要的模型中，您只會使用**LineNumber**做為索引鍵。 您將在第 4 課建立一個使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時序群集演算法的模型。  
  
9. 選取 IncomeGroup 和 Region 左邊的核取方塊，但不要選取其他任何選項。 檢查最左邊的資料行時，會將資料行加入到結構中供您日後參考，但是不會用於模型中。 您的選擇應該如下所示：  
  
     ![對話方塊應有的外觀](../../2014/tutorials/media/tutorial-configassocmodel.gif "對話方塊應有的外觀")  
  
10. 按 [下一步]  。  
  
11. 在 [**指定欄位的內容和資料類型**] 頁面上，檢查選取專案，如下表所示，然後按 **[下一步]**。  
  
    |資料行|內容類型|資料類型|  
    |-------------|------------------|---------------|  
    |IncomeGroup|Discrete|Text|  
    |訂單編號|Key|Text|  
    |區域|Discrete|Text|  
    |vAssocSeqLineItems|||  
    |模型|Key|Text|  
  
12. 在 [**建立測試集**] 頁面上，[**測試資料的百分比**] 選項的預設值為30%。 將此變更為**0**。 按 [下一步]  。  
  
    > [!NOTE]  
    >  
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會提供不同的圖表來測量模型精確度。 不過，有些圖表類型 (例如增益圖和交叉驗證報告)，是專為分類和估計而設計。 這些方法不支援用於關聯式預測。  
  
13. 在 [**正在完成嚮導]** 頁面的 [**採礦結構名稱**] `Association`中，輸入。  
  
14. 在 [**採礦模型名稱**] `Association`中，輸入。  
  
15. 選取 [**允許深入流覽**] 選項，然後按一下 **[完成]**。  
  
     [資料採礦設計師] 隨即開啟`Association` ，以顯示您剛建立的「採礦結構」。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [修改和處理購物籃模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 關聯分析演算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [&#40;資料採礦&#41;的內容類型](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  
