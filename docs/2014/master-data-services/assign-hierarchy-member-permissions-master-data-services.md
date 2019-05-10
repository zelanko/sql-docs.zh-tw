---
title: 指派階層成員權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], assigning member permissions
- members [Master Data Services], assigning permissions
ms.assetid: e1b8b46a-7cd1-4a7d-9345-dd7df081e145
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a12a46c1a250ce3d93c9ec2091dc5048ceebd61e
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483728"
---
# <a name="assign-hierarchy-member-permissions-master-data-services"></a>指派階層成員權限 (Master Data Services)
  指派階層成員的權限，提供使用者或群組存取權，以便在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 的總管功能區域中檢視資料。  
  
 階層成員權限為選擇性。 它們為必要的模型物件權限提供更細微的控制。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[使用者及群組的權限]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
### <a name="to-assign-hierarchy-member-permissions"></a>若要指派階層成員權限  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  在 **[使用者]** 或 **[群組]** 頁面上，選取要編輯之使用者或群組的資料列。  
  
3.  按一下 **[編輯選取的使用者]**。  
  
4.  按一下 [階層成員] 索引標籤。  
  
5.  從 [模型] 清單中選取模型。  
  
6.  從 **[版本]** 清單中選取版本。  
  
7.  從 [階層] 清單中選取階層。  
  
8.  按一下 **[編輯]**。  
  
9. 展開樹狀結構，然後按一下要指派權限的階層節點。  
  
10. 從功能表中，選取**唯讀**，**更新**，或**拒絕**。  
  
11. 按一下 [儲存] 。  
  
    > [!NOTE]  
    >  階層成員權限不會立即生效。 如需詳細資訊，請參閱[立即套用成員權限 &#40;Master Data Services&#41;](../../2014/master-data-services/immediately-apply-member-permissions-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [刪除階層成員權限 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-hierarchy-member-permissions-master-data-services.md)   
 [指派模型物件權限 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [階層成員權限 &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
