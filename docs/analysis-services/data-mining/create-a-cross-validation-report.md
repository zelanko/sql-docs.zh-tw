---
title: 建立交叉驗證報表 |Microsoft 文件
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 88d3af205a1e92ac07a4c841c80f2abea463de9b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="create-a-cross-validation-report"></a>建立交叉驗證報表
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  此主題逐步解說如何在資料採礦設計師中使用 [精確度圖表] 索引標籤來建立交叉驗證報表。 如需交叉驗證報表外觀及其所含統計量值的一般資訊，請參閱[交叉驗證 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)。  
  
 交叉驗證報表在本質上不同於增益圖或分類矩陣之類的精確度圖表。  
  
-   交叉驗證評估模型或結構中所用資料的整體分佈情況；因此，您不指定測試資料集。 交叉驗證永遠僅使用定型模型或採礦結構所用的原始資料。  
  
-   只能針對單一可預測結果執行交叉驗證。 如果結構支援具有不同可預測屬性的模型，您必須為每個可預測輸出建立不同的報表。  
  
-   只有與目前選定結構有關的模型才可供交叉驗證使用。  
  
-   如果目前所選的結構支援叢集和非叢集模型的組合，則在您按一下 [取得結果] 時，交叉驗證預存程序會自動載入具有相同預測資料行的模型，並且忽略不共用相同可預測屬性的叢集模型。  
  
-   只有在採礦模型不支援任何其他可預測屬性的情況下，您才可以對沒有可預測屬性的叢集模型建立交叉驗證報表。  
  
### <a name="select-a-mining-structure"></a>選取採礦結構  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開啟資料採礦設計師。  
  
2.  在 [方案總管] 中，開啟包含您想要建立報表之結構或模型的資料庫。  
  
3.  按兩下此採礦結構，在資料採礦設計師中開啟此結構以及其相關的模型。  
  
4.  按一下 **[採礦精確度圖表]** 索引標籤。  
  
5.  按一下 **[交叉驗證]** 索引標籤。  
  
### <a name="set-cross-validation-options"></a>設定交叉驗證選項  
  
1.  在 **[交叉驗證]** 索引標籤上，針對 **[摺疊計數]** 按一下向下箭頭，選取 1 到 10 之間的數字。 預設值是 10。  
  
     **[摺疊計數]** 表示將會在原始資料集內建立的資料分割數目。 如果您將 [摺疊計數] 設定為 1，將會使用定型集而不加以分割。  
  
2.  針對 **[目標屬性]** 按一下向下箭頭，然後從清單中選取資料行。 如果此模型為叢集模型，請選取 [#Cluster] 來指示此模型沒有可預測屬性。 請注意，只有在採礦結構不支援其他類型的可預測屬性時，值 **#Cluster** 才可供使用。  
  
     每一個報表只能選取一個可預測屬性。 根據預設，具有相同可預測屬性的所有相關模型都會包含在報表中。  
  
3.  在 **[最大案例數]** 中，輸入一個夠大的數字來提供當資料分割成指定的摺疊數時的代表性資料樣本。 如果此數字大於模型定型集內的案例計數，將會使用所有的案例。  
  
     如果訓練資料集非常大，則設定 **[最大案例數]** 的值會限制處理的總案例數，並讓報表更快完成。 但是，您不應該將 [最大案例數] 設定為太低的值，否則將不會有足夠的資料來進行交叉驗證。  
  
4.  選擇性地針對 **[目標狀態]** 輸入您想要模型化之可預測屬性的值。 例如，如果 [Bike Buyer] 資料行有兩個可能的值：1 (是) 和 2 (否)，您可以輸入 1 的值，只針對所需結果評估此模型的精確度。  
  
    > [!NOTE]  
    >  如果您不輸入值，[目標臨界值] 選項將無法使用，而且將會針對可預測屬性的所有可能值來評估此模型。  
  
5.  選擇性地針對 **[目標臨界值]** 輸入一個介於 0 和 1 之間的小數值，以指定要將預測算為精確時，所必須擁有的最小機率。  
  
     如需如何設定機率臨界值的更多提示，請參閱 [交叉驗證報表中的量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。  
  
6.  按一下 **[取得結果]**。  
  
### <a name="print-the-cross-validation-report"></a>列印交叉驗證報表  
  
1.  在 [交叉驗證] 索引標籤上，以滑鼠右鍵按一下完成的報表。  
  
2.  在快速鍵功能表中，選取 **[列印]** ，或選取 **[預覽列印]** 先檢閱報表。  
  
### <a name="create-a-copy-of-the-report-in-microsoft-excel"></a>在 Microsoft Excel 中建立報表的複本  
  
1.  在 [交叉驗證] 索引標籤上，以滑鼠右鍵按一下完成的報表。  
  
2.  在快速鍵功能表中，選取 **[全選]**。  
  
3.  以滑鼠右鍵按一下選取的文字，然後選取 [複製]。  
  
4.  將選取範圍貼到開啟的 Excel 活頁簿中。 如果您使用 **[貼上]** 選項，報表將會以 HTML 格式貼到 Excel 中，這樣會保留資料列和資料行的格式設定。 如果您針對文字或 Unicode 文字使用 [選擇性貼上] 選項來貼上報表，報表將會使用資料列分隔的格式貼上。  
  
## <a name="see-also"></a>另請參閱  
 [交叉驗證報表中的量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)  
  
  
