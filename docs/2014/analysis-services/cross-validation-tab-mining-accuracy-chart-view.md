---
title: 交叉驗證索引標籤（[挖掘精確度圖表視圖]） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.crossvalidation.f1
ms.assetid: bd215a68-1ad7-4046-9c44-ec8e2be13a64
author: minewiskan
ms.author: owend
ms.openlocfilehash: 867bd6d1abffb29ec3eb2a8a78e562e5cbcc5b29
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526344"
---
# <a name="cross-validation-tab-mining-accuracy-chart-view"></a>交叉驗證索引標籤 (採礦精確度圖表檢視)
  交叉驗證可讓您將採礦結構資料分割成交叉區段，並反覆地針對每個交叉區段培訓和測試模型。 您會指定數個將資料分割成的折疊，然後使用每個折疊當做測試資料，而剩餘的資料則用來定型新模型。 然後 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 接著會針對每個模型產生一組標準精確度度量。 藉由比較針對每個交叉區段所產生的模型標準，您可以充分了解採礦模型對整個資料集而言有多可靠。  
  
 如需詳細資訊，請參閱[交叉驗證 &#40;Analysis Services - 資料採礦&#41;](data-mining/cross-validation-analysis-services-data-mining.md)。  
  
> [!NOTE]  
>  交叉驗證無法用於使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時序叢集演算法所建立的模型。 如果在包含上述類型之模型的採礦結構上執行報表，則報表中不會包含模型。  
  
## <a name="task-list"></a>工作清單  
  
-   指定摺疊數。  
  
-   指定用於交叉驗證的最大案例數目。  
  
-   指定可預測的資料行。  
  
-   選擇性地指定可預測的狀態。  
  
-   選擇性地設定參數以控制預測精確度的評估方式。  
  
-   按一下 [取得結果]**** 以顯示交叉驗證的結果。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **折迭計數**  
 指定要建立之摺疊或資料分割的數目。 最小值為 2，代表半數的資料集用於測試，半數用於培訓。  
  
 工作階段採礦結構的最大值為 10。  
  
 如果採礦結構儲存於 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體，則最大值為 256。  
  
> [!NOTE]  
>  隨著摺疊數增加，執行交叉驗證所需的時間同樣會增加 n。 如果案例數目很大，[摺疊計數]**** 的值也很大時，可能會發生效能問題。  
  
 **最大案例數**  
 指定用於交叉驗證的最大案例數目。 任何特定摺疊中的案例數都與 [最大案例數]**** 值除以 [摺疊計數]**** 值相同。  
  
 如果使用 **0**，則來源資料中的所有案例都會用來進行交叉驗證。  
  
 沒有任何預設值。  
  
> [!NOTE]  
>  如果增加案例數，則處理時間也會增加。  
  
 **目標屬性**  
 從所有模型中的可預測資料行清單選取資料行。 每次在執行交叉驗證時只能選取一個可預測資料行。  
  
 若僅要測試叢集模型，請選取 [叢集]****。  
  
 **目標狀態**  
 輸入值，或從下拉式的值清單選取目標值。  
  
 預設值為 `null`，表示要測試所有狀態。  
  
 已停用於叢集模型。  
  
 **目標**  **閾值**  
 指定 0 和 1 之間代表預測機率的值，高於該值的預測狀態會被視為正確。 可以用 0.1 的增量設定此值。  
  
 預設值是 `null`，代表會將最可能的預測計為正確。  
  
> [!NOTE]  
>  雖然可以將此值設定為 0.0，但使用此值會增加處理時間且不會產生有意義的結果。  
  
 **取得結果**  
 按一下即可使用指定的參數開始對模型進行交叉驗證。  
  
 模型會資料分割成指定的摺疊數，且針對每個折疊測試個別的模型。 因此，交叉驗證可能要花一些時間才能傳回結果。  
  
 如需如何解譯交叉驗證報表結果的詳細資訊，請參閱 [交叉驗證報表中的量值](data-mining/measures-in-the-cross-validation-report.md)。  
  
## <a name="setting-the-accuracy-threshold"></a>設定精確度臨界值  
 您可以藉由設定 [目標臨界值]**** **** 的值來控制預測精確度的測量標準。 臨界值代表一種精確度列。 每個預測都會被指派預測值正確的機率。 因此，如果將 [目標臨界值]**** **** 的值設定為接近 1，則任何特定預測的機率必須相當高才會計為良好的預測。 相反地，如果將 [目標臨界值]**** **** 的值設定為接近 0，則即使具有較低機率值的預測也會計為「良好」的預測。  
  
 我們不推薦任何臨界值，因為預測的機率是根據資料量及進行的預測類型而定。 您應該以不同的機率層級檢閱一些預測，如此才能為資料判斷適當的精確度列。 這項作業很重要，因為您為 [目標臨界值]**** **** 所設定的值會影響測量到的模型精確度。  
  
 例如，假設針對特定的目標狀態進行了三項預測，而每項預測的機率分別為 0.05、0.15 和 0.8。 如果將臨界值設定為 0.5，只有一項預測會計為正確。 如果您將 [目標臨界值]**** **** 設定為 0.10，其中兩項預測就會計為正確。  
  
 當 [**目標****臨界**值] 設定為 `null` （預設值）時，會將每個案例最可能的預測計為正確。 在剛剛提及的範例中，0.05、0.15 和 0.8 是三個不同案例的預測機率。 雖然機率非常不同，但每項預測都會被視為正確，因為每個案例都只會產生一項預測，而這些都是這些案例的最佳預測。  
  
## <a name="see-also"></a>另請參閱  
 [測試和驗證 &#40;資料採礦&#41;](data-mining/testing-and-validation-data-mining.md)   
 [交叉驗證 &#40;Analysis Services-資料採礦&#41;](data-mining/cross-validation-analysis-services-data-mining.md)   
 [交叉驗證報表中的量值](data-mining/measures-in-the-cross-validation-report.md)   
 [資料採礦預存程序 &#40;Analysis Services - 資料採礦&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  
