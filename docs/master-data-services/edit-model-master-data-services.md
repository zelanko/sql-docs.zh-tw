---
title: "編輯模型 (Master Data Services) | Microsoft Docs"
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
  - "模型 [Master Data Services], 變更名稱"
ms.assetid: 399eed32-7c61-4239-9c06-996a65219518
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# 編輯模型 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以變更模型的名稱和描述，並指定您要保留交易記錄的天數。  
  
 如需詳細資訊，請參閱[交易 &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)。  
  
## 必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### 變更模型  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 **[模型檢視]** 頁面上，從功能表列指向 **[管理]** ，然後按一下 **[模型]**。  
  
3.  從 [管理模型]  頁面的方格中，選取您要變更名稱或描述之模型的資料列。  
  
4.  按一下 **[編輯]**。  
  
5.  在 [名稱]  方塊中，輸入模型的更新名稱。  
  
6.  在 [描述]  欄位中，輸入模型的更新描述。  
  
7.  在 [Log Retention Days] (記錄保留天數)  欄位中，選取其中一個選項來保留記錄資料。 預設值為 [系統設定] ，表示會從 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中的系統設定繼承值。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)。  
  
     若要覆寫系統設定而不移除交易記錄資料，請選取 [否] 。 若只要保留今天的記錄資料並截斷過去幾天的所有記錄資料，請選取 [是]  ，然後將 [天數]  欄位設為 0。 若要保留指定天數的記錄資料，請選取 [是]  ，然後將 [天數]  欄位設為該天數。  
  
8.  按一下 **[儲存模型]**。  
  
 方格中的 [狀態]  資料行會顯示模型上的作業狀態。 當您按一下 [儲存模型] 按鈕時，![Updating](../master-data-services/media/mds-model-status-updating.png "Updating") 影像隨即顯示，表示正在更新模型。 如果建立或編輯模型時發生錯誤，會顯示 ![Error](../master-data-services/media/mds-model-status-error.png "Error") 影像。 否則，狀態為正常並顯示 ![OK](../master-data-services/media/mds-model-status-ok.png "OK") 影像。  
  
## 另請參閱  
 [建立模型 &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [刪除模型 &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [模型 &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
  