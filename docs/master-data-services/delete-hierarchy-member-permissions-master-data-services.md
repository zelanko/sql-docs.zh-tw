---
title: 刪除階層成員權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting member permissions [Master Data Services]
- members [Master Data Services], deleting permissions
- permissions [Master Data Services], deleting member permissions
ms.assetid: 7f22d5e2-70c1-422c-99c2-e995a47d812a
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 8c3708ac1899def00833b31f7774f627043f81a6
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35328032"
---
# <a name="delete-hierarchy-member-permissions-master-data-services"></a>刪除階層成員權限 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，刪除模型物件權限，移除所做的任何指派。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[使用者及群組的權限]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
### <a name="to-delete-hierarchy-member-permissions"></a>若要刪除階層成員權限  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  在 **[使用者]** 或 **[群組]** 頁面上，選取要編輯之使用者或群組的資料列。  
  
3.  按一下 **[編輯選取的使用者]**。  
  
4.  按一下 [階層成員] 索引標籤。  
  
5.  從 [模型] 清單中選取模型。  
  
6.  從 **[版本]** 清單中選取版本。  
  
7.  按一下 **[編輯]**。  
  
8.  在 [階層成員權限] 面板中，尋找擁有權限的樹狀節點。  
  
9. 按一下樹狀節點，然後在操作功能表中按一下 [節點]。  
  
    > [!NOTE]  
    >  如果權限繼承自群組，則無法從使用者移除權限。 您必須改為從群組移除權限。  
  
10. 按一下 **[儲存]**。  
  
## <a name="see-also"></a>另請參閱  
 [階層成員權限 &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [指派階層成員權限 &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
  
