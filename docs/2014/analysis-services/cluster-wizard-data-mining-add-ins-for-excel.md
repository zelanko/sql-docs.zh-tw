---
title: 叢集 Wizard （適用于 Excel 的資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [data mining]
ms.assetid: 85b25625-a7ab-4960-9f9c-df22e8ecae37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d93f676aec67b5d791924cbbda8f71a966d5bbc2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087813"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>叢集精靈 (適用於 Excel 的資料採礦增益集)
  ![資料採礦功能區中的群集精靈](media/dmc-cluster.gif "資料採礦功能區中的群集精靈")  
  
 叢集精靈可協助您建立模型，此模型會偵測共用類似特性的資料列，並將這些資料列分組以最大化群組間的差距。 這個精靈對於尋找所有資料類型中的模式很有幫助。  
  
 叢集精靈使用 Microsoft 叢集演算法，並可廣泛地加以自訂。 該精靈使用 Excel 資料表、Excel 範圍或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 查詢中的現有資料。 適用于 Excel 的資料表分析工具中提供的 [偵測[類別目錄](detect-categories-table-analysis-tools-for-excel.md)] 工具提供類似的功能。 但是，您無法自訂偵測類別目錄工具，且該工具必須使用 Excel 資料表中的資料。  
  
## <a name="using-the-cluster-wizard"></a>使用叢集精靈  
  
1.  在 [資料採礦] 功能區中 **，按一下 [** 叢集]，然後按 **[下一步]**。  
  
2.  在 [**選取來源資料**] 頁面中，選取 Excel 資料表或範圍。 或指定外部資料來源。  
  
     如果使用外部資料來源，您可以建立自訂檢視或貼入自訂查詢文字，然後將資料集儲存為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源。  
  
3.  在 [**群集**] 頁面上，您可以自訂模型的建立方式。  
  
    -   對於**區段數目**，您可以告訴 wizard 建立固定數目的類別，或讓它自動偵測最佳的群組數目。  
  
    -   檢查 [**輸入資料行**] 清單中的資料行清單，並取消選取在建立模式時不適用的任何資料行。 您應排除的資料行包括識別碼、客戶名稱等。  
  
4.  （選擇性）按一下 [**參數**] 以變更演算法參數，並自訂群集模型的行為。  
  
5.  在 [將**資料分割成定型集和測試集**] 頁面上，指定要保留多少資料來進行測試。 定型模型時，一律會使用其餘資料。  
  
     預設設定為 30% 測試資料和 70% 定型資料。  
  
6.  在 [**完成]** 頁面上，為您的資料集和模型提供描述性的名稱，並設定下列選項來控制如何使用完成的模型：  
  
    -   **流覽模型**。 選取這個選項時，一旦 wizard 完成模型的處理，就會開啟 **[流覽**] 視窗以協助您流覽結果。 檢視器的內容取決於建立的模型類型。 如需詳細資訊，請參閱[流覽群集模型](browsing-a-clustering-model.md)。  
  
    -   **啟用 [鑽取**]。 選取此選項可檢視完成模型中的基礎資料。 只有建立決策樹模型時，才能使用這個選項。  
  
    -   **使用暫時性模型**。 如果選取這個選項，此模型將無法儲存到伺服器。 當您關閉 Excel 時，即會刪除暫時性模型。  
  
## <a name="more-about-clustering-models"></a>進一步了解叢集模型  
 您可以按一下 [ **Advanced** ]，然後使用 [**演算法參數**] 對話方塊來變更此 wizard 所使用的群集演算法。  
  
 Microsoft 群集演算法提供下列群集方法：  
  
-   K-means - 可擴充或不可擴充。  
  
-   Expectation Maximization (EM) - 可擴充或不可擴充。  
  
 您也可以使用 CLUSTER_SEED 參數控制此起始值，以確保使用相同資料集的重複模型擁有相同的結果。  
  
### <a name="requirements"></a>需求  
 您必須連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，才能使用 [叢集] 精靈。 如需詳細資訊，請參閱[連接到來源資料 &#40;適用于 Excel&#41;的資料採礦用戶端](connect-to-source-data-data-mining-client-for-excel.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)   
 [偵測適用于 Excel&#41;&#40;資料表分析工具的分類](detect-categories-table-analysis-tools-for-excel.md)  
  
  
