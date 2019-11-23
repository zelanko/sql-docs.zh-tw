---
title: 核准或拒絕變更集
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 45bd01f9-ae15-4fc5-a2ba-eee565a26ef8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 401983aa2e5094560f7bcc852c839986ffe4234d
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728769"
---
# <a name="approve-or-reject-a-changeset-master-data-services"></a>核准或拒絕變更集 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  變更集是對主要資料所做的暫止變更集合。 如果實體變更需要系統管理員核准，而且已提交變更集進行核准，您可以檢閱，然後再核准或拒絕變更集。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。 如需詳細資訊，請參閱[功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
-   您必須具有實體的系統管理員權限。  
  
-   實體變更必須要求系統管理員核准。  
  
-   如果變更集處於暫止狀態，您可以檢閱，然後再核准或拒絕變更集。  
  
-   使用者不可以核准自己的變更。 如果您是實體系統管理員，您必須指派次要系統管理員來核准您自己的變更集。  
  
## <a name="to-approve-or-reject-a-changeset"></a>核准或拒絕變更集  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取模型和版本，然後按一下 [總管]。  
  
2.  按一下 [實體] 功能表中的實體。  
  
3.  在右窗格中，選取 [變更集]，然後按兩下您要核准或拒絕的變更集。  
  
4.  按一下 [套用] 套用變更集，並檢閱暫止的變更。  
  
5.  按一下 [拒絕] 拒絕變更集，並將其送回給擁有者。  
  
6.  按一下 [核准] 核准變更集。 系統會自動認可變更集。  
  
## <a name="see-also"></a>另請參閱  
 [建立變更集 &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [套用及更新變更集 &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [認可或提交變更集 &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
  
