---
title: 檢視或變更演算法參數 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58b512d726d45a8ceabb76a4ce2b1e6c8c62815b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="view-or-change-algorithm-parameters"></a>檢視或變更演算法參數
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以變更演算法所提供的參數，您會使用該演算法來建立資料採礦模型，以自訂模型的結果。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中所提供的演算法參數所變更的項目不只是模型上的屬性而已，還可用來從根本上改變資料處理、群組和顯示的方式。 例如，您可以使用演算法參數來執行下列動作：  
  
-   變更分析的方法，例如叢集方法。  
  
-   控制特徵選取行為。  
  
-   指定項目集的大小或規則的機率。  
  
-   控制決策樹的分支和深度。  
  
-   指定模型建立所使用之內部鑑效組集合的初始值或大小。  
  
 為每個演算法提供的參數會有很大的差異；如需您可以為每個演算法設定的參數清單，請參閱本節中的技術參考主題：[資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
### <a name="change-an-algorithm-parameter"></a>變更演算法參數  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，於資料採礦設計師的 [採礦模型] 索引標籤上，以滑鼠右鍵按一下您要微調演算法之採礦模型的演算法類型，並選取 [設定演算法參數]。  
  
     就會開啟 **[演算法參數]** 對話方塊。  
  
2.  在 **[值]** 資料行中，設定您要變更之演算法的新值。  
  
     如果您沒有在 **[值]** 資料行中輸入值， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用預設參數值。 **[範圍]** 資料行描述您可以輸入的可能值。  
  
3.  按一下 **[確定]**。  
  
     演算法參數就會以新值設定。 要等到您重新處理採礦模型之後，參數變更才會反映在該採礦模型中。  
  
### <a name="view-the-parameters-used-in-an-existing-model"></a>檢視用於現有模型中的參數  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟 DMX 查詢視窗。  
  
2.  輸入類似以下的查詢：  
  
    ```  
    select MINING_PARAMETERS   
    from $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = '<model name>'  
  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型的工作與操作方法](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
