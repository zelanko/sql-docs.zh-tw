---
title: 合併衝突 (Master Data Services) | Microsoft Docs
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
ms.assetid: 797219ad-5109-4666-94d3-dd1d59440a33
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16c2873058f4dc720572ba92142456fa78b1bed1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="merge-conflicts-master-data-services"></a>合併衝突 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，如果您嘗試發佈已由另一位使用者變更的資料，則該發佈將會失敗並會出現衝突錯誤。 若要解決此錯誤，可以執行合併衝突，然後重新發佈所做的變更。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
-   針對要更新的實體分葉模型物件，您必須至少擁有最小的更新權限。  
  
### <a name="to-merge-conflicts"></a>合併衝突  
  
1.  在 [總管] 頁面上，更新成員屬性。  
  
2.  如果另一位使用者已變更同一個成員屬性，[合併衝突] 對話方塊隨即會出現。  
  
3.  在 [合併衝突] 對話方塊中，您可以︰  
  
    -   選擇 [最新]，並按一下 [套用] 復原暫止的變更，然後重新載入來自伺服器的最新版本。  
  
    -   選擇 [原始]，並按一下 [套用] 套用工作表中的原始版本。  
  
    -   選擇 [您的]，並按一下 [套用] 保留現有的本機變更。  
  
4.  按一下 [套用] 之後，您可以進行其他變更，並重新發佈。 或是按一下 [取消] 取消更新，並重新載入來自伺服器的最新版本。  
  
## <a name="see-also"></a>另請參閱  
 [成員 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
  
