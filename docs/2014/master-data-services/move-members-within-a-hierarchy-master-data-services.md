---
title: 在階層中移動成員（Master Data Services） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 58b39d2dc660fd51d1ba21308ff056874a239731
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054084"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>在階層中移動成員 (Master Data Services)
  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中，移動階層中的成員來變更成員的位置或父系指派。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
-   針對明確階層，您至少必須擁有實體的 [**更新**] 許可權。  
  
-   針對衍生階層，您必須至少有模型的**更新**，以及階層中所使用的任何網域屬性。  
  
### <a name="to-move-members-within-a-hierarchy"></a>若要移動階層中的成員  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取 **[模型]** 清單中的模型。  
  
2.  從 **[版本]** 清單中選取版本。  
  
3.  按一下 **[總管]**。  
  
4.  從功能表列指向 [階層] **，然後按一下**[ *hierarchy_name*]。  
  
5.  在階層顯示于樹狀結構**中的階層窗格中**，按一下您想要移動之每個成員的核取方塊。  
  
6.  在 [**階層] 窗格的頂端**，按一下 [**剪**下]。  
  
7.  **在 [階層] 窗格**中，按一下您想要將成員移至其中之成員的核取方塊。  
  
8.  按一下 [**貼**上]。  
  
    > [!NOTE]  
    >  在衍生階層中，您只能將成員移到相同的層級。 此外，您無法變更成員的排序次序。  
  
## <a name="see-also"></a>另請參閱  
 [使用暫存進程 &#40;Master Data Services 來移動明確階層成員&#41;](add-update-and-delete-data-master-data-services.md)   
 [衍生階層 &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [明確階層 &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
