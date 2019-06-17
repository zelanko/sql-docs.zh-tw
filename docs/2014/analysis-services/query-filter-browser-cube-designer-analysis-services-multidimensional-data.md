---
title: 查詢和篩選 （瀏覽器索引標籤，Cube 設計師） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.filterpane.f1
ms.assetid: f5cf0bb1-3afb-4856-a2ef-614deb4e7e49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d788a4957d7c6b3ea02e407f8b09fa80b957a4b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070543"
---
# <a name="query-and-filter-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>查詢和篩選 (瀏覽器索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  Cube 設計師中的 [瀏覽器]  索引標籤區域包含查詢和篩選區域，以協助您從 Cube 選擇用於瀏覽或查詢的資料。 您可以加入所需的 Cube 物件數，然後在資料區域中檢視結果，或者使用 [在 Excel 中進行分析] 將結果匯出至報表，以視覺化使用者檢使用者使用者檢視資料的方式。  
  
> [!WARNING]  
>  當您正在處理此區域中的資料時，[瀏覽器]  會使用圖形設計模式。 不過，您可以使用 MDX，或按一下 [設計模式]  切換按鈕，直接編輯該查詢。 當您這樣做時，可讓您設計的窗格會在維度消失時篩選。 如果您要加入篩選，可以切換回圖形設計模式。  
  
 根據預設，執行查詢時，目前使用者的認證 (而非在 [模擬資訊]  頁面中指定的認證) 會用來連接資料來源。 不過，您也可以按一下 [工具列]  上的 [變更使用者]  ，變更查詢或報表的使用者內容。  
  
## <a name="options"></a>選項  
 **Dimension**  
 選取要配量 Subcube 的維度。  
  
 **Hierarchy**  
 選取要配量 Subcube 的階層。  
  
 **運算子**  
 選取運算子，定義 [篩選運算式]  中的運算式如何套用至所選取階層。 下表描述可用的運算子。  
  
|值|描述|  
|-----------|-----------------|  
|**Equal**|結果會限制為 **[篩選運算式]** 中定義的集合。|  
|**不等於**|結果會限制為 **[篩選運算式]** 中定義之集合所排除的成員。|  
|**In**|結果會限制為 **[篩選運算式]** 中選擇的命名集。|  
|**不在**|結果會限制為 **[篩選運算式]** 中選擇之命名集所排除的成員。|  
|**包含**|結果會限制為成員名稱中包含 **[篩選運算式]** 中的字串之成員。|  
|**開始使用**|結果會限制為成員名稱是以 **[篩選運算式]** 中的字串開頭之成員。|  
|**範圍 （內含）**|結果會限制為 **[篩選運算式]** 中選擇的範圍。|  
|**範圍 （獨佔）**|結果會限制為 **[篩選運算式]** 中選擇之範圍所排除的成員。|  
|**MDX**|結果會限制為 [篩選運算式]  中的多維度運算式 (MDX) 運算式集合。|  
  
 **篩選運算式**  
 鍵入 [運算子]  所要評估的運算式，這會限制要瀏覽的結果。  
  
> [!NOTE]  
>  此欄位是一個動態資料輸入元素，外觀會變更以反映選取之運算子所需要的資料類型。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 設計師&#40;Analysis Services-多維度資料&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [瀏覽器&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [工具列&#40;瀏覽器索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [在 Excel 中分析&#40;瀏覽器索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [中繼資料&#40;瀏覽器索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
