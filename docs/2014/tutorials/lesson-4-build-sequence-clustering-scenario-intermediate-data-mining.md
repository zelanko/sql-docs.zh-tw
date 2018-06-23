---
title: 第 4 課： 建立時序群集案例 （中繼資料採礦教學課程） |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- sequence clustering algorithms [Analysis Services]
- tutorials [Data Mining]
ms.assetid: 63436bbd-0f73-4012-b6f1-358c81e4d92a
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7bfa4dd3a739e81b5a7f10cda0b17452fe48c4d0
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311876"
---
# <a name="lesson-4-building-a-sequence-clustering-scenario-intermediate-data-mining-tutorial"></a>第 4 課：建立時序群集案例 (中繼資料採礦教學課程)
  行銷部門[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]想了解客戶如何透過移動[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]網站。 公司猜想客戶會依某種次序模式，將產品放入購物籃中。 公司希望分析購物次序，以了解客戶如何將相關的產品加入購物籃中。 之後，他們就能利用這項資訊來簡化網站的流程，以便引導客戶購買其他產品。  
  
 當您完成這個課程的工作時，將會建好一個採礦模型，使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時序群集演算法預測客戶接著會將哪一項產品放入購物籃中。 您將實驗兩種版本的模型：第一個模型只分析購物籃中的產品順序，而第二個模型另外包含一些用於群集的客戶人口統計資料。 最後，您將使用這些模型來建立預測，以便向客戶提供產品建議。  
  
 若要完成本課程的工作，您會使用您在建立購物籃採礦結構[第 3 課： 建立購物籃狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)。 這一課包含下列工作：  
  
-   [建立時序群集採礦模型結構&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
-   [處理時序群集模型](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
-   [探索時序群集模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [建立相關的時序群集模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [時序群集模型上建立預測&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立時序群集採礦模型結構&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>所有課程  
 [第 1 課： 建立中繼資料採礦方案&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [第 2 課： 建立預測狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [第 3 課： 建立購物籃狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 第 4 課：時序群集案例 (中繼資料採礦教學課程)  
  
 [第 5 課： 建立類神經網路和羅吉斯迴歸模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [基本資料採礦教學課程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [中繼資料採礦教學課程&#40;Analysis Services-資料採礦&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  