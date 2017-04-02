---
title: "鎖定版本 (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "版本 [Master Data Services], 鎖定"
  - "鎖定版本 [Master Data Services]"
ms.assetid: 7bb62a84-12d8-4b29-9b6e-6aa25410618e
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 鎖定版本 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中，鎖定模型版本，以防止模型成員及其屬性的變更。  
  
> [!NOTE]  
>  版本已鎖定時，進階使用者和模型管理員可以繼續加入、編輯及移除成員。 其他具有模型權限的使用者只能檢視成員。  
  
## 必要條件  
 若要執行此程序：  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   版本的狀態必須是 [開啟]。  
  
-   您必須具有存取 [版本管理] 功能區域的權限。 如需詳細資訊，請參閱[功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
### 若要鎖定版本  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[版本管理]**。  
  
2.  在 [管理版本] 頁面上，選取要鎖定之版本的資料列。  
  
3.  按一下 [鎖定]。  
  
4.  在確認對話方塊中按一下 **[確定]**。  
  
## 後續步驟  
  
-   [根據商務規則驗證版本 &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   [認可版本 &#40;Master Data Services&#41;](../master-data-services/commit-a-version-master-data-services.md)  
  
## 另請參閱  
 [版本 &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [解除鎖定版本 &#40;Master Data Services&#41;](../master-data-services/unlock-a-version-master-data-services.md)  
  
  