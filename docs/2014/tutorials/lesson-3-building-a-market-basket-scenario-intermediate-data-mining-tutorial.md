---
title: 第3課：建立購物籃案例（元資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- association algorithms [Analysis Services]
- nested tables
- tutorials [Data Mining]
ms.assetid: 651eef38-772e-4d97-af51-075b1b27fc5a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c2f1c5a8ae897284f07c3fd6c65d9735099a41fa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63042784"
---
# <a name="lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial"></a>第 3 課：建立購物籃狀況 (中繼資料採礦教學課程)
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的行銷部門想改進公司網站，採行交叉銷售 (Cross-selling) 的策略進行促銷。 在更新網站時，他們想要能夠根據客戶線上購物籃中的其他產品來預測客戶可能會想購買的產品。 行銷部門也想要更了解客戶的購買行為，讓他們可以設計網站，將客戶想要同時購買的項目放在一起。 他們了解到資料採礦對於此種類型的 *「購物籃分析」* (Market Basket Analysis) 特別實用，要求您開發資料採礦模型。  
  
 當您完成本課程的工作時，將會有一個顯示客戶交易歷程記錄中之產品群組的採礦模型。 而且，您可以使用這個採礦模型來預測客戶可能購買的其他產品。  
  
 若要完成這一課的工作，您將使用在元資料採礦教學課程的第一課中建立的解決方案和資料來源， [&#40;Analysis Services 資料採礦&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)。 您將加入包含客戶相關資料表 (包括客戶購買記錄的巢狀資料表) 的資料來源檢視，以修改這個方案。  接著，您將建立一個採礦模型，使用適用於購物籃狀況的 Microsoft 關聯規則演算法。  
  
 這個課程包含下列主題：  
  
-   [使用嵌套的資料表加入資料來源視圖 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
-   [建立購物籃結構和模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [修改和處理購物籃模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
-   [流覽購物籃模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
-   [&#40;中繼資料採礦教學課程來篩選模型中的嵌套資料表&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
-   [&#40;中繼資料採礦教學課程來預測關聯&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [使用嵌套的資料表加入資料來源視圖 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>所有課程  
 [第1課：建立中繼資料採礦解決方案 &#40;元資料採礦教學課程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [第2課：建立預測案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 第 3 課：購物籃案例 (中繼資料採礦教學課程)  
  
 [第4課：建立時序群集案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [第五課：建立類神經網路和羅吉斯迴歸模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [基本資料採礦教學課程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [第2課：建立預測案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)   
 [第4課：建立時序群集案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
  
