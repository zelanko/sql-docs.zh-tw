---
title: "建立實體管理員 (Master Data Services) | Microsoft Docs"
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
ms.assetid: 717be1e8-488e-4219-8d1e-ca9084b864cd
caps.latest.revision: 5
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: b322107b8fa557d82b03a6b08b96c872be5205af
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="create-an-entity-administrator-master-data-services"></a>建立實體管理員 (Master Data Services)
  當您希望群組或使用者擁有一個或多個實體中全部物件的所有權限，或擁有核准暫止變更集的權限時，請在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中建立實體管理員。  
  
> [!TIP]  
>  若要簡化管理，請建立 Windows 或本機群組，然後將此群組設定為實體管理員。 然後不需存取 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]，您就可以在群組中加入及移除使用者。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 [使用者及群組的權限] 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
## <a name="to-create-an-entity-administrator"></a>建立實體管理員  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  選取您要編輯之使用者或群組的資料列，然後按一下 [編輯選取的使用者]。  
  
3.  按一下 [模型] 索引標籤，選擇性地從 [模型] 清單中選取模型，然後按一下 [編輯]。  
  
4.  按一下您要授與權限的實體，然後按一下功能表上的 [管理]。  
  
5.  針對您希望群組或使用者成為其管理員的每個實體，完成步驟 4。  
  
6.  按一下 **[儲存]**。  
  
## <a name="see-also"></a>另請參閱  
 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [指派模型物件權限 &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [指派階層成員權限 &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [模型物件權限 &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [階層成員權限 &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  

