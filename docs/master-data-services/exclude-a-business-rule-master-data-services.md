---
title: "排除商務規則 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f82830abaf67206b022fc7231c321507a7f9f22a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="exclude-a-business-rule-master-data-services"></a>排除商務規則 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您不想要永久刪除商務規則，但是也不想使用它來驗證資料時，可排除此商務規則。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-exclude-a-business-rule"></a>若要排除商務規則  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [商務規則]  頁面上，從 [模型]  下拉式清單選取模型。  
  
4.  從 [實體] 下拉式清單中，選取實體。  
  
5.  從 [成員類型] 下拉式清單中，選取成員的類型。  
  
6.  在方格中，選取您想要排除之商務規則的資料列，然後按一下 [編輯]。  
  
7.  選取 [已排除] 核取方塊。  
  
8.  按一下 **[儲存]**。  
  
9. 按一下 [全部發行]。  
  
10. 在確認對話方塊中按一下 **[確定]**。 [商務規則狀態] 資料行中的值是 [已排除] 且 [已排除] 資料行是 [是]。  
  
## <a name="see-also"></a>另請參閱  
 [刪除商務規則 &#40;Master Data Services&#41;](../master-data-services/delete-a-business-rule-master-data-services.md)   
 [建立及發行商務規則 &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
