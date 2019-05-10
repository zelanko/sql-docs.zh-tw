---
title: 衍生階層 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies
- hierarchies [Master Data Services], derived hierarchies
- derived hierarchies, about derived hierarchies
ms.assetid: a0fbd519-a10e-4cbd-92e6-5de9b8d3e3f0
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: af5bbc51420d8f32144bc91f687ae58b86d10d52
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479409"
---
# <a name="derived-hierarchies-master-data-services"></a>衍生階層 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 衍生階層衍生自已存在於模型中實體之間的網域屬性關聯性。  
  
 您可以建立衍生階層，以反白顯示模型中任何現有的網域屬性關聯性。  
  
## <a name="leaf-members-group-other-leaf-members"></a>分頁成員群組其他分頁成員  
 在衍生階層中，會使用來自某個實體的分頁成員為另一個實體的分頁成員分組。 衍生階層是以這些實體間的關聯性為基礎。 相反地，明確階層是僅以單一實體的成員為基礎，並以您指定的任何方式予以結構化。  
  
 您可以變更衍生階層的結構，而不影響基礎資料。 只要關聯性仍然存在於模型中，刪除衍生階層就不會影響主要資料。  
  
## <a name="explicit-hierarchies-versus-derived-hierarchies"></a>明確階層與衍生階層的比較  
 下表顯示明確階層與衍生階層之間的某些差異。  
  
|明確階層|衍生階層|  
|--------------------------|-------------------------|  
|結構是由使用者所定義|結構衍生自網域屬性之間的關聯性|  
|包含來自單一實體的成員|包含來自多個實體的成員|  
|使用合併成員群組其他成員|使用某個實體的分葉成員群組另一個實體的分葉成員|  
|可以是不完全的|永遠包含固定數目的層級|  
  
## <a name="creating-a-variable-depth-hierarchy"></a>建立可變深度的階層  
 有兩種建議的方式可建立可變深度的階層：  
  
-   如果您需要所有層級擁有相同的屬性，則建立單一實體，然後使用以實體為基礎的網域屬性在這個實體上建立遞迴階層。  
  
-   如果您需要一組屬性用於分葉成員，以及另一組屬性用於上層，請為衍生階層建立兩個實體。 若是分葉實體，請使用以父實體為基礎的網域屬性。 若是父實體，請使用以本身為基礎的網域屬性。  
  
## <a name="derived-hierarchy-example"></a>衍生階層範例  
 在下列範例中，Product 實體的分葉成員依 Subcategory 實體的分葉成員分組，後者則依 Category 實體的分葉成員分組。 此階層是可能的，因為 Product 實體有名稱為 Subcategory 的網域屬性，而 Subcategory 實體有名稱為 Category 的網域屬性。  
  
 階層結構顯示成員分組方式。 有最多成員的實體位於底部。  
  
 ![衍生自模型結構的階層](../../2014/master-data-services/media/mds-conc-derived-hierarchy-structure.gif "衍生自模型結構的階層")  
  
 在衍生階層中，您可以反白顯示 Product 與 Subcategory 之間的關聯性，然後反白顯示 Subcategory 與 Category 之間的關聯性。 當您在此階層中檢視成員時，樹狀結構中的每個層級都包含相同實體中的成員。  
  
 ![越野車衍生的階層範例](../../2014/master-data-services/media/mds-conc-derived-hierarchy-example.gif "越野車衍生的階層範例")  
  
 這種類型的階層可防止您將成員移到無效的層級。 例如，您可以將某個子類別目錄 Road Bikes 中的 Road-650 自行車移到另一個子類別目錄 Mountain Bikes。 您無法像 1 {Bikes} 一樣直接移動類別目錄底下的 Road-650。 每當您在階層樹狀結構中移動成員時，該成員的網域屬性值都會隨之變更，以反映這個移動作業。  
  
## <a name="notes"></a>注意  
 衍生階層樹狀結構中的所有成員都會依照代碼來排序。 您無法變更排序次序。  
  
 如果成員的網域屬性為空白，而且此屬性用於衍生階層，則該成員不會顯示在階層中。 建立商務規則來要求填入屬性。 如需詳細資訊，請參閱[要求屬性值 &#40;Master Data Services&#41;](require-attribute-values-master-data-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|建立新的衍生階層。|[建立衍生階層 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|隱藏或刪除現有衍生階層中的層級。|[隱藏或刪除衍生階層中的層級 &#40;Master Data Services&#41;](../../2014/master-data-services/hide-or-delete-levels-in-a-derived-hierarchy-master-data-services.md)|  
|變更現有衍生階層的名稱。|[變更衍生階層名稱 &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-derived-hierarchy-name-master-data-services.md)|  
|刪除現有衍生階層。|[刪除衍生階層 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
|||  
  
## <a name="related-content"></a>相關內容  
  
-   [網域屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [明確階層 &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [遞迴階層 &#40;Master Data Services&#41;](../../2014/master-data-services/recursive-hierarchies-master-data-services.md)  
  
-   [具有明確頂層的衍生階層 &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)  
  
-   [集合 &#40;Master Data Services&#41;](../../2014/master-data-services/collections-master-data-services.md)  
  
  
