---
title: 基本資料採礦教學課程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 6602edb6-d160-43fb-83c8-9df5dddfeb9c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d434df95a26485d4d7795d3ab960b8d2457b8ff6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63185570"
---
# <a name="basic-data-mining-tutorial"></a>資料採礦基本教學課程
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]歡迎使用基本資料採礦教學課程。 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]提供用來建立資料採礦模型和進行預測的整合式環境。 在本教學課程中，您將完成一個目標郵寄促銷活動案例，以運用機器學習方法來分析和預測客戶購買行為。 本教學課程示範如何使用三種最重要的資料採礦演算法：群集、決策樹和貝氏機率分類。 您也將瞭解如何使用「採礦模型檢視器」來分析您的結果，以及使用所包含[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的資料採礦工具來建立預測和精確度圖表。 所有範例都以虛構公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 為例。  
  
 當您習慣使用資料採礦工具時，我們建議您也[&#40;Analysis Services 資料採礦&#41;，完成中繼資料採礦教學](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)課程。 其課程示範如何使用預測、購物籃分析、時間序列、關聯模型、巢狀資料表和時序群集。  
  
## <a name="tutorial-scenario"></a>教學課程案例  
 在本教學課程中，您是[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]負責根據採購歷程記錄深入瞭解公司客戶的員工，然後使用該歷程記錄資料來進行可用於行銷的預測。 該公司尚未進行過資料採礦，所以您必須特別針對資料採礦建立新的資料庫，並設定數個資料採礦模型。  
  
## <a name="what-you-will-learn"></a>學習內容  
 這個教學課程告訴您如何建立與使用幾種不同類型的機器學習方法。 您也將學習如何建立採礦模型的副本，並對輸入資料套用篩選以取得不同的結果。 而後，您可以使用增益圖比較這兩個模型的結果。 最後，您將使用鑽研功能從基礎採礦結構擷取其他資料。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資料採礦包含下列功能，可協助您輕鬆地開發和比較多個預測模型，然後對結果採取動作：  
  
-   *維持的測試集-* 當您建立「採礦結構」時，您現在可以將「採礦結構」中的資料分割成定型集和測試集。 這可讓您在類似的資料集上測試模型，以及比較相關模型的精準度。  
  
-   *採礦模型篩選-* 您現在可以將篩選附加至「採礦模型」，並在定型和測試期間套用篩選。 這可讓您在不同的資料子集上輕鬆建立相關的模型。  
  
-   *對結構案例和結構資料行的鑽取-* 您現在可以輕鬆地從「採礦模型」中的一般模式移至資料來源中的可操作詳細資料。  
  
 這個教學課程分成下列課程：  
  
 [第1課：準備 Analysis Services 資料庫 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-1-preparing-the-analysis-services-database-basic-data-mining-tutorial.md)  
 在這個課程中，您將學習如何建立新的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫、加入資料來源和資料來源檢視，以及準備資料採礦要用的新資料庫。  
  
 [第2課：建立目標郵寄結構 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
 在這一課，您將學習如何建立目標郵寄狀況中所能使用的採礦模型結構。  
  
 [第 3 課：新增及處理模型](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
 在這一課，您將學會如何將模型加入到結構中。 您建立的模型會使用下列演算法建立：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹  
  
-    群集  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 貝氏機率分類  
  
 [第4課：探索目標郵寄模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
 在這一課，您將學會如何使用檢視器探索及解譯各模型的發現。  
  
 [第5課： &#40;基本資料採礦教學課程來測試模型&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
 在這一課，您要建立其中一個目標郵寄模型的副本、加入採礦模型篩選以便將定型資料限制在特定一組客戶，然後評估模型的可用性。  
  
 [第 6 課：建立及處理預測 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
 在這基本資料採礦教學課程的最後一課，您將使用模型來預測哪些客戶最有可能購買自行車。 接著，您要鑽研基礎案例以取得連絡資訊。  
  
## <a name="requirements"></a>需求  
 請確定已安裝下列項目：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]模式中  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫。  
  
 為了加強安全性，範例資料庫不會隨著 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 一起安裝。 若要安裝的正式資料庫[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請造訪[Microsoft SQL 範例資料庫](https://go.microsoft.com/fwlink/?LinkId=88417)頁面，並[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]選取。  
  
> [!NOTE]  
>  當您進行教學課程時，如果您將 [**下一個主題]** 和 [**上一個主題**] 按鈕新增至 [檔檢視器] 工具列，則可能會更容易在步驟之間來回移動。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦解決方案](../../2014/analysis-services/data-mining/data-mining-solutions.md)   
 [採礦模型工作和操作說明](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [使用 DMX 建立並查詢資料採礦模型：教學課程 &#40;Analysis Services - 資料採礦&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)  
  
  
