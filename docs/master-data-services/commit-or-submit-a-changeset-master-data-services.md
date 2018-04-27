---
title: 認可或提交變更集 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d323bbac-c8d4-4d2f-a7d2-a597e8b53e2d
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 149519f8072dc783747edb26ce449e4ade290685
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="commit-or-submit-a-changeset-master-data-services"></a>認可或提交變更集 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  變更集是對主要資料所做的暫止變更集合。 如果實體變更不需要系統管理員核准，您就可以認可變更集。 如果實體變更需要系統管理員核准，您可以提交變更集進行核准。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。 如需詳細資訊，請參閱[功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)  
  
-   如果實體變更不需要系統管理員核准，您只有在擁有變更集且變更集的狀態為開啟時，才可以認可變更集。  
  
-   如果實體變更需要系統管理員核准，您只有在擁有變更集且變更集的狀態為開啟或已拒絕時，才可以提交變更集進行核准。  
  
## <a name="to-commit-a-local-changeset"></a>認可本機變更集  
 認可選項只適用於實體系統管理員尚未啟用需要核准之實體上的本機變更集。  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取模型和版本，然後按一下總管。  
  
2.  按一下 [實體]  功能表中的實體。  
  
3.  在右窗格中，選取 [變更集]，然後按兩下您要認可的變更集。  
  
4.  按一下 [認可]。  
  
## <a name="to-submit-a-changeset"></a>提交本機變更集  
 提交選項只適用於實體系統管理員已啟用需要核准之實體上的變更集。  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取模型和版本，然後按一下總管。  
  
2.  按一下 [實體]  功能表中的實體。  
  
3.  在右窗格中，選取 [變更集]，然後按兩下您要提交的變更集。  
  
4.  按一下 [提交]。  
  
## <a name="next-steps"></a>Next Steps  
 [核准或拒絕變更集 &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [建立變更集 &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [套用及更新變更集 &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [核准或拒絕變更集 &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
