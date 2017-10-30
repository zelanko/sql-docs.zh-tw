---
title: "編輯和刪除實體同步關係 (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a5e37f3-352e-45a6-b4a0-6f98f83b4bd8
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 68b60fa3d77ae5786419e83dbbdfc9967130cb59
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="edit-and-delete-an-entity-sync-relationship-master-data-services"></a>編輯和刪除實體同步關係 (Master Data Services)
  實體同步是實體版本間單向且可重複的同步處理。 它提供不同模型間共用實體資料的方法。 您可以編輯和刪除您已建立的同步關係。  
  
## <a name="prerequisites"></a>必要條件  
 編輯實體同步關係的必要條件。  
  
-   您必須擁有存取系統管理功能區域的權限。 如需詳細資訊，請參閱[功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
-   您必須是目標模型的模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   您必須至少具備來源實體及其屬性與成員的讀取存取權。  
  
 刪除實體同步關係的必要條件。  
  
-   您必須擁有存取系統管理功能區域的權限。 如需詳細資訊，請參閱[功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
-   您必須是目標模型的模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
 編輯實體同步關係時，請考量以下事項。  
  
-   來源及目標實體必須在不同模型中。  
  
-   必須不會認可目標實體版本狀態。  
  
-   一旦建立同步關係，目標會立即與來源同步。  
  
-   目標實體版本不能是另一個同步關係的來源實體版本。  
  
 執行實體同步關係時，請考量以下事項。  
  
-   只會複製分葉成員。  
  
-   不會複製網域屬性。  
  
-   不會複製虛刪除的成員。  
  
-   同步處理不會產生目標實體交易/歷程。  
  
 **編輯實體同步關係**  
  
1.  在主資料管理員中，按一下 [系統管理] 。  
  
2.  在 [模型檢視]  頁面上，從功能表列指向 [管理]  ，然後按一下 [實體同步處理] 。  
  
3.  在 [實體同步維護]  業面上，選取方格中的同步關係。  
  
4.  按一下 **[編輯]**。 隨即會在右側顯示面板。  
  
5.  變更 [頻率]。 選取 [隨需同步處理] ，或選取 [自動同步處理]  並設定頻率。  
  
6.  按一下 **[儲存]**。  
  
 **刪除實體同步關係**  
  
1.  在主資料管理員中，按一下 [系統管理] 。  
  
2.  在 [模型檢視]  頁面上，從功能表列指向 [管理]  ，然後按一下 [實體同步處理] 。  
  
3.  在 [實體同步維護]  業面上，選取方格中的同步關係。  
  
4.  按一下 **[刪除]**。  
  
5.  在確認對話方塊中，按一下 [確定]。  
  
## <a name="see-also"></a>另請參閱  
 [建立及執行實體同步關係 &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [實體同步關聯性 &#40;Master Data Services&#41;](../master-data-services/entity-sync-relationship-master-data-services.md)  
  
  

