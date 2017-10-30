---
title: "指派模型物件權限 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- models [Master Data Services], assigning object permissions
- permissions [Master Data Services], assigning model object permissions
ms.assetid: 4b80148d-2318-415c-9479-28c240e48bcd
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: fa5c8efcfbefcc52aed6c4ffb5bd1614c3fb607c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="assign-model-object-permissions-master-data-services"></a>指派模型物件權限 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您需要提供使用者或群組對於 **之** [總管] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]功能區域中資料的存取權時，或當您需要將使用者或群組設為管理員時，請指派模型物件的權限。  
  
> [!NOTE]  
>  當您指派某個模型的權限時，會明確拒絕所有其他模型的權限。 如果未指派模型物件權限，使用者或群組就無法存取 **[總管]**中的資料。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[使用者及群組的權限]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-assign-model-object-permissions"></a>若要指派模型物件權限  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  在 **[使用者]** 或 **[群組]** 頁面上，選取要編輯之使用者或群組的資料列。  
  
3.  按一下 **[編輯選取的使用者]**。  
  
4.  按一下 **[模型]** 索引標籤。  
  
5.  (選擇性) 從 **[模型]** 清單中選取模型。  
  
6.  按一下 **[編輯]**。  
  
7.  展開樹狀結構，然後按一下要指派權限的模型物件。  
  
8.  從功能表中，選取 [讀取]、[建立]、[更新] 和 [刪除] 的組合，或是 [拒絕]。  
  
9. 在最上層模型層級中，如果您需要讓使用者模型成為系統管理員，請選取 [管理]  。  
  
10. 按一下 **[儲存]**。  
  
## <a name="next-steps"></a>後續步驟  
  
-   (選擇性) [指派階層成員權限 &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [刪除模型物件權限 &#40;Master Data Services&#41;](../master-data-services/delete-model-object-permissions-master-data-services.md)   
 [模型物件權限 &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [建立模型管理員 &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md)  
  
  

