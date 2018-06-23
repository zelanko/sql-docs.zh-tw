---
title: 第 4 課： 探索目標的郵寄模型 （基本資料採礦教學課程） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1e00c5b9-a9f8-4503-99ee-377c9cc02d7f
caps.latest.revision: 51
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 57ebae0dfb1e8f472647818cad2c8f724e8b3c0e
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313168"
---
# <a name="lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial"></a>第 4 課：探索目標郵寄模型 (基本資料採礦教學課程)
  處理完專案中的模型之後，您可以瀏覽模型來尋找值得參考的趨勢。 由於模式光看數字可能相當複雜且難以上手，SQL Server 資料採礦提供了一些視覺化工具，可協助您調查資料及了解演算法在資料內探索到的規則和關聯性。 您也可以使用各種精確度測試，在部署模型之前驗證您的資料集或找出執行能力最佳的模型。  
  
 當您使用[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]瀏覽模型，您建立每個模型都會列在**採礦模型檢視器**資料採礦設計師中的索引標籤。 您可以使用檢視器瀏覽模型。 這些檢視器也可以在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用。  
  
 您在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中用來建立模型的每個演算法都會傳回不同類型的結果。 因此，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 為每一類型的機器學習模型提供自訂檢視器。  
  
 如果您想要探查詳細資料，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]也提供了 HTML 檢視器，稱為**一般內容樹狀檢視器**，會顯示模型資料和任何模式中找不到，半邊表格格式的詳細的資訊。 如需詳細資訊，請參閱 [使用 Microsoft 一般內容樹狀檢視器瀏覽模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)。  
  
 在這一課，您將查看三種模型產生的結果。 每一種模型類型都根據不同的演算法，讓您以不同的角度去了解資料。  
  
-   決策樹模型指出影響自行車購買行為的因素。  
  
-   群集模型依客戶的自行車購買行為以及您選擇的其他屬性，將客戶予以分組。  
  
-   貝氏機率分類模型可以讓您探索不同屬性之間的關聯。  
  
 請參閱下列主題，深入了解每一種採礦模型檢視器。  
  
-   [瀏覽決策樹模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [瀏覽群集模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [瀏覽貝氏機率分類模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
 有三個模型可以使用檢視**一般內容樹狀檢視器**，以便擷取公式、 資料值，以及其他等等。  
  
## <a name="first-task-in-lesson"></a>本課程的第一項工作  
 [瀏覽決策樹模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-lesson"></a>上一課  
 [第 3 課： 加入及處理模型](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="next-lesson"></a>下一課  
 [第 5 課： 測試模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型檢視器工作和使用說明](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [資料採礦模型檢視器](../../2014/analysis-services/data-mining/data-mining-model-viewers.md)  
  
  