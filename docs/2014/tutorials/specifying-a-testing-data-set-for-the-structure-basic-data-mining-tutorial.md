---
title: 指定測試資料集結構 （基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 75cd508f-b126-418b-848d-3c4c3e6c303f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1e0bee469bd6dbbc93a48051e7c2e236c6c65c74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180918"
---
# <a name="specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial"></a>為結構指定測試資料集 (基本資料採礦教學課程)
  在資料採礦精靈的最後幾個畫面中，您會將資料分成測試集和定型集。 然後您會命名您的結構，並啟用模型上的鑽研。  
  
## <a name="specifying-a-testing-set"></a>指定測試集  
 在建立採礦結構時將資料分成定型集和測試集，可輕鬆評估您稍後建立之採礦模型的精確度。 如需有關測試集的詳細資訊，請參閱 <<c0> [ 定型和測試資料集](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
#### <a name="to-specify-the-testing-set"></a>若要指定測試集  
  
1.  在上**建立測試集**頁面上，如**測試資料的百分比**，保留預設值的`30`。  
  
2.  針對**的情況下，在測試資料集內的最大數目**，輸入`1000`。  
  
3.  按 [下一步] 。  
  
## <a name="specifying-drillthrough"></a>指定鑽研  
 可以在模型和結構上啟用鑽研。 此對話方塊中的核取方塊允許在具名模型上鑽研。 此模型經過處理之後，您將能夠從定型資料 中擷取用來建立模型的詳細資訊。  
  
 如果基礎採礦結構也已經設定為允許鑽研，您就可以同時從模型案例和採礦結構中擷取詳細資訊，包括未包含在採礦模型中的資料行。 如需詳細資訊，請參閱[鑽研查詢 &#40;資料採礦&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
#### <a name="to-name-the-model-and-structure-and-specify-drillthrough"></a>若要命名模型和結構及指定鑽研  
  
1.  在 **完成精靈**頁面上，於**採礦結構名稱**，型別`Targeted Mailing`。  
  
2.  在 **採礦模型名稱**，輸入`TM_Decision_Tree`。  
  
3.  選取 **允許使用鑽研**核取方塊。  
  
4.  檢閱**預覽**窗格。 請注意，只有選取做為這些資料行**金鑰**，**輸入**或是**可預測**列示如下。 您所選的其他資料行 (例如 AddressLine1) 不會用於建立模型，但是可在基礎結構中使用，而且可在處理及部署模型之後加以查詢。  
  
5.  按一下 **[完成]**。  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [指定資料類型和內容類型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一課  
 [第 3 課：新增及處理模型](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="see-also"></a>另請參閱  
 [針對採礦模型啟用鑽研](../../2014/analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)   
 [鑽研查詢&#40;資料採礦&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [指定定型資料&#40;資料採礦精靈&#41;](../../2014/analysis-services/specify-the-training-data-data-mining-wizard.md)  
  
  
