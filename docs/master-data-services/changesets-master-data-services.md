---
title: "變更集 (Master Data Services) | Microsoft Docs"
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
ms.assetid: f227c49a-ed46-4e0f-8992-83093456cf94
caps.latest.revision: 13
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 5cfdab0f4b48cbb0f4abaca5f1d8e9e07a71d07b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="changesets-master-data-services"></a>變更集 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 現可支援將任何暫止的實體變更儲存為變更集的功能。 這項功能有下列兩個使用案例：  
  
-   **實體管理員開啟「需要核准」時的變更**  
  
     如果實體管理員指定特定實體所做的變更需經核准後才能獲得認可，則實體的任何變更均需先儲存到新的或現有的變更集才能提交核准。  如需詳細資訊，請參閱[需要核准 &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md)。  
  
     您會進行下列工作流程：  
  
    1.  您建立變更集。 變更集處於 [開啟] 狀態。 請參閱 [建立變更集 &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  您套用變更集，並將某些變更新增至變更集。 請參閱 [套用及更新變更集 &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  您將變更集提交給實體管理員核准。 變更集處於 [暫止] 狀態。 請參閱 [認可或提交變更集 &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
    4.  實體管理員取得變更集正在等待核准的電子郵件通知。 如果實體管理員核准變更集，變更集就會處於 [已核准] 狀態。 請參閱 [核准或拒絕變更集 &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
    5.  核准的變更集將會自動獲得認可。 如果變更成功獲得認可，變更集就會處於已認可狀態。  
  
-   **本機使用者的變更**  
  
     如果您只想要儲存本機的變更，以供日後使用或擷取，您可以使用變更集來達成此目標。  
  
     您會進行下列工作流程：  
  
    1.  您建立變更集。 變更集處於 [開啟] 狀態。 請參閱 [建立變更集 &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  您套用變更集，並將某些變更新增至變更集。 請參閱 [套用及更新變更集 &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  待一切就緒，您即可認可變更集。 請參閱 [認可或提交變更集 &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [建立變更集 &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [套用及更新變更集 &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [認可或提交變更集 &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)   
 [核准或拒絕變更集 &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)   
 [管理變更集 &#40;Master Data Services&#41;](../master-data-services/manage-changesets-master-data-services.md)  
  
  

