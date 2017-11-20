---
title: "隱藏或刪除衍生階層中的層級 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- derived hierarchies, hiding levels
- derived hierarchies, deleting levels
ms.assetid: e00582b9-9415-4b66-b4a7-9f590d83875f
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: a4d70ee875bdd39ee4ff79c7ce19cad426c677b6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="hide-or-delete-levels-in-a-derived-hierarchy-master-data-services"></a>隱藏或刪除衍生階層中的層級 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您要求群組的層級但是不需要顯示該層級時，請在衍生階層中隱藏該層級。 當您不想要使用層級來群組時，請將它刪除。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-hide-or-delete-levels-in-a-derived-hierarchy"></a>若要隱藏或刪除衍生階層中的層級  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列指向 [管理]，然後按一下 [衍生階層]。  
  
3.  在 [衍生階層維護] 頁面上，選取 [模型] 清單中的模型。  
  
4.  選取要編輯之衍生階層的資料列。  
  
5.  按一下 **[編輯]**。  
  
6.  在 [目前層級] 窗格中：  
  
    -   若要隱藏層級，請按一下頂端或底端以外的層級。 從 [可見] 清單中，選取 [否]。 然後按一下 [儲存選取的階層項目]。  
  
    -   若要刪除最上層，請按一下 [刪除選取的階層項目]。 在確認對話方塊中按一下 **[確定]**。 您可以只刪除最上層。  
  
## <a name="see-also"></a>另請參閱  
    
 [衍生階層 &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  

