---
title: 時間序列預測 DMX 教學課程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 38ea7c03-4754-4e71-896a-f68cc2c98ce2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1623f824c062c270268323fd45ebf0e9533c8788
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044177"
---
# <a name="time-series-prediction-dmx-tutorial"></a>時間序列預測 DMX 教學課程
  在本教學課程中，您將學會如何建立時間序列採礦結構、建立三種自訂時間序列採礦模型，以及使用這些模型建立預測。  
  
 採礦模型將依據 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 範例資料庫中的資料，該資料庫儲存了虛構公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的資料。 
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨國製造公司。  
  
## <a name="tutorial-scenario"></a>教學課程案例  
 
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 決定使用資料採礦來產生銷售預測。 他們已經建立了一些區域預測模型;如需詳細資訊，請參閱[第2課：建立預測案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。 不過，業務部門需要能夠定期以新的銷售資料來更新資料採礦模型。 而且，還要自訂模型以提供不同預測。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]提供數個可用來完成這項工作的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]工具：  
  
-   資料採礦延伸模組 (DMX) 查詢語言  
  
-   Microsoft 時間序列演算法  
  
-   中的查詢編輯器[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]時間序列演算法會建立可用於預測時間相關資料的模型。 資料採礦延伸模組 (DMX) 是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的一種查詢語言，您可以使用它來建立採礦模型與預測查詢。  
  
## <a name="what-you-will-learn"></a>學習內容  
 這個教學課程假設您已熟悉 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用來建立採礦模型的物件。 如果您先前未曾使用 DMX 建立了「採礦結構」或「採礦模型」，請參閱[自行車購買者 DMX 教學](../../2014/tutorials/bike-buyer-dmx-tutorial.md)課程。  
  
 這個教學課程分成下列課程：  
  
 [第 1 課：建立時間序列採礦模型和採礦結構](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)  
 在這一課，您將學會如何使用 `CREATE MINING MODEL` 陳述式來新增預測模型及相關聯的採礦模型。  
  
 [第 2 課：將採礦模型加入時間序列採礦結構中](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
 在這一課，您將學會如何使用 ALTER MINING STRUCTURE 陳述式將新的採礦模型加入至時間序列結構。 此外，您還將學習如何自訂用於分析時間序列的演算法。  
  
 [第 3 課：處理時間序列結構和模型](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
 在這一課，您將學習如何使用 `INSERT INTO` 陳述式來定型模型，以及用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫中的資料來擴展結構。  
  
 [第 4 課：使用 DMX 建立時間序列預測](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
 在這一課，您將學習如何建立時間序列預測。  
  
 [第 5 課：擴充時間序列模型](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
 在這一課，您將學會如何使用 `EXTEND_MODEL_CASES` 參數，在進行預測時以新資料更新模型。  
  
## <a name="requirements"></a>需求  
 在執行此教學課程之前，請確定有安裝下列各項：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   
  [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫  
  
 為了加強安全性，系統預設不會安裝範例資料庫。 若要安裝的正式範例資料庫[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請移[http://www.CodePlex.com/MSFTDBProdSamples](https://go.microsoft.com/fwlink/?LinkId=88417)至或 Microsoft SQL Server 產品範例一節中的 Microsoft SQL Server 範例和 [社區專案] 首頁。 按一下 [**資料庫**]，然後按一下 [**發行**] 索引標籤，並選取您想要的資料庫。  
  
> [!NOTE]  
>  當您查看教學課程時，建議您將 **[下一個主題]** 和 [**上一個主題**] 按鈕新增至 [檔檢視器] 工具列。  
  
## <a name="see-also"></a>另請參閱  
 [基本資料採礦教學課程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [元資料採礦教學課程 &#40;Analysis Services-資料採礦&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
