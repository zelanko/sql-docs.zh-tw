---
title: "刪除成員或集合 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collections [Master Data Services], deleting
- leaf members [Master Data Services], deleting
- deleting members [Master Data Services]
- members [Master Data Services], deleting
- consolidated members [Master Data Services], deleting
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
caps.latest.revision: "10"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39185736867be88bb1d8e7f6e397a775bc22159b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="delete-a-member-or-collection-master-data-services"></a>刪除成員或集合 (Master Data Services)
  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，刪除您不再需要的成員或集合。 如果您要大量刪除成員，請改用暫存表格。 如需詳細資訊，請參閱[從資料表匯入資料 &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md)。  
  
> [!NOTE]  
>  如果某個成員是當做另一個成員的網域屬性值使用，您就無法刪除該成員。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
-   針對成員，您至少必須擁有分葉模型物件的 **刪除** 權限，才能從中刪除成員。  
  
-   針對集合，您必須至少擁有分頁集合物件 **更新** 權限，才能將其刪除。  
  
### <a name="to-delete-a-member-or-collection"></a>若要刪除成員或集合  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取 **[模型]** 清單中的模型。  
  
2.  從 **[版本]** 清單中選取版本。  
  
3.  按一下 **[總管]**。  
  
4.  若要刪除：  
  
    -   分葉成員，請從功能表列指向 [實體]，然後按一下包含該成員的實體名稱。  
  
    -   合併成員，請從功能表列指向 [階層]，然後按一下包含該成員的階層名稱。 然後按一下階層中包含此成員的節點。  
  
    -   集合，請從功能表列指向 [集合]，然後按一下包含該集合的實體名稱。  
  
5.  在方格中，按一下要刪除之成員或集合的資料列。  
  
6.  按一下 [刪除成員]、[刪除] 或 [刪除集合]。  
  
7.  實體系統管理員也會在實體版本中看到清除 (永久刪除) 所有虛刪除成員的功能表選項。  
  
8.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [重新啟用成員或集合 &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [成員 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [集合 &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
  
