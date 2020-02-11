---
title: 建立目標郵寄採礦模型結構（基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9c67f29-0c47-4a5a-862b-db0f5213c2c9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2bd2e9d0decc730a59b63ee600bec2d080cc85fb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62856167"
---
# <a name="creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial"></a>建立目標郵寄採礦模型結構 (基本資料採礦教學課程)
  建立目標郵寄狀況的第一個步驟是，利用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的資料採礦精靈來建立新的採礦結構和決策樹採礦模型。  
  
 在這項工作中，您將設定新的「採礦結構」，並根據[!INCLUDE[msCoName](../includes/msconame-md.md)]決策樹演算法新增初始的「採礦模型」。 若要建立此結構，您會先選取資料表和檢視表，然後識別哪些資料行將用於定型，哪些資料行將用於測試。  
  
### <a name="to-create-a-mining-structure-for-the-targeted-mailing-scenario"></a>若要建立目標郵寄案例的採礦結構  
  
1.  在方案總管中，以滑鼠右鍵按一下 [**採礦結構**]，然後選取 [新增] [**採礦結構**] 來啟動資料採礦嚮導。  
  
2.  在 **[歡迎使用資料採礦精靈]** 頁面上，按 **[下一步]**。  
  
3.  在 [**選取定義方法**] 頁面上，確認已選取 [**從現有的關係資料庫或資料倉儲**]，然後按 **[下一步]**。  
  
4.  在 [**建立資料採礦結構**] 頁面上，于 [**您要使用哪一項資料採礦技術？**] 底下，選取 [ **Microsoft 決策樹**]。  
  
    > [!NOTE]  
    >  如果出現找不到資料採礦演算法的警告，可能無法正確設定專案屬性。 當專案嘗試從 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器擷取資料採礦演算法的清單，而且找不到伺服器時，就會出現這個警告。 根據預設， [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]會使用**localhost**做為伺服器。 如果您要使用不同的執行個體或具名執行個體，您必須變更專案屬性。 如需詳細資訊，請參閱[建立 Analysis Services 專案 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)。  
  
5.  按 [下一步]  。  
  
6.  在 [**選取資料來源視圖**] 頁面的 [**可用的資料來源視圖**] 窗格中，選取 [**目標郵寄**]。 您可以按一下 **[流覽]** 以在 [資料來源] 視圖中查看資料表，然後按一下 [**關閉**] 返回嚮導。  
  
7.  按 [下一步]  。  
  
8.  在 [**指定資料表類型**] 頁面上，選取 [vTargetMail] 的 [**案例**] 資料行中的核取方塊，以將它當做案例資料表，然後按 **[下一步]**。 您之後將會使用 ProspectiveBuyer 資料表進行測試，現在請先忽略。  
  
9. 在 [**指定定型資料**] 頁面上，您將會識別至少一個可預測資料行、一個索引鍵資料行，以及一個用於模型的輸入資料行。 在 [ **BikeBuyer** ] 資料列的 [**可預測**] 資料行中選取此核取方塊。  
  
    > [!NOTE]  
    >  請注意視窗底部的警告。 您必須至少選取一個**輸入**和一個**可預測**的資料行，才能流覽至下一個頁面。  
  
10. 按一下 [**建議**] 以開啟 [**建議相關資料行**] 對話方塊。  
  
     每當至少選取一個可預測的屬性時，就會啟用 [**建議**] 按鈕。 [**建議相關資料行**] 對話方塊會列出與可預測資料行最密切相關的資料行，並依其與可預測屬性的相互關聯排序屬性。 系統會自動選取具有重大相互關聯性的資料行 (信心大於 95%)，使其包含在模型中。  
  
     檢查建議，然後按一下 [**取消**] 以 toignore 建議。  
  
    > [!NOTE]  
    >  如果您按一下 **[確定**]，則會在嚮導中將所有列出的建議標示為輸入資料行。 如果您僅同意其中某些建議，就必須手動變更其值。  
  
11. 確認已在**CustomerKey**資料列中選取 [索引**鍵**] 資料行中的核取方塊。  
  
    > [!NOTE]  
    >  如果資料來源檢視中的來源資料表指出索引鍵，資料採礦精靈會自動選擇這個資料行來做為模型的索引鍵。  
  
12. 在下列資料列中，選取 [**輸入**] 資料行中的核取方塊。 您可以核取多個資料行，其方式是反白顯示某個資料格範圍並按下 CTRL 鍵，然後同時選取核取方塊。  
  
    -   **存在**  
  
    -   **CommuteDistance**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **性別**  
  
    -   **GeographyKey**  
  
    -   **HouseOwnerFlag**  
  
    -   **MaritalStatus**  
  
    -   **NumberCarsOwned**  
  
    -   **NumberChildrenAtHome**  
  
    -   **區域**  
  
    -   **TotalChildren**  
  
    -   **YearlyIncome**  
  
13. 在頁面上最左邊的資料行上，選取以下資料列中的核取方塊。  
  
    -   **AddressLine1**  
  
    -   **AddressLine2**  
  
    -   **DateFirstPurchase**  
  
    -   **EmailAddress**  
  
    -   **名字**  
  
    -   **姓氏**  
  
     請確定這些資料列只有在左邊的資料行中才有核取記號。 這些資料行將會加入到您的結構中，但是不會併入模型中。 但是在建立此模型之後，這些資料行將可用於鑽研和測試。 如需有關「鑽取」的詳細資訊，請參閱[&#40;資料採礦的鑽看查詢&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
14. 按 [下一步]  。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [&#40;基本資料採礦教學課程中指定資料類型和內容類型&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [指定資料表類型 &#40;資料採礦嚮導&#41;](../../2014/analysis-services/specify-table-types-data-mining-wizard.md)   
 [資料採礦設計工具](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 決策樹演算法](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)  
  
  
