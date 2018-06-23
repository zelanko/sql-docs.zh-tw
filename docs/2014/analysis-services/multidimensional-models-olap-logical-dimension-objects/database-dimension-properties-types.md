---
title: 維度類型 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- time dimensions [Analysis Services]
- quantitative dimensions [Analysis Services]
- BillOfMaterials dimension [Analysis Services]
- geography dimensions
- utility dimensions [Analysis Services]
- channel dimensions
- dimensions [Analysis Services], types
- products dimensions [Analysis Services]
- account dimensions [Analysis Services]
- organization dimensions
- currency dimensions [Analysis Services]
- rates dimensions
- promotion dimensions
- scenario dimensions [Analysis Services]
- customers dimensions [Analysis Services]
- Type property
ms.assetid: bd3195da-e762-4c98-b643-34c76e842343
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1fe0311a992f0f8c067ba6e7096698f96f8bc4bc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131596"
---
# <a name="dimension-types"></a>維度類型
  `Type` 屬性設定會提供關於維度內容的資訊給伺服器和用戶端應用程式。 在某些情況下，`Type` 設定只會提供用戶端應用程式的指導，而且是選擇性的。 在其他情況下 (例如 `Accounts` 或 `Time` 維度)，維度的 `Type` 屬性 (Property) 設定及其屬性 (Attribute) 會決定特定的伺服器型行為，且在 Cube 中實作某些行為時可能會需要用到。 例如，維度的 `Type` 屬性可設定為 `Accounts`，對用戶端應用程式指出標準維度包含帳戶屬性。 如需有關時間、 帳戶和貨幣維度的詳細資訊，請參閱[建立日期類型維度](../multidimensional-models/database-dimensions-create-a-date-type-dimension.md)，[建立父子式類型維度的財務帳戶](../multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)，和[建立貨幣輸入維度](../multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)。  
  
 維度類型的預設值是 `Regular`，亦即不會對維度的內容進行假設。 除非您在使用維度精靈定義維度時指定 `Time`，否則當您初始定義維度時，這就是所有維度的預設值。 如果維度精靈未列出維度類型的適當類型，則您也應將 `Regular` 保留為維度類型。  
  
## <a name="available-dimension-types"></a>可用的維度類型  
 下表描述中可用的維度類型[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
|維度類型|描述|  
|--------------------|-----------------|  
|一般|此維度的類型並未設定為特殊維度類型。|  
|Time|此維度的屬性代表時間週期，例如年數、半年數、季數、月數和日數。|  
|組織|此維度的屬性代表組織的資訊，例如員工或分公司。|  
|Geography|此維度的屬性代表地理資訊，例如城市或郵遞區號。|  
|BillOfMaterials|維度的屬性代表存貨或製造資訊 (例如產品的組件清單)。|  
|帳戶|此維度的屬性代表財務報表用途的帳戶圖表。|  
|客戶|此維度的屬性代表客戶或連絡資訊。|  
|產品|此維度的屬性代表產品資訊。|  
|狀況|此維度的屬性代表計畫或策略分析資訊。|  
|數量|此維度的屬性代表數量的資訊。|  
|公用程式|此維度的屬性代表其他資訊。|  
|CURRENCY|此維度類型包含貨幣資料和中繼資料。|  
|匯率|此維度的屬性代表貨幣匯率的資訊。|  
|通路|此維度的屬性代表通道資訊。|  
|促銷|此維度的屬性代表行銷促銷資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [使用現有的資料表建立維度](../multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [維度 &#40;Analysis Services-多維度資料 &#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  