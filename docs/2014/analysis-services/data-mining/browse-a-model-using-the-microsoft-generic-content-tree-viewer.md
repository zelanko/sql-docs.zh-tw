---
title: 瀏覽模型，使用 Microsoft 一般內容樹狀檢視器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, viewing
ms.assetid: 4a5f7c51-c704-4214-b05d-21cf735e6d96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e0d945e1fe95fe95d8ed655a0bd6b94e132f3c9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48176281"
---
# <a name="browse-a-model-using-the-microsoft-generic-content-tree-viewer"></a>使用 Microsoft 一般內容樹狀檢視器瀏覽模型
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般採礦模型內容檢視器能針對採礦演算法所找到的模式提供詳細的資訊，也可以用來存取在分析程序期間所產生的各種統計資料。 資訊的量及類型是根據使用的演算法而定，但可能包含下列類別：  
  
-   資料區段和它們的特性。  
  
-   有關每個群組或整組資料的描述性統計資料。  
  
-   樹狀結構中的分支或子節點數。  
  
-   群集或整組資料的計算，例如變異數和平均。  
  
 檢視這項資訊有助於更了解分析的結果。 您也可以識別微調的方法，然後重新培訓模型， 或者決定使用不同的演算法進行重新培訓。  
  
## <a name="viewing-mining-model-content"></a>檢視採礦模型內容  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容檢視器會從採礦模型的 *「內容結構描述資料列集」* (Content Schema Rowset) 顯示資料行、規則、屬性 (Property)、屬性 (Attribute)、節點和其他內容。 內容結構描述資料列集是一般性架構，用來展示有關資料採礦模型內容的詳細資訊。  
  
 此詳細資訊包含在一個 HTML 資料表中，該資料表將模型中的模式、叢集或樹狀表示為節點。 您可以按一下各節點，然後將其展開以查看詳細資料，例如公式或數值屬性的相異值計數。 您也可以瀏覽節點之間的父子式關聯性。  
  
 如需採礦模型內容中所使用術語之一般意義的詳細資訊，請參閱[採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-analysis-services-data-mining.md)。 這個主題也包含連結，提供關於特定類型模型之採礦模型內容的資訊。 每種類型的採礦模型都包含演算法專屬的資訊以及在資料中找到的模式，因此，建議您查閱每個模型類型的技術參考主題，以了解每個模型類型的完整資訊。  
  
## <a name="querying-mining-model-content"></a>查詢採礦模型內容  
 由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容樹狀檢視器所提供的相同資訊，也可藉由查詢採礦模型而提供。 您可以藉由使用資料採礦延伸模組 (DMX) 陳述式來針對採礦模型內容建立查詢。 例如，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，您可以執行下列 DMX 陳述式來執行內容查詢：  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 如需詳細資訊，請參閱 [資料採礦查詢](data-mining-queries.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 一般內容樹狀檢視器&#40;資料採礦&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)   
 [資料採礦演算法&#40;Analysis Services-資料採礦&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
  
