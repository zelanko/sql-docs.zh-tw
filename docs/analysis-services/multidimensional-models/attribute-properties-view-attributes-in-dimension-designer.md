---
title: "在維度設計師中檢視屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying attributes
- attributes [Analysis Services], viewing
- viewing attributes
ms.assetid: 855bef07-b72d-4ce3-bf02-de77abeee71a
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e73cba395d806e834dc03e7f7cd79d030eb5c36e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-properties---view-attributes-in-dimension-designer"></a>屬性的內容位在維度設計師中檢視屬性
  屬性是在維度物件上建立的。 您可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的維度設計師，檢視和設定屬性。 維度設計師之 [維度結構] 索引標籤的 [屬性] 窗格，會列出維度中的屬性。 使用此窗格，即可加入、移除或設定屬性。 您也可以選取屬性，以用來做為新階層中的層級，或者加入做為現有階層的層級。  
  
 若要檢視維度中的屬性，請針對維度開啟維度設計師。 設計師之 [維度結構] 索引標籤的 [屬性] 窗格，會顯示維度中的屬性。 您可以指向 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 之 [維度] 功能表上的 [顯示屬性於]，然後按一下下列命令之一，在清單、樹狀或方格檢視之間切換：  
  
1.  顯示屬性於 [清單] 中。 以清單格式顯示屬性。 以滑鼠右鍵按一下某個屬性，即可將屬性從清單中刪除、將屬性重新命名，或者變更屬性的使用方式。 使用此檢視建立階層。 屬性 (Attribute) 資訊和成員屬性 (Property) 是看不到的。  
  
2.  顯示屬性於 [樹狀] 中。 以樹狀格式顯示屬性，且維度是樹狀中的最上層節點。 執行下列動作，即可展開屬性來檢視其屬性關聯性，或是建立新的屬性關聯性：  
  
    -   按一下維度、屬性 (Attribute) 或成員屬性 (Property)，即可在 [屬性] \(Property) 視窗中檢視其屬性 (Property)。  
  
    -   以滑鼠右鍵按一下屬性 (Attribute) 或成員屬性 (Property)，即可從清單刪除屬性、將屬性重新命名，或者變更屬性的使用方式。  
  
     使用此檢視，即可檢視和建立成員屬性。 也您可以使用此檢視來建立階層。  
  
3.  顯示屬性於 [方格] 中。 以方格格式顯示屬性。 方格會顯示下列資料行：  
  
    -   [名稱] 會顯示 **Name** 屬性的值。 輸入其他名稱即可變更設定。  
  
    -   [使用方式] 會指定這是 Regular、Key、Parent 或 AccountType 屬性。 按一下此資料行中的值，即可選取其他設定。  
  
    -   [類型] 會指定屬性的商業智慧類別目錄。 按一下此資料格，即可選取其他設定。  
  
    -   [索引鍵資料行] 會顯示屬性 (Attribute) 上之 **KeyColumn** 屬性 (Property) 的 OLE DB 資料類型。 無法變更此資料行。  
  
    -   [名稱資料行] 指出屬性 (Attribute) 上的 **NameColumn** 屬性 (Property) 設定，是否與 **KeyColumn** 屬性 (Property) 的設定是同一個資料行。 無法變更此資料行。  
  
     按一下方格中的任一個資料列，即可檢視該屬性 (Attribute) 的屬性 (Property)。  
  
     使用此檢視來建立和設定屬性。  
  
 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，下表裡顯示的圖示會根據屬性的使用方式標示屬性。  
  
|圖示|屬性使用方式|  
|----------|---------------------|  
|![屬性圖示](../../analysis-services/multidimensional-models/media/as-icon-attribute.gif "屬性圖示")|Regular 或 AccountType|  
|![索引鍵屬性圖示](../../analysis-services/multidimensional-models/media/as-icon-key-attribute.gif "索引鍵屬性圖示")|索引鍵|  
|![父屬性圖示](../../analysis-services/multidimensional-models/media/as-icon-parent-attribute.gif "父屬性圖示")|父系|  
  
## <a name="see-also"></a>請參閱＜  
 [維度屬性 (Attribute) 屬性 (Property) 參考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  

