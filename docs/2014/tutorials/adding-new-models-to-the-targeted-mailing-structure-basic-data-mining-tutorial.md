---
title: 將新模型加入至目標的郵寄結構 （基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
caps.latest.revision: 45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db935cec3d17815d0884b1f596e870f6d09d5086
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222608"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>將新模型加入至目標郵寄結構 (基本資料採礦教學課程)
  在這個工作中，您將定義另外兩個模型，使用**採礦模型**資料採礦設計師 索引標籤。 您將會使用 Microsoft 群集和 Microsoft 貝氏機率分類演算法來建立模型。 之所以選擇這兩種演算法，是因為它們可以預測離散值 (例如自行車購買)。 如需有關這些演算法的詳細資訊，請參閱 < [Microsoft 群集演算法](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)和[Microsoft 貝氏機率分類演算法](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
### <a name="to-create-a-clustering-mining-model"></a>若要建立群集採礦模型  
  
1.  若要切換**Mining Models**  索引標籤中的資料採礦設計師中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
     請注意，設計工具會顯示兩個資料行，一個用於採礦結構，另一個用於`TM_Decision_Tree`您在上一課中建立的採礦模型。  
  
2.  以滑鼠右鍵按一下**結構**資料行，然後選取**新的採礦模型**。  
  
3.  在 **新的採礦模型**對話方塊中，於**模型名稱**，型別`TM_Clustering`。  
  
4.  在 **演算法名稱**，選取**Microsoft clustering 演譯**。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 新的模型現在會出現在**採礦模型**資料採礦設計師 索引標籤。 此模型中，以建置[!INCLUDE[msCoName](../includes/msconame-md.md)]群集演算法，分組到群集具有類似特性的客戶，並預測自行車購買行為，每個叢集。 雖然您可以修改的資料行使用方式和屬性的新模型，也就是沒有變更`TM_Clustering`模型不需要在此教學課程。  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>若要建立貝氏機率分類採礦模型  
  
1.  在 **採礦模型** 索引標籤的 資料採礦設計師中，權限可按一下**結構**資料行，然後選取**新的採礦模型**。  
  
2.  在 **新的採礦模型**對話方塊的 **模型名稱**，型別`TM_NaiveBayes`。  
  
3.  在 **演算法名稱**，選取**Microsoft 貝氏機率分類**，然後按一下 **確定**。  
  
     會出現訊息指出[!INCLUDE[msCoName](../includes/msconame-md.md)]貝氏機率分類演算法不支援**年齡**並**Yearly Income**連續資料行。  
  
4.  按一下 **是**確認訊息，並繼續。  
  
 新的模型會出現在**採礦模型**資料採礦設計師 索引標籤。 雖然您可以修改的資料行使用方式和屬性中的所有模型 索引標籤，變更`TM_NaiveBayes`模型不需要在此教學課程。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [處理目標的郵寄結構中的模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [將採礦模型加入結構中&#40;Analysis Services-資料採礦&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [資料採礦設計師](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [移動資料採礦物件](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  
