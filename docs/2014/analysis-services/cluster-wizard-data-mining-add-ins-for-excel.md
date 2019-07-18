---
title: 叢集精靈 （資料採礦適用於 Excel 的增益集） |Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087813"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>叢集精靈 (適用於 Excel 的資料採礦增益集)
  ![資料採礦功能區中的叢集精靈](media/dmc-cluster.gif "資料採礦功能區中的叢集精靈")  
  
 叢集精靈可協助您建立模型，此模型會偵測共用類似特性的資料列，並將這些資料列分組以最大化群組間的差距。 這個精靈對於尋找所有資料類型中的模式很有幫助。  
  
 叢集精靈使用 Microsoft 叢集演算法，並可廣泛地加以自訂。 該精靈使用 Excel 資料表、Excel 範圍或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 查詢中的現有資料。 藉由提供類似的功能[偵測類別目錄](detect-categories-table-analysis-tools-for-excel.md)工具，適用於 Excel 的資料表分析工具中提供。 但是，您無法自訂偵測類別目錄工具，且該工具必須使用 Excel 資料表中的資料。  
  
## <a name="using-the-cluster-wizard"></a>使用叢集精靈  
  
1.  在 [資料採礦功能區中，按一下**叢集**，然後按一下**下一步]** 。  
  
2.  在 **選取來源資料**頁面上，選取 Excel 資料表或範圍。 或指定外部資料來源。  
  
     如果使用外部資料來源，您可以建立自訂檢視或貼入自訂查詢文字，然後將資料集儲存為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源。  
  
3.  在 [**群集**] 頁面上，您可以自訂建置模型的方式。  
  
    -   針對**的區段數目**，您可以告知精靈建立固定的數目的類別目錄，或讓它自動偵測最佳的群組數目。  
  
    -   檢閱清單中的資料行**輸入資料行**清單，然後取消選取任何不適合建立模式的資料行。 您應排除的資料行包括識別碼、客戶名稱等。  
  
4.  （選擇性） 按一下**參數**以變更演算法參數，並自訂叢集模型的行為。  
  
5.  在 **將資料分割成定型集和測試集**頁面上，指定要進行測試的資料量。 定型模型時，一律會使用其餘資料。  
  
     預設設定為 30% 測試資料和 70% 定型資料。  
  
6.  在 **完成**頁面上，提供您的資料集和模型的描述性名稱，然後設定下列選項可控制如何使用完成的模型：  
  
    -   **瀏覽模型**。 選取此選項時，只要精靈完成處理模型，它會開啟**瀏覽**幫助您探索結果 視窗。 檢視器的內容取決於建立的模型類型。 如需詳細資訊，請參閱 <<c0> [ 瀏覽叢集模型](browsing-a-clustering-model.md)。  
  
    -   **啟用鑽研**。 選取此選項可檢視完成模型中的基礎資料。 只有建立決策樹模型時，才能使用這個選項。  
  
    -   **使用暫時性模型**。 如果選取這個選項，此模型將無法儲存到伺服器。 當您關閉 Excel 時，即會刪除暫時性模型。  
  
## <a name="more-about-clustering-models"></a>進一步了解叢集模型  
 您可以變更，即可使用此精靈的群集演算法**進階**並用**演算法參數** 對話方塊。  
  
 Microsoft 群集演算法提供下列群集方法：  
  
-   K-means - 可擴充或不可擴充。  
  
-   Expectation Maximization (EM) - 可擴充或不可擴充。  
  
 您也可以使用 CLUSTER_SEED 參數控制此起始值，以確保使用相同資料集的重複模型擁有相同的結果。  
  
### <a name="requirements"></a>需求  
 您必須連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，才能使用 [叢集] 精靈。 如需詳細資訊，請參閱 <<c0> [ 連接至來源的資料&#40;適用於 Excel 的資料採礦用戶端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)   
 [偵測類別目錄&#40;適用於 Excel 的資料表分析工具&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
