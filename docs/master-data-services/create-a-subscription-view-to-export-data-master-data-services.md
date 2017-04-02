---
title: "建立訂閱檢視以匯出資料 (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "訂閱檢視 [Master Data Services], 建立"
  - "建立訂閱檢視 [Master Data Services]"
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# 建立訂閱檢視以匯出資料 (Master Data Services)
  建立訂閱檢視，以將 Master Data Services 資料匯出至訂閱系統。 您要建立的檢視中的資料 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。  
  
## 必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[整合管理]** 功能區域的權限。 如需詳細資訊，請參閱 [功能區域權限 & #40。Master Data Services & #41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員及 #40。Master Data Services & #41;](../master-data-services/administrators-master-data-services.md)。  
  
### 建立和編輯訂閱檢視  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，按一下 **[整合管理]**。  
  
2.  按一下功能表列上的 **[建立檢視表]**。  
  
3.  在 **訂閱檢視** 頁面上，按一下 **新增** 建立檢視，或按一下 **編輯** 來編輯檢視。 隨即會在右側顯示面板。  
  
4.  在 **建立訂閱檢視** 窗格，請在 **名稱** 方塊中，輸入檢視的名稱。  
  
     在 **編輯訂閱檢視** 窗格，請在 **名稱** 方塊中，輸入檢視的更新的名稱。  
  
5.  從 **模型** 清單中，選取模型。  
  
6.  選取 **包含虛刪除成員**, 、 要包含在檢視中的虛刪除的成員。  
  
7.  選取 [ **版本** 或 **版本旗標** 中 **版本選項**, ，然後選取 [從對應的清單。  
  
    > [!TIP]  
    >  根據版本旗標建立訂閱檢視。 當您鎖定版本時，您可以重新指派旗標給開啟的版本，而不用更新訂閱檢視。  
  
8.  選取 [ **實體** 或 **衍生階層** 中 **資料來源** 選項，然後從對應的清單。  
  
9. 從 **格式** 清單中，選取 [訂閱檢視格式。  
  
10. 如果您選擇 **明確層級** 或 **衍生層級** 從 **格式** 清單中，輸入要包含在檢視中的階層層級數目。  
  
11. 按一下 **[儲存]**。  
  
## 檢視資訊  
 對於每個建立的檢視，會將含十個資料行的資料列加入方格中。 下表描述該資料行。  
  
|資料行|描述|  
|------------|-----------------|  
|狀態|檢視狀態。<br /><br /> 當您按一下 **儲存**, 、 ![Icon for updating status](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status") 影像會顯示，指出正在更新檢視。<br /><br /> 如果發生錯誤時建立或編輯檢視 ![Icon for error status](../master-data-services/media/mds-statusicon-error.png "Icon for error status") 影像顯示。<br /><br /> 否則，狀態為 [確定] 和 ![Icon for OK status](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status") 影像顯示。|  
|名稱|訂閱檢視名稱。|  
|模型|模型名稱。|  
|版本|版本名稱。|  
|版本旗標|版本旗標名稱。|  
|衍生階層|衍生階層名稱。|  
|實體|實體名稱。|  
|格式|指定檢視中資料的類型。|  
|層級|指定檢視中的層級數目 (僅用於明確層級或衍生層級檢視格式)。|  
|包含刪除成員|表示檢視中是否包含虛刪除成員。|  
  
 當您按一下檢視時，會顯示下列資訊。  
  
-   **建立者**︰ 建立檢視的使用者名稱。  
  
-   **在**︰ 建立檢視時的時間與日期。  
  
-   **更新由**︰ 最後一個使用者名稱已更新檢視。  
  
-   **在**︰ 檢視上次更新的時間與日期。  
  
## 另請參閱  
 [概觀︰ 匯出資料和 #40。Master Data Services & #41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [刪除訂閱檢視 & #40。Master Data Services & #41;](../master-data-services/delete-a-subscription-view-master-data-services.md)   
 [建立版本旗標和 #40。Master Data Services & #41;](../master-data-services/create-a-version-flag-master-data-services.md)  
  
  