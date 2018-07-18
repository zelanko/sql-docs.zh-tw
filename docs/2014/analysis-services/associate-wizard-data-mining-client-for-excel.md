---
title: 關聯精靈 （適用於 Excel 的資料採礦用戶端） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- nested tables, in association models
- association [data mining]
ms.assetid: 4db6462f-93c7-443f-8ff7-39474dc7029e
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ed09d260a7db66561af6cf80136c801ea46cc5a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37216608"
---
# <a name="associate-wizard-data-mining-client-for-excel"></a>關聯精靈 (適用於 Excel 的資料採礦用戶端)
  ![資料採礦功能區中的關聯精靈](media/dmc-associate.gif "資料採礦功能區中的關聯精靈")  
  
 關聯精靈可協助您使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯規則演算法建立資料採礦模型。 這類採礦模型會建立特別有用*推薦系統*。  
  
 其運作方式為：[!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯規則演算法會掃描由交易或事件組成的資料集，並尋找經常一起出現的組合。 可能有數千種組合，不過您可以自訂演算法來尋找較多或較少結果，並且僅保留最可能的組合。  
  
 您可以對許多問題套用關聯分析。 這個方法最常應用在購物籃分析，用於找出經常一起購買的個別產品。 您接著可以使用這項資訊，根據客戶已經購買的項目向客戶建議其他產品。  
  
## <a name="using-the-associate-wizard"></a>使用關聯精靈  
  
1.  在 **資料採礦**功能區中，按一下**關聯**。  
  
2.  在 [**選取來源資料**頁面上，選擇 Excel 資料表或資料範圍，然後按一下**下一步]**。  
  
     [關聯] 索引標籤中的範例資料活頁簿包含交易資料通常如何排列的範例；例如，每筆交易有多項產品或每個客戶有多筆購買記錄需要分析。  
  
     如果您想要使用外部資料來建立關聯模型中使用關聯精靈，您必須將資料加入 Excel 第一次，並*壓平合併*資料。 如需有關準備資料進行關聯模型的詳細資訊，請參閱 <<c0> [ 巢狀資料表&#40;Analysis Services-Data Mining&#41;](data-mining/nested-tables-analysis-services-data-mining.md)，在 SQL Server 線上叢書 》。</c0>  
  
3.  在 **關聯**頁面上，選擇識別交易的資料行。  
  
     若為購物籃模型，此識別碼表示您要建立模型的單位。 您是否要分析個別客戶在一段時間內購買的項目，或者您要分析涉及多個客戶的許多交易？ 在第一個案例中，您會選擇客戶識別碼；在第二個案例中，您會選擇採購單或其他交易識別碼。  
  
4.  針對**項目**，選取包含您要尋找關聯之項目之資料行。  
  
     例如，在購物籃模型中，您可以選擇產品欄位，以分析哪些產品經常一起購買。 如果有太多個別產品，而無法有效地相互關聯，您可以選擇產品類別目錄或子類別目錄欄位。  
  
5.  在 **閾值**，您可以設定值，控制或影響模型的輸出：  
  
    -   **最小支援。** 指定項目群組必須被視為重要的次數。 演算法會忽略不符合此準則的任何項目組合。 例如，您可能只想查看項目一起出現至少 10 次的項目集。  
  
    -   **最小規則機率**。 指定儲存規則所需的最小機率值。 系統會分析整個資料集以尋找所有組合，然後計算機率。 如果臨界值太低，則精靈可能會讓相互關聯性鬆散的項目產生關聯。 如果臨界值太高，則某些關聯可能會省略，因為這些關聯沒有足夠的支援資料。  
  
     一般而言，變更這些值會產生下列結果：  
  
    -   當您降低支援的值時，您會增加找到的組合數目。  
  
    -   當您減少最大支援時，您會篩選出太常發生，但是沒有什麼意義的項目。  
  
    -   當您降低規則的機率時，您會降低組合必須達到的門檻需求，才能在總資料集的內容中視為是重要的。  
  
     **提示：** 是個不錯的主意，若要建立使用支援與機率的不同組合的多個採礦模型。 若要追蹤您用於每個模型的設定，您可以使用**文件模型**for Excel 和使用資料採礦用戶端中提供精靈**Detailed**報表選項。 如需詳細資訊，請參閱 <<c0> [ 記載的採礦模型&#40;適用於 Excel 的資料採礦增益集&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)。</c0>  
  
6.  （選擇性） 按一下**參數**以變更演算法參數，並自訂採礦模型的行為。  
  
     演算法參數對話方塊包含您在精靈中設定的所有參數，以及幾個較少使用的參數，例如 MAXIMUM_SUPPORT。 如需有關如何使用這些參數的資訊，請參閱 < [Microsoft 關聯分析演算法技術參考](data-mining/microsoft-association-algorithm-technical-reference.md)。  
  
7.  在 **完成**頁面上，輸入資料集和模型的唯一名稱。  
  
8.  在 **選項**，您定義您要使用模型，完成後的方式：  
  
    -   **瀏覽**。  當模型就緒時，精靈會開啟視窗，以顯示規則、項目集及描述關聯的相依性網路圖表。  
  
         如需如何解譯關聯模型檢視器中的資料的詳細資訊，請參閱[瀏覽關聯規則模型](browsing-an-association-rules-model.md)。  
  
    -   **啟用鑽研**。 選取此選項可透過模型取得基礎資料的存取權。  
  
         例如，如果您想按一下特定項目集以查看來源資料，鑽研是很有用的方式。  
  
    -   **使用暫時性模型**。 如果您不想將模型儲存到伺服器上，請選取這個選項。 當您關閉 Excel 時，即會刪除暫時性模型。  
  
9. 精靈會分析所有可能的組合，並且建立包含項目集和規則的報表。  
  
## <a name="more-about-association-models"></a>進一步了解關聯模型  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯規則演算法會檢查定型資料來尋找一起出現在交易中的項目。 每個群組的項目構成*項目集*。 接著，演算法會計算每個項目集出現的次數，以及每個項目集在所有交易中的相對重要性。  
  
 演算法會使用關於項目集的這個資訊產生可用於預測關聯或進行建議的規則。 例如，規則可以如下：「如果使用者購買作者 1 和作者 2 的書，則這位使用者也可能會購買作者 3 的書」。 系統會根據關聯的強度來為每個建議指派機率。  
  
### <a name="requirements"></a>需求  
 若要使用關聯精靈，您必須連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。  
  
 您的來源資料必須組織成交易資料表， 來源資料必須包含一個含有交易識別碼的資料行， 此資料行會識別每一組項目。 該交易資料行必須與第二個資料行 (也就是項目識別碼) 具有一對多的關聯性，第二個資料行會儲存群組中個別項目的名稱或識別碼。  
  
 概念上而言，如果回想起購物車的範例，這可能是最容易了解的部分。 如果為購物車指派識別碼，此購物車識別碼會當做交易的識別碼。 購物車中的每一個項目 (如馬鈴薯或牛奶) 都是該筆交易的成員。 關聯分析演算法可跨交易追蹤項目，例如，用來判斷馬鈴薯和牛奶出現在任何單筆交易中的次數。  
  
 您的來源資料必須依據交易識別碼資料行排序。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)   
 [瀏覽關聯規則模型](browsing-an-association-rules-model.md)   
 [購物籃分析&#40;AnalysisTools 適用於 Excel 的資料表&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)   
 [相依性網路圖表逐步解說&#40;資料採礦增益集&#41;](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
  
