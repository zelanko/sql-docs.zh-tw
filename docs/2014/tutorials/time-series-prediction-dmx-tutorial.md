---
title: 時間序列預測 DMX 教學課程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 38ea7c03-4754-4e71-896a-f68cc2c98ce2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 722077829513f96b02680b530a0c366252f1ba33
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134208"
---
# <a name="time-series-prediction-dmx-tutorial"></a>時間序列預測 DMX 教學課程
  在本教學課程中，您將學會如何建立時間序列採礦結構、建立三種自訂時間序列採礦模型，以及使用這些模型建立預測。  
  
 採礦模型將依據 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 範例資料庫中的資料，該資料庫儲存了虛構公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的資料。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨國製造公司。  
  
## <a name="tutorial-scenario"></a>教學課程案例  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 決定使用資料採礦來產生銷售預測。 它們已建置一些區域預測模型;如需詳細資訊，請參閱 <<c0> [ 第 2 課： 建立預測狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。</c0> 不過，業務部門需要能夠定期以新的銷售資料來更新資料採礦模型。 而且，還要自訂模型以提供不同預測。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供數個工具，可用來完成這項工作：  
  
-   資料採礦延伸模組 (DMX) 查詢語言  
  
-   Microsoft 時間序列演算法  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的查詢編輯器  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法所建立的模型，可用來進行與時間相關的資料預測。 資料採礦延伸模組 (DMX) 是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的一種查詢語言，您可以使用它來建立採礦模型與預測查詢。  
  
## <a name="what-you-will-learn"></a>學習內容  
 這個教學課程假設您已熟悉 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用來建立採礦模型的物件。 如果您已建立的採礦結構或採礦模型使用 DMX，請參閱[Bike Buyer DMX 教學課程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)。  
  
 這個教學課程分成下列課程：  
  
 [第 1 課：建立時間序列採礦模型和採礦結構](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)  
 在這一課，您將學會如何使用 `CREATE MINING MODEL` 陳述式來新增預測模型及相關聯的採礦模型。  
  
 [第 2 課：將採礦模型新增至時間序列採礦結構中](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
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
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫  
  
 為了加強安全性，系統預設不會安裝範例資料庫。 若要安裝的正式範例資料庫[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請前往[ http://www.CodePlex.com/MSFTDBProdSamples ](http://go.microsoft.com/fwlink/?LinkId=88417)或在 Microsoft SQL Server Samples and Community Projects 首頁上，在 [Microsoft SQL Server Product Samples] 區段。 按一下 **資料庫**，然後按一下**版本**索引標籤，然後選取您想要的資料庫。  
  
> [!NOTE]  
>  當檢閱教學課程時，我們建議您將新增**下一個主題**並**上一個主題**文件檢視器工具列的按鈕。  
  
## <a name="see-also"></a>另請參閱  
 [基本資料採礦教學課程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [中繼資料採礦教學課程&#40;Analysis Services-資料採礦&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
