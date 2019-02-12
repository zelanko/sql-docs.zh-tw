---
title: 第 5 課：建立類神經網路和羅吉斯迴歸模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- data mining [Analysis Services], tutorials
- neural networks
- tutorials [Data Mining]
- neural network model [Analysis Services]
ms.assetid: 42c3701a-1fd2-44ff-b7de-377345bbbd6b
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: daf554338a50a81f46d86a77bf04e770fcc2512e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035809"
---
# <a name="lesson-5-building-neural-network-and-logistic-regression-models-intermediate-data-mining-tutorial"></a>第 5 課：建立類神經網路和羅吉斯迴歸模型 （中繼資料採礦教學課程）
  
  
 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 的營業部門正在負責處理一個專案，目標是提升撥接中心的客戶滿意度。 他們雇用廠商來管理撥接中心、回報撥接中心績效的數據，並要求您分析廠商所提供的一些初步資料。 他們想要知道是否有任何有趣的發現。 他們尤其想知道這些資料是否反映出有關人員雇用的任何問題，或改善客戶滿意度的方式。  
  
 這個資料集很小，只包含期限為 30 天的撥接中心作業。 這些資料會追蹤每個排班的新進和資深操作員數目、來電數目、訂單數目、必須解決的問題數目，以及客戶等候電話回應的平均時間。 資料也包含以 *「放棄率」*(Abandon Rate) (這是客戶挫折度的指標) 為基礎的服務品質標準。  
  
 由於您對於資料呈現的內容沒有任何預先的期待，因此您決定使用類神經網路模型來探索可能的相互關聯。 類神經網路模型經常用於進行探索，因為這種模型可以分析許多輸入和輸出之間的複雜關聯性。  
  
## <a name="what-you-will-learn"></a>學習內容  
 在本課中，您將使用類神經網路演算法建立模型，幫助您和營業小組理解資料中的趨勢。 在這個課程中，您將嘗試回答下列問題：  
  
-   什麼因數會影響客戶滿意度？  
  
-   撥接中心可以做些什麼來改善服務品質？  
  
 根據這些結果，您將接著建立一個羅吉斯迴歸模型以進行預測。 營業小組將使用這些預測來協助規劃撥接中心作業。  
  
 這個課程包含下列主題：  
  
-   [新增資料來源的撥接中心資料的檢視&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
-   [建立類神經網路結構和模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [探索撥接中心模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
-   [將羅吉斯迴歸模型加入到撥接中心結構&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
-   [建立用於撥接中心模型的預測&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [新增資料來源的撥接中心資料的檢視&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>所有課程  
 [第 1 課：建立中繼資料採礦方案&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [第 2 課：建立預測狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [第 3 課：建立購物籃狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [第 4 課：建立時序群集案例&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 第 5 課：類神經網路和羅吉斯迴歸案例 （中繼資料採礦教學課程）  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦基本教學課程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [中繼資料採礦教學課程&#40;Analysis Services-資料採礦&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
