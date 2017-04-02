---
title: "建立分葉成員 (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "分葉成員 [Master Data Services], 建立"
  - "建立分葉成員 [Master Data Services]"
  - "成員 [Master Data Services], 建立分葉成員"
ms.assetid: 0499d3b3-d508-4d43-a740-19cf53ade9f1
caps.latest.revision: 14
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 14
---
# 建立分葉成員 (Master Data Services)
  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中，您可建立分葉成員以將主要資料新增至系統。 如果您想要加入大量資料，請改用暫存表格。 如需詳細資訊，請參閱[從資料表匯入資料 &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md)。  
  
 您也可以使用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 匯入資料。  
  
## 必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
-   您至少必須擁有要新增成員之實體分葉模型物件的**建立**或**更新**權限。 建立權限可讓您建立成員和只編輯 Code 屬性。 更新權限可讓您更新其他屬性。  
  
     如需詳細資訊，請參閱[安全性 &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)。  
  
### 若要建立分葉成員  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取 [模型]  清單中的模型。  
  
2.  如果您是使用者，請從 [版本] 清單中選取開啟的版本。 如果您是系統管理員，請從 [版本] 清單中選取狀態為開啟或鎖定的版本。  
  
3.  按一下 **[總管]**。  
  
4.  從功能表列指向 [實體]，然後按一下要新增成員的實體名稱。  
  
5.  按一下 [加入成員]。  
  
6.  填妥 [詳細資料] 窗格中的欄位。  
  
     如為網域型屬性，且屬性已套用篩選，則篩選父屬性就會限制屬性值清單。  
  
     如需篩選父屬性和網域屬性的詳細資訊，請參閱[建立網域屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)。  
  
7.  選擇性。 在 **[註解]** 方塊中，輸入有關加入此成員之原因的註解。 可存取成員的所有使用者都可以檢視註解。  
  
8.  按一下 **[確定]**。  
  
## 另請參閱  
 [建立合併成員 &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)   
 [成員 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
  