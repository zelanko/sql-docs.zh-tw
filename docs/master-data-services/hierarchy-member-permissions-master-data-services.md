---
title: 階層成員權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], permissions
- permissions [Master Data Services], members
ms.assetid: b3880eed-1bf6-4f65-ab23-b08c194cc858
caps.latest.revision: 11
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e14a87d5398f3d47274708e5c411b5259314d883
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="hierarchy-member-permissions-master-data-services"></a>階層成員權限 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  階層成員權限為選擇性，而且只有當您希望使用者擁有特定成員的受限存取權時，才應該使用。 如果您未在 [階層成員] 索引標籤上指派權限，則使用者的權限完全是根據 [模型] 索引標籤上指派的權限。  
  
 階層成員權限會在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者介面 (UI) 中，[使用者及群組的權限] 功能區域的 [階層成員] 索引標籤上指派。這些權限會決定使用者可以在此 UI 的總管功能區域中存取哪些成員。  
  
 在 [階層成員] 索引標籤上，每一個階層會表示為一個樹狀結構。 當您將權限指派給樹狀結構中的節點時，所有子項都會繼承該權限，除非在較低層級明確指派權限。  
  
> [!NOTE]  
>  當您指派權限給階層中的節點時，相同層級或更高層級的其他節點中的所有成員都會以隱含方式遭到拒絕。  
  
 在總管中，成員權限會套用到顯示成員的每一個地方。 例如，具有 [讀取] 權限的成員可以讀取該成員所屬的任何實體、階層和集合。  
  
 階層成員權限會套用到您指派的模型版本以及該版本的任何將來複本。 它們不會套用到早於您所指派的版本。  
  
|權限|描述|  
|----------------|-----------------|  
|**讀取**|顯示成員。<br /><br /> <br /><br /> 注意：如果您僅指派 [讀取] 權限給 [根]，[根] 底下的成員是唯讀的。但是在明確階層和集合中，使用者可以將成員移到 [根] 而且可以將新的成員加入到 [根]。|  
|**建立**|階層成員的權限不足以建立權限。|  
|**Update**|顯示成員，而且使用者可加以變更。 使用者也可以在任何明確階層或成員所屬的集合中移動成員。|  
|**刪除**|顯示成員，而且使用者可加以刪除。|  
|**拒絕**|不顯示成員。|  
  
 在 [階層成員] 索引標籤上，您指派的權限不會立即生效。 權限套用的頻率取決於 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中 [系統設定] 資料表內的 [成員安全性處理間隔設定]。 遵循[立即套用成員權限 &#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md) 中的步驟，可以立即套用成員權限。  
  
> [!NOTE]  
>  您無法將階層成員權限指派給遞迴階層、具有明確頂層的衍生階層，以及具有隱藏層級的衍生階層。  
  
## <a name="possible-overlapping-permissions"></a>可能重疊的權限  
 當指派權限給成員時，您可能必須解析重疊的權限。  
  
### <a name="when-a-member-belongs-to-multiple-hierarchies"></a>當成員屬於多個階層  
 兩個或多個階層可以包含相同的成員。  
  
-   如果一個階層節點被指派 [更新] 權限，另一個節點被指派 [讀取] 權限，則該節點中的成員為 [讀取] 狀態。  
  
-   如果一個階層節點被指派 [更新] 和 [建立] 權限，另一個節點被指派 [更新] 和 [刪除] 權限，則該節點中的成員為可以更新。  
  
-   如果一個階層節點被指派任何 [建立]/[讀取]/[更新]/[刪除] 權限的組合，另一個節點被指派 [拒絕] 權限，則存取節點中的成員將遭到拒絕。  
  
## <a name="external-resources"></a>外部資源  
 請參考 msdn.com 上的 [Security Improvements](http://go.microsoft.com/fwlink/p/?LinkId=615376)(安全性改進) 部落格文章。  
  
## <a name="see-also"></a>另請參閱  
 [指派階層成員權限 &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [如何決定權限 &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [成員 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [階層 &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md)   
 [立即套用成員權限 &#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md)  
  
  
