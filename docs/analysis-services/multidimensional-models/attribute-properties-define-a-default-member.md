---
title: "定義預設成員 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ca6ba7f117f4803e62efe9904b3028d5f9262f4f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="attribute-properties---define-a-default-member"></a>屬性內容-定義預設成員
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]之預設成員的屬性階層用於查詢中不包含屬性階層時，評估運算式。 只要查詢包含屬性階層，或是使用者階層包含做為屬性階層來源的屬性，就會忽略預設成員。 這是因為使用查詢中指定的成員。  
  
 屬性階層的預設成員是透過指定屬性成員作為屬性階層的 **DefaultMember** 屬性值而設定的。 您可以在維度設計師中的 [維度結構] 索引標籤上設定此屬性，也可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中 Cube 設計師的 [計算] 索引標籤上的 Cube 計算指令碼中設定此屬性。 您也可以在定義維度安全性時，在 [維度資料] 索引標籤上指定安全性角色的 **DefaultMember** 屬性 (覆寫在維度上設定的預設成員)。 若要避免名稱解析問題，請於下列情況，在 Cube 的 MDX 指令碼中定義預設成員：如果 Cube 多次參考資料庫維度、如果 Cube 中的維度名稱與資料庫中的維度名稱不同，或是如果您要在不同的 Cube 中有不同的預設成員。  
  
 當查詢中並未包含屬性時，會使用屬性的預設成員來評估運算式。 屬性的預設成員由該屬性的 **DefaultMember** 屬性指定。 只要查詢內包含來自維度的階層，對應到該階層內各層級之屬性的所有預設成員都會忽略。 如果查詢內並未包含維度的階層，預設成員會用於維度中的所有屬性。  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>未指定預設成員時，解析預設成員  
 如果屬性階層沒有指定預設成員，而且該屬性階層為可彙總的 (屬性 (attribute) 上的 **IsAggregatable** 屬性 (property) 設定為 **True**)，則 (全部) 成員都是預設成員。 如果未指定任何預設成員，且屬性階層為不可彙總的 (屬性 (attribute) 上的 **IsAggregatable** 屬性 (property) 設定為 **False**)，則會從屬性階層的最上層中選取預設成員。  
  
## <a name="specifying-the-default-member"></a>指定預設成員  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中維度的每一個屬性 (attribute) 都有預設成員，您可以針對屬性 (attribute) 使用 **DefaultMember** 屬性 (property) 來指定此成員。 如果查詢中不包含屬性，則此設定可用來評估運算式。 如果查詢在維度中指定階層，則會忽略階層中之屬性的預設成員。 如果查詢未在維度中指定階層，則維度屬性的 **DefaultMember** 設定會生效。  
  
 如果屬性的 **DefaultMember** 設定空白，且其 **IsAggregatable** 屬性是設為 **True**，則預設成員是全部成員。 如果 **IsAggregatable** 屬性設為 **False**，預設成員是第一個可見層級的第一個成員。  
  
 屬性的 **DefaultMember** 設定，會套用至屬性所參與的每一個階層。 您不能對維度中的不同階層使用不同設定。 比方說，如果 [1998] 成員是 [Year] 屬性的預設成員，此設定將套用至維度中的每一個階層。 此案例中的 **DefaultMember** 設定不可以在一個階層是 [1998]，在另一個階層又變成 [1997]。  
  
 如果您為沒有自然彙總之階層的特定層級定義預設成員，則必須定義階層中位於該層級上方之所有層級中的預設成員。 例如，在 All-Countries–Climate 階層中，除非您有定義 Countries 的預設成員，否則您不能定義 Climate 的預設成員。 如果沒有這麼做，會產生查詢階段錯誤。  
  
 若階層中的層級自然彙總，您可以定義階層中任何屬性的預設成員，而不必管階層中的其他屬性。 例如，在 Country–Province–City 階層中，您可以定義 City 的預設成員，例如 [City].[Montreal]，而不必定義 State 或 Country 的預設成員。  
  
## <a name="see-also"></a>請參閱  
 [設定屬性階層的 &#40;全部&#41; 層級](../../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
