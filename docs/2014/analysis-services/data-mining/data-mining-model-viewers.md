---
title: 資料採礦模型檢視器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- displaying data mining models
- mining models [Analysis Services], viewing
- data mining [Analysis Services], models
- viewing data mining models
- mining model content
- support [data mining]
- exploring data mining models [Analysis Services]
ms.assetid: 14c8e656-f63c-4e8a-a3af-1d580e823d28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: adbed9b575be07354cfe1d1a3bf5f2c0526f458c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722834"
---
# <a name="data-mining-model-viewers"></a>資料採礦模型檢視器
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中定型資料採礦模型之後，您可以瀏覽該模型來尋找值得參考的趨勢。 因為採礦模型的結果很複雜，而且其原始格式不易了解，所以用視覺化方式調查資料通常是了解演算法在資料內探索的規則和關聯性的最簡單方式。  
  
 您用來建立模型的每一個演算法都會傳回不同類型的結果。 因此， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會為每一個演算法提供個別的檢視器。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中瀏覽採礦模型時，該模型會使用適合它的檢視器顯示在資料採礦設計師的 **[採礦模型檢視器]** 索引標籤上。  
  
## <a name="how-to-use-the-model-viewers"></a>如何使用模型檢視器  
 您要先選取採礦模型，然後再選取檢視器。 每一個模型一定都有兩個可用的檢視器：自訂檢視器 (可包含多個索引標籤) 和一般檢視器。  
  
 根據您選取的模型類型而定，您會看到瀏覽模型的不同選項。 與每一個模型類型有關的自訂檢視器會依照您用來建立選定資料採礦模型的演算法而訂製。 每一個自訂檢視器都有各種工具和對話方塊，可幫助您瀏覽模型中的統計資料和模式、檢視圖表，或是以互動方式處理機率臨界值或依名稱篩選掉項目。  
  
 下圖說明當您為相同的模型選擇自訂檢視器和一般檢視器時，兩者之間的差異。  
  
1.  首先，您會看到當您選取以 Microsoft 時間序列演算法為根據的採礦模型時，所顯示的自訂檢視器。  
  
     這個特定自訂檢視器會自動建立時間序列的圖形，並提供五個預測。  
  
2.  接下來，您會看到使用 **[Microsoft 一般內容樹狀檢視器]** 時所顯示的相同模型。  
  
     一般檢視器會在左邊顯示模型中的節點清單。 您可以按一下節點，在右窗格中檢視其內容。  
  
 ![採礦模型設計工具的概觀](../media/generic-mining-model-tab1.gif "採礦模型設計工具的概觀")  
  
## <a name="more-about-the-microsoft-generic-content-tree-viewer"></a>Microsoft 一般內容樹狀檢視器詳細資料  
 您也可以使用 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](../microsoft-generic-content-tree-viewer-data-mining.md) 來檢視每個模型。 此檢視器會根據標準 HTML 表格格式來呈現採礦模型的內容。 但是，節點的排列和每一個節點的內容將會因為用來產生結果的演算法而有很大的差異。  
  
 雖然自訂檢視器的設計目的是要了瀏覽及了解模型，但是當您已經了解此模型而且想要從特定節點擷取統計資料或規則時，一般檢視器會更為實用。 例如，當您想要檢視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在分析期間擷取之有關模式與統計資料的詳細資訊 (例如節點的機率或迴歸公式) 時，您會使用一般檢視器。  
  
 您也可以使用 DMX 撰寫 *「內容查詢」* (Content Query)，以取得在此檢視器中呈現的所有資訊。 如需詳細資訊，請參閱 [內容查詢 &#40;資料採礦&#41;](content-queries-data-mining.md)。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題會更詳細描述每一個檢視器以及如何解譯其中的資訊。  
  
 [使用 Microsoft 樹狀檢視器瀏覽模型](browse-a-model-using-the-microsoft-tree-viewer.md)  
 描述 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 樹狀檢視器。 這個檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法建立的採礦模型。  
  
 [使用 Microsoft 叢集檢視器瀏覽模型](browse-a-model-using-the-microsoft-cluster-viewer.md)  
 描述 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集檢視器。 這個檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法建立的採礦模型。  
  
 [使用 Microsoft 時間序列檢視器瀏覽模型](browse-a-model-using-the-microsoft-time-series-viewer.md)  
 描述 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列檢視器。 這個檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法建立的採礦模型。  
  
 [使用 Microsoft 貝氏機率分類檢視器瀏覽模型](browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
 描述 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類檢視器。 這個檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類演算法建立的採礦模型。  
  
 [使用 Microsoft 時序叢集檢視器瀏覽模型](browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
 描述 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集檢視器。 這個檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法建立的採礦模型。  
  
 [使用 Microsoft 關聯規則檢視器瀏覽模型](browse-a-model-using-the-microsoft-association-rules-viewer.md)  
 描述 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯規則檢視器。 這個檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯分析演算法建立的採礦模型。  
  
 [使用 Microsoft 類神經網路檢視器瀏覽模型](browse-a-model-using-the-microsoft-neural-network-viewer.md)  
 描述 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路檢視器。 這個檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法建立的採礦模型，包括使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 羅吉斯迴歸演算法的模型。  
  
 [使用 Microsoft 一般內容樹狀檢視器瀏覽模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)  
 描述一般檢視器中可用於所有資料採礦模型的詳細資訊，並提供範例說明如何解譯每種演算法的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [資料採礦設計師](data-mining-designer.md)  
  
  
