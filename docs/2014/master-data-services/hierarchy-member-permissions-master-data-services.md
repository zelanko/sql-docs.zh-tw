---
title: 階層成員權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], permissions
- permissions [Master Data Services], members
ms.assetid: b3880eed-1bf6-4f65-ab23-b08c194cc858
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 371c7c605b5415654c01f3faa66fbd0801202785
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482958"
---
# <a name="hierarchy-member-permissions-master-data-services"></a>階層成員權限 (Master Data Services)
  階層成員權限為選擇性，而且只有當您希望使用者擁有特定成員的受限存取權時，才應該使用。 如果您未在 [階層成員] 索引標籤上指派權限，則使用者的權限完全是根據 [模型] 索引標籤上指派的權限。  
  
 階層成員權限會在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者介面 (UI) 中，[使用者及群組的權限] 功能區域的 [階層成員] 索引標籤上指派。這些權限會決定使用者可以在此 UI 的總管功能區域中存取哪些成員。  
  
 在 [階層成員] 索引標籤上，每一個階層會表示為一個樹狀結構。 當您將權限指派給樹狀結構中的節點時，所有子項都會繼承該權限，除非在較低層級明確指派權限。  
  
> [!NOTE]  
>  當您指派權限給階層中的節點時，相同層級或更高層級的其他節點中的所有成員都會以隱含方式遭到拒絕。  
  
 在總管中，成員權限會套用到顯示成員的每一個地方。 例如，具有成員**唯讀**權限為唯讀，而與其所屬任何實體、 階層和集合中。  
  
 階層成員權限會套用到您指派的模型版本以及該版本的任何將來複本。 它們不會套用到早於您所指派的版本。  
  
|權限|描述|  
|----------------|-----------------|  
|**唯讀**|顯示成員，但是使用者無法變更成員。 使用者也無法在任何明確階層或成員所屬的集合中移動成員。<br /><br /> 注意:如果您指派**唯讀**權限**根**，底下的成員**根**是唯讀的; 不過，在明確階層和集合中，使用者可以將成員移到**根**，可以將新成員加入**根**。|  
|**Update**|顯示成員，而且使用者可加以變更。 使用者也可以在任何明確階層或成員所屬的集合中移動成員。|  
|**拒絕**|不顯示成員。|  
  
 在 [階層成員] 索引標籤上，您指派的權限不會立即生效。 權限套用的頻率取決於 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中 [系統設定] 資料表內的 [成員安全性處理間隔設定]。 遵循[立即套用成員權限 &#40;Master Data Services&#41;](immediately-apply-member-permissions-master-data-services.md) 中的步驟，可以立即套用成員權限。  
  
> [!NOTE]  
>  您無法將階層成員權限指派給遞迴階層、具有明確頂層的衍生階層，以及具有隱藏層級的衍生階層。  
  
## <a name="possible-overlapping-permissions"></a>可能重疊的權限  
 當指派權限給成員時，您可能必須解析重疊的權限。  
  
### <a name="when-a-member-belongs-to-multiple-hierarchies"></a>當成員屬於多個階層  
 兩個或多個階層可以包含相同的成員。  
  
-   如果一個階層節點被指派**更新**指派權限，而另一個**唯讀**，則該節點中的成員**唯讀**。  
  
-   如果一個階層節點被指派**更新**或是**唯讀**權限，另一個節點被指派**拒絕**，則不會顯示該節點中的成員。  
  
## <a name="see-also"></a>另請參閱  
 [指派階層成員權限 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [如何決定權限 &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)   
 [成員 &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [階層 &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchies-master-data-services.md)   
 [立即套用成員權限 &#40;Master Data Services&#41;](immediately-apply-member-permissions-master-data-services.md)  
  
  
