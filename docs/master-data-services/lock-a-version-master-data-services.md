---
title: "鎖定版本 (Master Data Services) | Microsoft Docs"
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
- versions [Master Data Services], locking
- locking versions [Master Data Services]
ms.assetid: 7bb62a84-12d8-4b29-9b6e-6aa25410618e
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d8d93779665f832f59f8748241ac9af67837c71d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="lock-a-version-master-data-services"></a>鎖定版本 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，鎖定模型版本，以防止模型成員及其屬性的變更。  
  
> [!NOTE]  
>  版本已鎖定時，進階使用者和模型管理員可以繼續加入、編輯及移除成員。 其他具有模型權限的使用者只能檢視成員。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   版本的狀態必須是 [開啟]。  
  
-   您必須擁有存取 [版本管理] 功能區域的權限。 如需詳細資訊，請參閱[功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
### <a name="to-lock-a-version"></a>若要鎖定版本  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[版本管理]**。  
  
2.  在 [管理版本] 頁面上，選取要鎖定之版本的資料列。  
  
3.  按一下 [鎖定]。  
  
4.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="next-steps"></a>Next Steps  
  
-   [根據商務規則驗證版本 &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   [認可版本 &#40;Master Data Services&#41;](../master-data-services/commit-a-version-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [版本 &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [解除鎖定版本 &#40;Master Data Services&#41;](../master-data-services/unlock-a-version-master-data-services.md)  
  
  
