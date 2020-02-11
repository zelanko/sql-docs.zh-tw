---
title: 中繼資料採礦教學課程（Analysis Services 資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 404b31d5-27f4-4875-bd60-7b2b8613eb1b
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4c244701d8a58765061ef3bde1f918c8be5a941d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63017174"
---
# <a name="intermediate-data-mining-tutorial-analysis-services---data-mining"></a>中繼資料採礦教學課程 (Analysis Services - 資料採礦)
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]提供用來建立和使用資料採礦模型的整合式環境。 您可以輕易地繫結資料來源、以相同資料建立及測試多個模型，以及部署模型以供預測分析。  
  
 在基本資料採礦教學課程中，您學會了如何使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 建立資料採礦方案，並且建立了三個模型來支援目標郵寄行銷資料，以供分析客戶購買行為與目標潛在購買者。  
  
 這個中繼教學課程會進一步運用這些工具，並且介紹許多新狀況，包括像是預測和購物籃分析等常見的商業需求。 您將學習如何建立時間序列模型、關聯模型以及時序群集模型。 最後，您將學習如何使用類神經網路探索資料的相關性，以及使用羅吉斯迴歸進行預測。  
  
 這些課程都是獨立的，而且可以分開完成。  
  
 若要完成下列教學課程，您應該熟悉在基本資料採礦教學課程中介紹的資料採礦工具與採礦模型檢視器。  
  
 所有狀況都使用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料來源，不過您需要為不同的狀況建立不同的資料來源。 只要先建立資料來源，就可以依任何順序進行課程。  
  
## <a name="lesson-scenarios"></a>課程狀況  
 當您成功完成目標郵寄行銷資料後，接著要運用您的資料採礦知識，開發數種新模型以便用於商務計畫。 這些包括下列工作：  
  
-   **預測：** 您將會建立*時間序列*模型，以預測全球不同區域的產品銷售。 您將為每個區域開發個別的模型，並瞭解如何使用*交叉預測*。  
  
-   **購物籃分析：** 您將建立*關聯模型*，以分析造訪[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]電子商務網站時所購買的產品群組。 您可以根據這個購物籃模型向客戶提供產品建議。  
  
-   **順序分析：** 您會建立時序*群集模型*，以分析客戶購買產品的順序。 您可以根據這個模型，計畫網站設計變更或規劃新產品供應項目。  
  
-   **因素分析：** 您可以使用類*神經網路*模型，在撥接中心資料中探索服務品質不佳的可能原因。 根據初步模型的見解，您將建立*羅吉斯回歸模型*，以預測改善客戶經驗的策略。  
  
## <a name="what-you-will-learn"></a>學習內容  
 這個教學課程告訴您如何建立和使用各種類型的資料採礦演算法。 這個教學課程分成下列課程：  
  
 [第1課：建立中繼資料採礦解決方案 &#40;元資料採礦教學課程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
 在這一課，您將根據 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫建立新專案，以便支援多個新資料來源檢視和更多的採礦模型。  
  
 [第2課：建立預測案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
 在這個課程中，您將建立預測狀況中所能使用的採礦模型。 另外，您還將探索 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法建立的採礦模型。  
  
 您將為各區域建立個別的模型，然後建立一個用來交叉預測的一般模型。  
  
 [第3課：建立購物籃案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
 在這個課程中，您將加入新的資料來源檢視，並學習如何使用巢狀資料表與索引鍵。 根據這項資料，您將建立購物籃狀況中所能使用的採礦模型。 此外，您還將探索 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯分析演算法建立的採礦模型。  
  
 [第4課：建立時序群集案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
 在這個課程中，您將建立時序群集狀況中所能使用的採礦模型。 另外，您也將學習如何探索 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時序群集演算法所建立的採礦模型。  
  
 [第5課：建立類神經網路和羅吉斯回歸模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
 在這一課，您將使用 Microsoft 類神經網路演算法和 Microsoft 羅吉斯迴歸演算法，建立數個相關的採礦模型。 另外，您也將學習如何使用資料來源檢視探索模型的基礎資料。  
  
## <a name="requirements"></a>需求  
 請確定已安裝下列項目：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 與 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫。  
  
 為了加強安全性，系統預設不會安裝範例資料庫。 若要安裝的正式資料庫[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請造訪[Microsoft SQL 範例資料庫](https://go.microsoft.com/fwlink/?LinkId=88417)頁面，並選取適當版本的範例資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [基本資料採礦教學課程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [自行車購買者 DMX 教學課程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [購物籃 DMX 教學課程](../../2014/tutorials/market-basket-dmx-tutorial.md)  
  
  
