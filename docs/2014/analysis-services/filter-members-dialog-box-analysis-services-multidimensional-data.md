---
title: 篩選成員對話方塊 (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dimensiondesigner.filtermembers.f1
helpviewer_keywords:
- Filter Members dialog box
ms.assetid: 52c6da1d-9fb5-4dbc-bffa-248d11cd337c
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fd9ab683243b938ed50c6e71cb7e438974ac7097
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022294"
---
# <a name="filter-members-dialog-box-analysis-services---multidimensional-data"></a>篩選成員對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [篩選成員] 對話方塊，即可在 [維度設計師] 的 [瀏覽器] 索引標籤中瀏覽維度時，依成員標題、成員名稱、成員唯一的名稱、索引鍵資料行的值或值資料行的值，篩選目前層級的維度成員。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**篩選條件運算式**|顯示用來建構篩選運算式之屬性、運算子和值的方格。 請注意，在加入資料列之後，就無法移除該資料列。 您必須關閉和重新開啟對話方塊，以指定新的篩選運算式。 方格包含下列資料行：<br /><br /> **屬性**： 選取要用於篩選運算式之成員的屬性。<br /><br /> **運算子**： 選取要用於篩選運算式的運算子。<br /><br /> **值**： 輸入中所選取的屬性值**屬性**以評估使用在指定的運算子**運算子**。|  
|**測試窗格**|按一下 [測試] 時，此窗格會顯示篩選運算式傳回的成員。 如果使用 [篩選運算式] 中指定的準則而沒有傳回任何成員，則會顯示警告。|  
|**測試**|按一下即可測試 [篩選運算式] 中指定的準則。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [瀏覽器&#40;維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](browser-dimension-designer-analysis-services-multidimensional-data.md)  
  
  