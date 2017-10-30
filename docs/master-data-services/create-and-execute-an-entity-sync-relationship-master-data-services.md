---
title: "建立及執行實體同步關係 (Master Data Services) | Microsoft Docs"
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
ms.assetid: 0ddceab4-d2b3-4bc1-bd9c-6b852200b414
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 14bc03c2c8c462895102d6c34c62cf23724c706f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="create-and-execute-an-entity-sync-relationship-master-data-services"></a>建立及執行實體同步關係 (Master Data Services)
  實體同步是實體版本間單向且可重複的同步處理。 它提供不同模型間共用實體資料的方法。  
  
## <a name="prerequisites"></a>必要條件  
 建立實體同步關係的必要條件：  
  
-   您必須擁有存取系統管理功能區域的權限。 如需詳細資訊，請參閱[功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
-   您必須是目標模型的模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   您必須至少具備來源實體及其屬性與成員的讀取存取權。  
  
 執行實體同步關係的必要條件：  
  
-   您必須擁有存取系統管理功能區域的權限。 如需詳細資訊，請參閱[功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
-   您必須是目標模型的模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
 建立實體同步關係時，請考量以下事項。  
  
-   來源及目標實體必須在不同模型中。  
  
-   必須不會認可目標實體版本狀態。  
  
-   一旦建立同步關係，目標會立即與來源同步。  
  
-   目標實體版本不能是另一個同步關係的來源實體版本。  
  
 執行實體同步關係時，請考量以下事項。  
  
-   只會複製分葉成員  
  
-   不會複製網域屬性。  
  
-   不會複製虛刪除的成員。  
  
-   同步處理不會產生目標實體交易/歷程。  
  
 **建立實體同步關係**  
  
1.  在主資料管理員中，按一下 [系統管理] 。  
  
2.  在 [模型檢視]  頁面上，從功能表列指向 [管理]  ，然後按一下 [實體同步處理] 。  
  
3.  按一下 [實體同步維護]  頁面上的 [加入] 。 隨即會在右側顯示面板。  
  
4.  從來源 [模型]  清單中選取模型。  
  
5.  從來源 [版本]  清單中選取版本。  
  
6.  從來源 [實體]  清單中選取實體。  
  
7.  從目標 [模型]  清單中選取模型。  
  
8.  從目標 [版本]  清單中選取版本。  
  
9. 如果您想要同步現有實體，請選擇 [現有實體]  然後從 [實體] 清單中選取實體，或如果您想要同步新實體，請選擇 [新實體]  ，然後輸入目標實體的名稱  
  
10. 選取 [隨需同步處理] ，或選取 [自動同步處理]  並設定頻率。  
  
11. 按一下 **[儲存]**。  
  
 **執行實體同步關係**  
  
1.  在主資料管理員中，按一下 [系統管理] 。  
  
2.  在 [模型檢視]  頁面上，從功能表列指向 [管理]  ，然後按一下 [實體同步處理] 。  
  
3.  在 [實體同步維護]  業面上，選取方格中的同步關係。  
  
4.  按一下 **[執行]**。  
  
## <a name="sync-relationship-information"></a>同步關係資訊  
 對於每個建立的同步關係，會新增含有十個資料行的資料列到方格。 下表描述該資料行。  
  
|資料行|說明|  
|------------|-----------------|  
|狀態|同步關係狀態。<br /><br /> 當您按一下 [儲存] 或執行同步關係時，會顯示![正在更新狀態圖示](../master-data-services/media/mds-statusicon-updating.png "正在更新狀態圖示")影像，表示正在更新同步關係。<br /><br /> 如果建立、編輯或執行同步關係時發生錯誤，則會顯示![錯誤狀態圖示](../master-data-services/media/mds-statusicon-error.png "錯誤狀態圖示")影像。<br /><br /> 否則，狀態為正常，並顯示![正常狀態圖示](../master-data-services/media/mds-statusicon-ok.png "正常狀態圖示")影像。|  
|來源模型|來源模型名稱。|  
|來源版本|來源版本名稱。|  
|來源實體|來源實體名稱。|  
|目標模型|目標模型名稱。|  
|目標版本|目標版本名稱。|  
|目標實體|目標實體名稱。|  
|頻率|指定同步關係的頻率。|  
|上次嘗試時間|顯示上次嘗試同步的發生時間。|  
|上次成功時間|顯示上次成功嘗試同步的發生時間。|  
  
 當您按一下索引時，則會顯示下列資訊。  
  
-   **上次嘗試的錯誤**︰顯示上次嘗試同步的錯誤資訊。  
  
-   **建立者**：建立同步的使用者名稱。  
  
-   **於**：建立同步的日期與時間。  
  
-   **更新者**：上次更新同步的使用者名稱。  
  
-   **於**：上次更新同步的日期與時間。  
  
## <a name="next-steps"></a>後續步驟  
 [編輯和刪除實體同步關係 &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  

