---
title: 建立目標的郵寄採礦模型結構 （基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a9c67f29-0c47-4a5a-862b-db0f5213c2c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 112b45f2d5797d6797903661de0376bd4d316c6a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087708"
---
# <a name="creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial"></a>建立目標郵寄採礦模型結構 (基本資料採礦教學課程)
  建立目標郵寄狀況的第一個步驟是，利用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的資料採礦精靈來建立新的採礦結構和決策樹採礦模型。  
  
 在這項工作，您會設定新的採礦結構，並加入初始採礦模型為基礎[!INCLUDE[msCoName](../includes/msconame-md.md)]決策樹演算法。 若要建立此結構，您會先選取資料表和檢視表，然後識別哪些資料行將用於定型，哪些資料行將用於測試。  
  
### <a name="to-create-a-mining-structure-for-the-targeted-mailing-scenario"></a>若要建立目標郵寄案例的採礦結構  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下**採礦結構**，然後選取**New Mining Structure&lt**即可啟動資料採礦精靈。  
  
2.  在 **[歡迎使用資料採礦精靈]** 頁面上，按 **[下一步]**。  
  
3.  在 [**選取定義方法**頁面上，確認**從現有的關聯式資料庫或資料倉儲**已選取，然後按一下**下一步]**。  
  
4.  在 **建立資料採礦結構**頁面的 **您想要使用哪一種資料採礦技術？**，選取**Microsoft Decision Trees**。  
  
    > [!NOTE]  
    >  如果出現找不到資料採礦演算法的警告，可能無法正確設定專案屬性。 當專案嘗試從 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器擷取資料採礦演算法的清單，而且找不到伺服器時，就會出現這個警告。 根據預設，[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]會使用**localhost**做為伺服器。 如果您要使用不同的執行個體或具名執行個體，您必須變更專案屬性。 如需詳細資訊，請參閱 <<c0> [ 建立 Analysis Services 專案&#40;資料採礦基本教學課程&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)。</c0>  
  
5.  按 [下一步] 。  
  
6.  在 **選取資料來源檢視**頁面上，於**可用的資料來源檢視**窗格中，選取**目標郵寄**。 您可以按一下**瀏覽**來檢視資料來源檢視中的資料表，然後按一下**關閉**返回精靈。  
  
7.  按 [下一步] 。  
  
8.  上**指定資料表類型**頁面上，選取核取方塊**案例**資料行，以作為案例資料表，然後按一下 [vtargetmail**下一步]**。 您之後將會使用 ProspectiveBuyer 資料表進行測試，現在請先忽略。  
  
9. 在上**指定培訓資料** 頁面上，您會指出至少一個可預測資料行、 一個索引鍵資料行，和一個輸入資料行，為您的模型。 選取核取方塊，在**Predictable**中的資料行**BikeBuyer**資料列。  
  
    > [!NOTE]  
    >  請注意視窗底部的警告。 您無法巡覽至下一個頁面，直到您選取至少一個**輸入**一個**Predictable**資料行。  
  
10. 按一下 [**建議**來開啟**建議相關資料行**] 對話方塊。  
  
     **建議**已選取至少一個可預測屬性時，已啟用 按鈕。 **建議相關資料行**對話方塊列出可預測資料行中，最密切相關的資料行，並依其相互關聯，以可預測的屬性排列屬性。 系統會自動選取具有重大相互關聯性的資料行 (信心大於 95%)，使其包含在模型中。  
  
     檢閱建議，，然後按**取消**toignore 建議。  
  
    > [!NOTE]  
    >  如果您按一下**確定**，所有列出的建議會標示為在精靈中的輸入資料行。 如果您僅同意其中某些建議，就必須手動變更其值。  
  
11. 確認中的核取方塊**金鑰**中選取資料行**CustomerKey**資料列。  
  
    > [!NOTE]  
    >  如果資料來源檢視中的來源資料表指出索引鍵，資料採礦精靈會自動選擇這個資料行來做為模型的索引鍵。  
  
12. 選取核取方塊後**輸入**以下資料列中的資料行。 您可以核取多個資料行，其方式是反白顯示某個資料格範圍並按下 CTRL 鍵，然後同時選取核取方塊。  
  
    -   **存留期**  
  
    -   **CommuteDistance**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **Gender**  
  
    -   **[Geographykey]**  
  
    -   **HouseOwnerFlag**  
  
    -   **MaritalStatus**  
  
    -   **NumberCarsOwned**  
  
    -   **NumberChildrenAtHome**  
  
    -   **Region**  
  
    -   **TotalChildren**  
  
    -   **YearlyIncome**  
  
13. 在頁面上最左邊的資料行上，選取以下資料列中的核取方塊。  
  
    -   **AddressLine1**  
  
    -   **AddressLine2**  
  
    -   **DateFirstPurchase**  
  
    -   **EmailAddress**  
  
    -   **FirstName**  
  
    -   **lastName**  
  
     請確定這些資料列只有在左邊的資料行中才有核取記號。 這些資料行將會加入到您的結構中，但是不會併入模型中。 但是在建立此模型之後，這些資料行將可用於鑽研和測試。 如需有關鑽研的詳細資訊，請參閱 <<c0> [ 鑽研查詢&#40;資料採礦&#41;</c0>](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
14. 按 [下一步] 。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [指定資料類型和內容類型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [指定資料表類型&#40;資料採礦精靈&#41;](../../2014/analysis-services/specify-table-types-data-mining-wizard.md)   
 [資料採礦設計師](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 決策樹演算法](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)  
  
  
