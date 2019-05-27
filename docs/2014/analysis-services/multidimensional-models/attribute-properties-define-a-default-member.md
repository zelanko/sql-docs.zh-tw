---
title: 定義預設成員 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 959645223eacec6c000ddbfa23615b7949d10d5a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077423"
---
# <a name="define-a-default-member"></a>定義預設成員
  當查詢中並未包含屬性階層時，會使用屬性階層的預設成員來評估運算式。 只要查詢包含屬性階層，或是使用者階層包含做為屬性階層來源的屬性，就會忽略預設成員。 這是因為使用查詢中指定的成員。  
  
 屬性階層的預設成員是透過指定屬性成員做為屬性階層的 `DefaultMember` 屬性值而設定的。 您可以在維度設計師中的 [維度結構] 索引標籤上設定此屬性，也可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中 Cube 設計師的 [計算] 索引標籤上的 Cube 計算指令碼中設定此屬性。 您也可以在定義維度安全性時，在 [維度資料] 索引標籤上指定安全性角色的 `DefaultMember` 屬性 (覆寫在維度上設定的預設成員)。 若要避免名稱解析問題，請於下列情況，在 Cube 的 MDX 指令碼中定義預設成員：如果 Cube 多次參考資料庫維度、如果 Cube 中的維度名稱與資料庫中的維度名稱不同，或是如果您要在不同的 Cube 中有不同的預設成員。  
  
 當查詢中並未包含屬性時，會使用屬性的預設成員來評估運算式。 屬性的預設成員由該屬性的 `DefaultMember` 屬性指定。 只要查詢內包含來自維度的階層，對應到該階層內各層級之屬性的所有預設成員都會忽略。 如果查詢內並未包含維度的階層，預設成員會用於維度中的所有屬性。  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>未指定預設成員時，解析預設成員  
 如果屬性階層沒有指定預設成員，而且該屬性階層是可彙總的 (屬性 (Attribute) 上的 `IsAggregatable` 屬性 (Property) 設定為 `True`)，則 (全部) 成員都是預設成員。 如果未指定任何預設成員，且屬性階層是不可彙總的 (屬性 (attribute) 上的 `IsAggregatable` 屬性 (property) 設定為 `False`)，則會從屬性階層的最上層中選取預設成員。  
  
## <a name="specifying-the-default-member"></a>指定預設成員  
 在維度中的每個屬性[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]都有預設成員，您可以指定使用`DefaultMember`屬性的屬性。 如果查詢中不包含屬性，則此設定可用來評估運算式。 如果查詢在維度中指定階層，則會忽略階層中之屬性的預設成員。 如果查詢未在維度中，指定階層`DefaultMember`維度屬性的設定才會生效。  
  
 如果`DefaultMember`設定的屬性空白且其`IsAggregatable`屬性設定為`True`的預設成員是全部成員。 如果`IsAggregatable`屬性設定為`False`的預設成員是第一個可見層級的第一個成員。  
  
 `DefaultMember`設定屬性，會套用至屬性所參與的每一個階層。 您不能對維度中的不同階層使用不同設定。 比方說，如果 [1998] 成員是 [Year] 屬性的預設成員，此設定將套用至維度中的每一個階層。 `DefaultMember`設定在此情況下不能 [1998] 在一個階層又 [1997] 在不同的階層架構中。  
  
 如果您為沒有自然彙總之階層的特定層級定義預設成員，則必須定義階層中位於該層級上方之所有層級中的預設成員。 比方說，在階層中 All-國家/地區-氣候，除非您定義國家 （地區） 的預設成員不能定義 climate 的預設成員。 如果沒有這麼做，會產生查詢階段錯誤。  
  
 若階層中的層級自然彙總，您可以定義階層中任何屬性的預設成員，而不必管階層中的其他屬性。 比方說，如果您在階層中的國家/地區-省-城市，您可以定義縣 （市），例如 [City] 的預設成員。[Montreal] 不必定義 State 或國家/地區的預設成員。  
  
## <a name="see-also"></a>另請參閱  
 [設定屬性階層的 &#40;全部&#41; 層級](database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
