---
title: "分葉權限 (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "屬性群組 [Master Data Services], 權限"
  - "成員 [Master Data Services] 分葉成員權限"
  - "權限 [Master Data Services], 分葉成員"
  - "分葉成員 [Master Data Services], 屬性權限"
  - "屬性 [Master Data Services], 分葉成員屬性權限"
ms.assetid: bde16e8c-bcd4-4041-8130-55c5450e5f72
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# 分葉權限 (Master Data Services)
  分葉權限適用於某個實體所有分葉成員的屬性值。  
  
 如果是沒有啟用明確階層的實體，將權限指派給 [分葉] 與指派給實體相同。  
  
 **注意：**  
  
-   分葉權限只適用於使用者介面的總管功能區域。  
  
-   系統不會強制使用指派給 **Name** 和 **Code** 屬性的權限。  
  
|權限|說明|  
|----------------|-----------------|  
|**讀取**|使用者可以讀取分葉成員、屬性。|  
|**建立**|使用者可以建立分葉成員，並在建立期間指派屬性值。|  
|**Update**|使用者可以更新分葉成員和屬性。|  
|**Delete**|使用者可以刪除分葉成員。|  
|**拒絕**|拒絕所有對分葉成員的存取。|  
  
 讀取、建立、更新和刪除權限可以合併。 指派建立、更新和刪除時，將會自動指派讀取權限。  
  
## 屬性權限  
 屬性權限適用於特定實體的屬性值。 只有屬性權限的使用者無法加入或移除成員。  
  
|權限|說明|  
|----------------|-----------------|  
|**讀取**|使用者可以讀取屬性。|  
|**建立**|使用者可以在建立成員時指派值。|  
|**Update**|使用者可以更新屬性。|  
|**Delete**|沒有影響。|  
|**拒絕**|不顯示屬性。<br /><br /> 注意：您無法明確拒絕存取 Name 和 Code 屬性。|  
  
### 範例  
 如果是 Product 實體，請將 [更新] 權限指派給 Subcategory 屬性。 拒絕其他所有屬性的權限。  
  
|名稱|程式碼|Subcategory (更新)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|{5} Mountain Bikes|  
|Mountain-100|BK-M201|{5} Mountain Bikes|  
  
 在總管中，您可以更新 Subcategory 資料行中的任何屬性值。 如果您沒有屬性的權限，就不會顯示該屬性。  
  
> [!NOTE]  
>  在這個範例中，Subcategory 是根據 SubcategoryList 實體的網域屬性。 您可以為 Mountain-100 選取不同的子類別目錄，但是您無法從 SubcategoryList 實體中加入成員或刪除成員。  
  
## 另請參閱  
 [指派模型物件權限 &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [合併的權限 &#40;Master Data Services&#41;](../Topic/Consolidated%20Permissions%20\(Master%20Data%20Services\).md)   
 [模型物件權限 &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [成員 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  