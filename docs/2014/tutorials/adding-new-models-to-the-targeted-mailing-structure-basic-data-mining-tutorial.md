---
title: 將新模型加入至目標郵寄結構（基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 285ee82110ffdef521d75fb43343f4889663e981
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62822629"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>將新模型加入至目標郵寄結構 (基本資料採礦教學課程)
  在這項工作中，您將使用資料採礦設計師的 [**採礦模型**] 索引標籤來定義兩個額外的模型。 您將會使用 Microsoft 群集和 Microsoft 貝氏機率分類演算法來建立模型。 之所以選擇這兩種演算法，是因為它們可以預測離散值 (例如自行車購買)。 如需這些演算法的詳細資訊，請參閱[Microsoft 群集演算法](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)和[Microsoft 貝氏貝氏機率分類演算法](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
### <a name="to-create-a-clustering-mining-model"></a>若要建立群集採礦模型  
  
1.  在中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，切換至 [資料採礦設計師] 中的 [**採礦模型**] 索引標籤。  
  
     請注意，設計工具會顯示兩個數據行，一個用於「採礦結構`TM_Decision_Tree` 」，另一個用於「採礦模型」（在上一課中建立）。  
  
2.  以滑鼠右鍵按一下 [**結構**] 資料行，然後選取 [新增] [**採礦模型**]。  
  
3.  在 [**新增採礦模型**] 對話方塊的 [**模型名稱**] 中`TM_Clustering`，輸入。  
  
4.  在 [**演算法名稱]** 中，選取 [ **Microsoft 群集**]。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 新的模型現在會出現在資料採礦設計師的 [**採礦模型**] 索引標籤中。 此模型是以叢集演算法[!INCLUDE[msCoName](../includes/msconame-md.md)]為基礎，將具有類似特性的客戶群組到叢集，並預測每個叢集的自行車購買。 雖然您可以修改新模型的資料行使用方式和屬性，但在`TM_Clustering`本教學課程中不需要對模型進行任何變更。  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>若要建立貝氏機率分類採礦模型  
  
1.  在資料採礦設計師的 [**採礦模型**] 索引標籤中，以滑鼠右鍵 clickthe**結構**資料行，然後選取 [新增] [**採礦模型**]。  
  
2.  在 [**新增採礦模型**] 對話方塊的 [**模型名稱**] 下`TM_NaiveBayes`，輸入。  
  
3.  在 [**演算法名稱]** 中，選取 [ **Microsoft 貝氏貝氏機率分類**]，然後按一下 **[確定]**。  
  
     此時會出現一則訊息[!INCLUDE[msCoName](../includes/msconame-md.md)] ，指出貝氏貝氏機率分類演算法不支援**Age**和**年收入**資料行，這是連續的。  
  
4.  按一下 **[是]** 以確認訊息並繼續。  
  
 新模型會出現在 [資料採礦設計師] 的 [**採礦模型**] 索引標籤中。 雖然您可以修改此索引標籤中所有模型的資料行使用方式和屬性，但在`TM_NaiveBayes`本教學課程中不需要對模型進行任何變更。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [處理目標郵寄結構中的模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [將採礦模型新增至結構 &#40;Analysis Services 資料採礦&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [資料採礦設計工具](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [移動資料採礦物件](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  
