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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185570"
---
# <a name="basic-data-mining-tutorial"></a>資料採礦基本教學課程
  歡迎來到[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]基本資料採礦教學課程。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供一個整合式的環境來建立資料採礦模型及進行預測。 在本教學課程中，您將完成您的使用機器學習服務來分析和預測客戶購買行為的目標郵寄促銷活動的案例。 本教學課程示範如何使用三種最重要的資料採礦演算法：群集、決策樹和貝氏機率分類。 您也將學習如何使用採礦模型檢視器分析您找到並建立預測和精確度圖表使用資料採礦工具隨附於[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 所有範例都以虛構公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 為例。  
  
 當您準備好使用資料採礦工具時，我們建議您最好也完成[中繼資料採礦教學課程&#40;Analysis Services-Data Mining&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)。 其課程示範如何使用預測、購物籃分析、時間序列、關聯模型、巢狀資料表和時序群集。  
  
## <a name="tutorial-scenario"></a>教學課程案例  
 在本教學課程中，您是員工[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]誰負責深入了解公司客戶根據的採購歷程記錄，，然後使用該歷程記錄資料進行行銷可用的預測。 該公司尚未進行過資料採礦，所以您必須特別針對資料採礦建立新的資料庫，並設定數個資料採礦模型。  
  
## <a name="what-you-will-learn"></a>學習內容  
 這個教學課程告訴您如何建立與使用幾種不同類型的機器學習方法。 您也將學習如何建立採礦模型的副本，並對輸入資料套用篩選以取得不同的結果。 而後，您可以使用增益圖比較這兩個模型的結果。 最後，您將使用鑽研功能從基礎採礦結構擷取其他資料。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料採礦包括下列功能，協助您輕鬆地開發和比較多個預測性模型，以及再對結果採取動作：  
  
-   *鑑效組測試集-* 當您建立採礦結構時，您現在可以將採礦結構中的資料分成定型和測試集。 這可讓您在類似的資料集上測試模型，以及比較相關模型的精準度。  
  
-   *採礦模型篩選器-* 現在可以將篩選附加至採礦模型，並在定型和測試期間套用的篩選器。 這可讓您在不同的資料子集上輕鬆建立相關的模型。  
  
-   *鑽研結構案例和結構資料行-* 您現在可以輕鬆移從採礦模型中的一般模式中的資料來源可採取動作的詳細資料。  
  
 這個教學課程分成下列課程：  
  
 [第 1 課：正在準備分析服務資料庫&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-1-preparing-the-analysis-services-database-basic-data-mining-tutorial.md)  
 在這個課程中，您將學習如何建立新的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫、加入資料來源和資料來源檢視，以及準備資料採礦要用的新資料庫。  
  
 [第 2 課：建立目標的郵寄結構&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
 在這一課，您將學習如何建立目標郵寄狀況中所能使用的採礦模型結構。  
  
 [第 3 課：加入及處理模型](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
 在這一課，您將學會如何將模型加入到結構中。 您建立的模型會使用下列演算法建立：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 群集  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 貝氏機率分類  
  
 [第 4 課：探索目標的郵寄模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
 在這一課，您將學會如何使用檢視器探索及解譯各模型的發現。  
  
 [第 5 課：測試模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
 在這一課，您要建立其中一個目標郵寄模型的副本、加入採礦模型篩選以便將定型資料限制在特定一組客戶，然後評估模型的可用性。  
  
 [第 6 課：建立及處理預測&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
 在這基本資料採礦教學課程的最後一課，您將使用模型來預測哪些客戶最有可能購買自行車。 接著，您要鑽研基礎案例以取得連絡資訊。  
  
## <a name="requirements"></a>需求  
 請確定已安裝下列項目：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多維度模式  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫。  
  
 為了加強安全性，範例資料庫不會隨著 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 一起安裝。 若要安裝的正式資料庫[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請瀏覽[Microsoft SQL Sample Databases](https://go.microsoft.com/fwlink/?LinkId=88417)頁面，然後選取[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]。  
  
> [!NOTE]  
>  當您使用透過本教學課程時，您可能會發現它在步驟之間來回移動，如果您新增的工作變得更容易**下一個主題**並**上一個主題**文件檢視器工具列的按鈕。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦方案](../../2014/analysis-services/data-mining/data-mining-solutions.md)   
 [採礦模型工作和使用說明](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [建立及查詢使用 DMX 資料採礦模型：教學課程&#40;Analysis Services-資料採礦&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)  
  
  
