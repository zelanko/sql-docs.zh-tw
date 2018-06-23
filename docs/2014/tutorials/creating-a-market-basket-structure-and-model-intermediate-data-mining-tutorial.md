---
title: 建立購物籃結構和模型 （中繼資料採礦教學課程） |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 659b7a4e-f687-44d9-a60a-86490ccbf90f
caps.latest.revision: 48
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 957a55114e5a4fb756c63b63779eed3fbfb5f95b
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312596"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>建立購物籃結構和模型 (中繼資料採礦教學課程)
  現在您已經建立了資料來源檢視，接著要使用資料採礦精靈建立新的採礦結構。 在這項工作中，您將根據 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯分析演算法建立一個採礦結構和一個採礦模型。  
  
> [!NOTE]  
>  如果出現 vAssocSeqLineItems 無法當做巢狀資料表使用的錯誤訊息，請返回本課程的上一個工作，並務必從 vAssocSeqLineItems 資料表 (多方) 拖曳至 vAssocSeqOrders 資料表 (一方)，藉以建立多對一聯結。 您也可以用滑鼠右鍵按一下聯結線，編輯資料表之間的關聯性。  
  
### <a name="to-create-an-association-mining-structure"></a>若要建立關聯採礦結構  
  
1.  在 [方案總管] 中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，以滑鼠右鍵按一下**採礦結構**選取**新的採礦結構**以開啟 資料採礦精靈。  
  
2.  在 **[歡迎使用資料採礦精靈]** 頁面上，按 **[下一步]**。  
  
3.  在**選取定義方法**頁面上，確認**從現有的關聯式資料庫或資料倉儲**已選取，然後按一下**下一步**。  
  
4.  在**建立資料採礦結構**頁面的 **您想要使用哪一種資料採礦技術？**，選取**Microsoft 關聯規則**從清單中，然後按一下**下一步**。 **選取資料來源檢視**頁面隨即出現。  
  
5.  選取**訂單**下**可用的資料來源檢視**，然後按一下 **下一步**。  
  
6.  在**指定資料表類型**vAssocSeqLineItems 資料表的資料列中的頁面上，選取**巢狀**核取方塊，然後在巢狀的資料表 vAssocSeqOrders 列中，選取**案例**核取方塊。 按 [下一步] 。  
  
7.  在**指定培訓資料**頁面上，清除任何可能會核取方塊。 選取以設定 vAssocSeqOrders 案例資料表、 索引鍵**金鑰**OrderNumber 旁的核取方塊。  
  
     由於購物籃分析的目的是要判斷哪些產品包含在單一交易中，您不必使用 **[customerkey]** 欄位。  
  
8.  選取以設定 vAssocSeqLineItems 巢狀資料表索引鍵**金鑰**Model 旁的核取方塊。 **輸入**當您執行此動作也會自動選取核取方塊。 選取**可預測**核取方塊`Model`以及。  
  
     在購物籃模型中，您不在意購物籃中的產品順序，因此您不應該包含**LineNumber**做為巢狀資料表索引鍵。 您可以使用**LineNumber**做為索引鍵，只能在模型中在時序很重要。 您將在第 4 課建立一個使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時序群集演算法的模型。  
  
9. 選取 IncomeGroup 和 Region 左邊的核取方塊，但不要選取其他任何選項。 檢查最左邊的資料行時，會將資料行加入到結構中供您日後參考，但是不會用於模型中。 您的選擇應該如下所示：  
  
     ![對話方塊應該看起來](../../2014/tutorials/media/tutorial-configassocmodel.gif "外觀對話方塊")  
  
10. 按 [下一步] 。  
  
11. 在**指定資料行的內容和資料類型**頁面上，檢閱選取項目，這應該是下表所示，然後按一下 **下一步**。  
  
    |[資料行]|內容類型|資料類型|  
    |-------------|------------------|---------------|  
    |IncomeGroup|Discrete|文字|  
    |Order Number|索引鍵|文字|  
    |Region|Discrete|文字|  
    |vAssocSeqLineItems|||  
    |[模型]|索引鍵|文字|  
  
12. 在**建立測試設定**頁面上，選項的預設值**測試資料的百分比**是百分之 30。 將這變更為**0**。 按 [下一步] 。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會提供不同的圖表來測量模型精確度。 不過，有些圖表類型 (例如增益圖和交叉驗證報告)，是專為分類和估計而設計。 這些方法不支援用於關聯式預測。  
  
13. 在**正在完成精靈**頁面上，於**採礦結構名稱**，型別`Association`。  
  
14. 在**採礦模型名稱**，型別`Association`。  
  
15. 選取的選項**允許使用鑽研**，然後按一下 **完成**。  
  
     資料採礦設計師會開啟以顯示`Association`您剛才建立的採礦結構。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [修改及處理購物籃模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 關聯分析演算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [內容類型&#40;資料採礦&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  