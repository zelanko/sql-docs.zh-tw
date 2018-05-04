---
title: Microsoft 線性迴歸演算法 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- linear regression algorithms [Analysis Services]
- linear regression [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 50a4abb8-c0b0-4380-ba5e-c49b305b9d22
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 15fd60a8cf05e501fda781e76fd716a45c0df1ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-linear-regression-algorithm"></a>Microsoft 線性迴歸演算法
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法的變異形式，可幫助您計算相依與獨立變數之間的線性關聯性，然後使用該關聯性進行預測。  
  
 關聯性會以最能夠代表一系列資料的線性方程式表示。 例如，下列圖表中的線條是最佳的資料線性表示法。  
  
 ![模型的一組資料列](../../analysis-services/data-mining/media/linear-regression.gif "模型的一組資料行")  
  
 圖表中的每一個資料點都有錯誤，與它到迴歸線的距離相關聯。 迴歸方程式中的係數 a 和 b 會調整迴歸線的角度和位置。 您可以調整 a 和 b，直到與所有點相關聯的錯誤總和達到最小值為止，以取得迴歸方程式。  
  
 還有其他種類的迴歸會使用多個變數，以及迴歸的非線性方法。 但是，線性迴歸是一個實用且知名的方法，可將某個基礎因數之變更的回應模型化。  
  
## <a name="example"></a>範例  
 您可以使用線性迴歸來決定兩個連續資料行之間的關聯性。 例如，您可以使用線性迴歸，從製造或銷售資料計算趨勢線。 您也可以使用線性迴歸當做開發更複雜之資料採礦模型的先驅，以評估資料行之間的關聯性。  
  
 雖然有許多方法可計算線性迴歸，而不需要資料採礦工具，但是針對這項工作使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法的好處在於，變數之間所有可能的關聯性都會自動計算出來，並加以測試。 您不必選取計算方法，例如最小平方的解決方式。 但是，在有多個因數影響結果的狀況下，線性迴歸可能會過於簡化關聯性。  
  
## <a name="how-the-algorithm-works"></a>演算法的運作方式  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法的變異形式。 當您選取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法時，會叫用特殊形式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法，其參數會限制此演算法的行為，而且需要某些輸入資料類型。 此外，在線性迴歸模型中，整個資料集都會用來計算初始行程內的關聯性，而標準決策樹模型則會將資料重複分割成較小的子集或樹狀結構。  
  
## <a name="data-required-for-linear-regression-models"></a>線性迴歸模型所需的資料  
 當您準備資料以供線性迴歸模型使用時，您需要了解特定演算法的需求。 其中包括所需的資料數量及資料的使用方式。 此模型類型的需求如下：  
  
-   **單一索引鍵資料行** ：每個模型都必須包含一個能唯一識別每一筆記錄的數值或文字資料行。 不允許複合的索引鍵。  
  
-   **可預測資料行** ：至少需要一個可預測資料行。 您可以在模型中加入多個可預測的屬性，但是這些可預測的屬性必須是連續數值資料類型。 即使資料的原生儲存體為數值，您還是不能將日期時間資料類型當做可預測的屬性使用。  
  
-   **輸入資料行** ：輸入資料行必須包含連續數值資料，而且必須為它指派適當的資料類型。  
  
 如需詳細資訊，請參閱的 [Microsoft 線性迴歸演算法技術參考](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)的＜需求＞一節。  
  
## <a name="viewing-a-linear-regression-model"></a>檢視線性迴歸模型  
 若要瀏覽此模型，您可使用 [Microsoft 樹狀檢視器]。 線性迴歸模型的樹狀結構非常簡單，其中包含有關單一節點內所包含之迴歸方程式的所有資訊。 如需詳細資訊，請參閱 [使用 Microsoft 樹狀檢視器瀏覽模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)。  
  
 如果您想要知道此方程式的詳細資料，也可以使用 [Microsoft 一般內容樹狀檢視器](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)來檢視係數和其他詳細資料。  
  
 如果是線性迴歸模型，此模型內容包含中繼資料、迴歸公式及有關輸入值分佈的統計資料。 如需詳細資訊，請參閱 [線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)的＜需求＞一節。  
  
## <a name="creating-predictions"></a>建立預測  
 當此模型已處理完之後，結果會儲存成一組統計資料，連同線性迴歸公式 (這些公式可用來計算未來趨勢)。 如需搭配線性迴歸模型使用之查詢的範例，請參閱 [線性迴歸模型查詢範例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)。  
  
 如需如何針對採礦模型建立查詢的一般資訊，請參閱 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)。  
  
 除了選取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法來建立線性迴歸模型之外，如果可預測屬性為連續數值資料類型，您也可以建立一個包含迴歸的決策樹模型。 在此情況下，此演算法會在找到適當的分隔點時分割資料，但如果是某些資料區，則會改為建立迴歸公式。 如需決策樹模型內之迴歸樹的詳細資訊，請參閱[決策樹模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)。  
  
## <a name="remarks"></a>備註  
  
-   不支援使用預測模型標記語言 (PMML) 來建立採礦模型。  
  
-   不支援建立資料採礦維度。  
  
-   支援鑽研。  
  
-   支援 OLAP 採礦模型的使用。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services-資料採礦 &#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft 線性迴歸演算法技術參考](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)   
 [線性迴歸模型查詢範例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)   
 [線性迴歸模型 & #40; 的採礦模型內容Analysis Services-資料採礦 & #41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
