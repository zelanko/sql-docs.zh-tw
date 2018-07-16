---
title: 轉譯資料區域 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4f3b2c7d-3669-457f-899b-b758d1db3426
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c1dfbb97a7b02ebaaa82369f7d1883ad4d2eb299
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321748"
---
# <a name="rendering-data-regions-report-builder-and-ssrs"></a>轉譯資料區 (報表產生器及 SSRS)
  除了適用於所有報表項目的一般轉譯行為之外，資料區也擁有所遵循的其他分頁與轉譯行為。 資料區域特定的轉譯規則包括如何擴展資料區域；如何轉譯特殊資料格，例如，邊角資料格或標頭資料格；以及如何轉譯由右至左讀取的資料區域。 本主題討論如何轉譯資料區的各個部分。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="tablix-data-regions"></a>Tablix 資料區  
 可讓您建立資料表、矩陣與清單的 Tablix 資料區會轉譯為由資料行和資料列組成的方格。 資料列與資料行的交集就是資料格。 進行轉譯時，此資料格可以包含資料或其他報表項目，例如，影像、矩形、文字方塊或子報表。 Tablix 資料區可以用垂直和/或水平方式擴展。 此外，邊角資料格、資料區域的標頭資料格，以及資料區域的主體資料格可以根據其內容而擴展。 如果資料區跨越多個頁面，在顯示資料區的每一個頁面上，都會轉譯設定為隨著資料區重複的報表項目。 如需詳細資訊，請參閱 <<c0> [ 列出&#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)。</c0>  
  
### <a name="right-to-left"></a>由右至左  
 設定為由右至左顯示的 Tablix 資料區會隨著其結構，轉譯為資料區的鏡映影像 (如果是由左至右轉譯)。 資料區域的邊角會出現在右上角。 如果報表中有動態資料行，則會向左展開。 由右至左設定不會影像資料區域中資料的順序，只有您的資料行順序會有所不同。  
  
### <a name="tablix-headers"></a>Tablix 標頭  
 Tablix 標頭會根據標頭資料格出現在資料列群組階層或資料行群組階層中的位置，轉譯為資料列標頭或資料行標頭。 如果標頭的資料格內容中有邏輯分頁符號，則該符號會被忽略。 系統會忽略資料行群組的邏輯分頁符號。  
  
 群組的邏輯分頁符號則不會使外部群組標頭分頁。 例如，假設您的報表有一個國家 (地區) 的外部群組，以及一個國家地區的內部群組。 如果在國家地區群組的執行個體之間有邏輯分頁符號，則外部群組 (也就是國家 (地區)) 將會同時出現在報表的兩個頁面上。  
  
#### <a name="repeated-tablix-headers"></a>重複的 Tablix 標頭  
 在 [屬性] 窗格中設定 RepeatWith 屬性時，在資料區中沒有變更的項目 (例如資料行標頭) 在轉譯部分資料區的每個頁面上會重複。 例如，如果資料的資料列出現在下一個頁面上，而且有設定 [重複] 屬性，資料行標頭就也會出現在轉譯的頁面上。  
  
### <a name="tablix-corner"></a>Tablix 邊角  
 左上角稱為 Tablix 邊角。 Tablix 邊角可以包含其中的其他報表項目，但是，如果有將邏輯分頁符號插入到邊角中，系統在轉譯 Tablix 資料區時，則會忽略這些項目。  
  
### <a name="tablix-body"></a>Tablix 主體  
 Tablix 主體是由 Tablix 資料格所組成。 Tablix 主體會根據報表項目的分頁規則與轉譯行為進行轉譯。 如需詳細資訊，請參閱 <<c0> [ 轉譯報表項目&#40;報表產生器及 SSRS&#41;](rendering-report-items-report-builder-and-ssrs.md)。</c0>  
  
## <a name="chart-gauge-and-map-data-regions"></a>圖表、量測計以及對應資料區域  
 當系統轉譯圖表、量測計以及對應資料區域並顯示在報表主體中時，其行為如同影像。 資料區域內的值可以擁有相關聯的動作 (例如，連結到其他報表或移至書籤)，而且，如果轉譯器有提供支援，也可以轉譯這些動作。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)   
 [不同報表轉譯延伸模組的互動式功能&#40;報表產生器及 SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [轉譯報表項目 &#40;報表產生器及 SSRS&#41;](rendering-report-items-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [量測計 &#40;報表產生器及 SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
