---
title: 第4課：探索目標郵寄模型（基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e00c5b9-a9f8-4503-99ee-377c9cc02d7f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 97db61dc3b9adf2e345957c8e08aa752e51286e0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63312144"
---
# <a name="lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial"></a>第 4 課：探索目標郵寄模型 (基本資料採礦教學課程)
  處理完專案中的模型之後，您可以瀏覽模型來尋找值得參考的趨勢。 由於模式光看數字可能相當複雜且難以上手，SQL Server 資料採礦提供了一些視覺化工具，可協助您調查資料及了解演算法在資料內探索到的規則和關聯性。 您也可以使用各種精確度測試，在部署模型之前驗證您的資料集或找出執行能力最佳的模型。  
  
 當您使用[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]來探索模型時，您建立的每個模型都會列在資料採礦設計師的 [**採礦模型檢視器**] 索引標籤中。 您可以使用檢視器瀏覽模型。 這些檢視器也可以在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用。  
  
 您在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中用來建立模型的每個演算法都會傳回不同類型的結果。 因此，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 為每一類型的機器學習模型提供自訂檢視器。  
  
 如果您想要深入瞭解詳細資料[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，也會提供稱為「**一般內容樹狀檢視器**」的 HTML 檢視器，其中會以半表格式格式顯示模型資料的詳細資訊，以及找到的任何模式。 如需詳細資訊，請參閱 [使用 Microsoft 一般內容樹狀檢視器瀏覽模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)。  
  
 在這一課，您將查看三種模型產生的結果。 每一種模型類型都根據不同的演算法，讓您以不同的角度去了解資料。  
  
-   決策樹模型指出影響自行車購買行為的因素。  
  
-   群集模型依客戶的自行車購買行為以及您選擇的其他屬性，將客戶予以分組。  
  
-   貝氏機率分類模型可以讓您探索不同屬性之間的關聯。  
  
 請參閱下列主題，深入了解每一種採礦模型檢視器。  
  
-   [流覽決策樹模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [&#40;基本資料採礦教學課程中探索群集模型&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [探索貝氏貝氏機率分類模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
 這三種模型都可以使用**一般內容樹狀檢視器**來查看，以解壓縮公式、資料值等等。  
  
## <a name="first-task-in-lesson"></a>本課程的第一項工作  
 [流覽決策樹模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-lesson"></a>上一課  
 [第 3 課：新增及處理模型](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="next-lesson"></a>下一課  
 [第5課： &#40;基本資料採礦教學課程來測試模型&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型檢視器工作和操作說明](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [資料採礦模型檢視器](../../2014/analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
