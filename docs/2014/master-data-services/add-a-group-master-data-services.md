---
title: 新增群組 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- groups [Master Data Services], adding
- adding groups [Master Data Services]
ms.assetid: c7a88381-3b2c-4af7-9cf7-3a930c1abdee
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: df04cd5bcb216a716312783aff3b78d03ea01ac1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480138"
---
# <a name="add-a-group-master-data-services"></a>加入群組 (Master Data Services)
  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 的 [群組]  清單中加入群組，開始指派 Web 應用程式權限的程序。 在群組中的使用者存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 之前，您必須提供群組一個或多個功能區域和模型物件的權限。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[使用者及群組的權限]** 功能區域的權限。  
  
### <a name="to-add-a-group"></a>若要加入群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]** 。  
  
2.  在 [使用者]  頁面上，按一下功能表列中的 [管理群組]  。  
  
3.  按一下 [加入群組]  。  
  
4.  輸入群組名稱，並在名稱前面加入 Active Directory 網域名稱或伺服器電腦名稱，如下：*domain\group_name* 或 *computer\group_name*。  
  
5.  (選擇性) 按一下 **[檢查名稱]** 。  
  
6.  按一下 [確定]  。  
  
    > [!NOTE]  
    >  在使用者第一次存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]時，使用者的名稱就會加入至 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者清單。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [指派功能區域權限 &#40;Master Data Services&#41;](assign-functional-area-permissions-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [安全性 &#40;Master Data Services&#41;](../../2014/master-data-services/security-master-data-services.md)  
  
  
