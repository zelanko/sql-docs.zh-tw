---
title: 建立時序群集採礦模型結構 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e9339227-6c2e-4c4b-8be2-8c1960bc4a8d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b7f4f543952fd86cf6c3c66f9f4b2c51019b1869
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273482"
---
# <a name="creating-a-sequence-clustering-mining-model-structure-intermediate-data-mining-tutorial"></a>建立時序群集採礦模型結構 (中繼資料採礦教學課程)
  建立時序群集採礦模型的第一個步驟就是使用資料採礦精靈，根據 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時序群集演算法來建立新的採礦結構和採礦模型。  
  
 您將會使用與購物籃分析相同的資料來源檢視，但是您會加入一個包含 `sequence` 識別碼的資料行。 在此案例中，時序表示客戶將項目加入到購物籃的順序。  
  
 您也會加入某些資料行，這些資料行會在其中一個模型內使用，以根據人口統計資料來分組客戶。  
  
### <a name="to-create-a-sequence-clustering-structure-and-model"></a>若要建立時序群集結構和模型  
  
1.  在 [方案總管] 中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，以滑鼠右鍵按一下**採礦結構**，然後選取**New Mining Structure&lt**。  
  
2.  在 **[歡迎使用資料採礦精靈]** 頁面上，按 **[下一步]** 。  
  
3.  在 [**選取定義方法**頁面上，確認**從現有的關聯式資料庫或資料倉儲**已選取，然後按一下**下一步]** 。  
  
4.  在 **建立資料採礦結構**頁面上，確認選項**建立採礦結構與採礦模型**已選取。 接下來，按一下下拉式清單選項時，**您想要使用哪一種資料採礦技術？** ，然後選取**Microsoft 時序群集**。 按一下 [下一步]  。  
  
     **選取資料來源檢視**頁面隨即出現。 底下**可用的資料來源檢視**，選取`Orders`。  
  
     Orders 是您用於購物籃分析案例的相同資料來源檢視。 如果您尚未建立這個資料來源檢視，請參閱[加入具有巢狀資料表的資料來源檢視&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)。  
  
5.  按一下 [下一步]  。  
  
6.  在 **指定資料表類型**頁面上，選取**案例**旁的核取方塊**vAssocSeqOrders**資料表，然後選取**巢狀**核取方塊旁**vAssocSeqLineItems**資料表。 按一下 [下一步]  。  
  
    > [!NOTE]  
    >  如果當您選取時，就會發生錯誤**案例**或是**巢狀**核取方塊，它可能是資料來源檢視中的聯結不正確。 巢狀的資料表中， **vAssocSeqLineItems**，必須連接到案例資料表**vAssocSeqOrders**由多對一聯結。 您可以用滑鼠右鍵按一下聯結線並反轉聯結的方向，藉以編輯關聯性。 如需詳細資訊，請參閱 <<c0> [ 建立或編輯關聯性對話方塊&#40;Analysis Services-多維度資料&#41;](../../2014/analysis-services/create-or-edit-relationship-dialog-box-analysis-services-multidimensional-data.md)。</c0>  
  
7.  在 **指定培訓資料**頁面上，選擇使用的資料行在模型中，選取核取方塊，如下所示：  
  
    -   **IncomeGroup**選取 **輸入**核取方塊。  
  
         這個資料行包含有關您可用於群集之客戶的有趣資訊。 您將會在第一個模型中使用它，然後在第二個模型中忽略它。  
  
    -   **OrderNumber**選取`Key`核取方塊。  
  
         此欄位將會當做案例資料表的識別碼或 `Key` 使用。 一般來說，您絕對不應該使用案例資料表的索引鍵欄位當做輸入，因為此索引鍵包含對於群集沒什麼用處的唯一值。  
  
    -   **區域**選取 **輸入**核取方塊。  
  
         這個資料行包含有關您可用於群集之客戶的有趣資訊。 您將會在第一個模型中使用它，然後在第二個模型中忽略它。  
  
    -   **LineNumber**選取 `Key`並**輸入**核取方塊。  
  
         **LineNumber**欄位會當做識別項用於巢狀資料表，或`Sequence Key`。 巢狀資料表的索引鍵永遠都必須用於輸入。  
  
    -   **模型**選取 **輸入**並**Predictable**核取方塊。  
  
     確認選取項目都正確無誤，然後按一下 [**下一步]** 。  
  
8.  在 [**指定資料行的內容和資料類型**頁面上，確認此方格有包含資料行、 內容類型和下表所示的資料類型，然後按一下**下一步]** 。  
  
    |資料表/資料行|內容類型|資料類型|  
    |---------------------|------------------|---------------|  
    |IncomeGroup|Discrete|Text|  
    |OrderNumber|Key|Text|  
    |Region|Discrete|Text|  
    |vAssocSeqLineItems|||  
    |Line Number|Key Sequence|長整數|  
    |[模型]|Discrete|Text|  
  
9. 在 [**建立測試集**頁面上，變更**測試資料的百分比**為 20，然後按一下**下一步]** 。  
  
10. 在上**完成精靈**頁面上，如**採礦結構名稱**，型別`Sequence Clustering with Region`。  
  
11. 針對**採礦模型名稱**，輸入`Sequence Clustering with Region`。  
  
12. 請檢查**允許使用鑽研**方塊，然後再按一下**完成**。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [處理時序群集模型](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦設計師](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 時序群集演算法](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)  
  
  
