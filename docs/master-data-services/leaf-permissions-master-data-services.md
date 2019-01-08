---
title: 分葉權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], permissions
- members [Master Data Services], leaf member permissions
- permissions [Master Data Services], leaf members
- leaf members [Master Data Services], attribute permissions
- attributes [Master Data Services], leaf member attribute permissions
ms.assetid: bde16e8c-bcd4-4041-8130-55c5450e5f72
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c34e517cadb6f529cd0406ae84a09eefc13f9c25
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817800"
---
# <a name="leaf-permissions-master-data-services"></a>分葉權限 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  分葉權限適用於某個實體所有分葉成員的屬性值。  
  
 如果是沒有啟用明確階層的實體，將權限指派給 [分葉] 與指派給實體相同。  
  
 **注意：**  
  
-   分葉權限只適用於使用者介面的總管功能區域。  
  
-   系統不會強制使用指派給 **Name** 和 **Code** 屬性的權限。  
  
|權限|Description|  
|----------------|-----------------|  
|**讀取**|使用者可以讀取分葉成員、屬性。|  
|**建立**|使用者可以建立分葉成員，並在建立期間指派屬性值。|  
|**Update**|使用者可以更新分葉成員和屬性。|  
|**刪除**|使用者可以刪除分葉成員。|  
|**拒絕**|拒絕所有對分葉成員的存取。|  
  
 讀取、建立、更新和刪除權限可以合併。 指派建立、更新和刪除時，將會自動指派讀取權限。  
  
## <a name="attribute-permissions"></a>屬性權限  
 屬性權限適用於特定實體的屬性值。 只有屬性權限的使用者無法加入或移除成員。  
  
|權限|Description|  
|----------------|-----------------|  
|**讀取**|使用者可以讀取屬性。|  
|**建立**|使用者可以在建立成員時指派值。|  
|**Update**|使用者可以更新屬性。|  
|**刪除**|沒有影響。|  
|**拒絕**|不顯示屬性。<br /><br /> 注意：您無法明確拒絕存取 Name 和 Code 屬性。|  
  
### <a name="example"></a>範例  
 如果是 Product 實體，請將 [更新] 權限指派給 Subcategory 屬性。 拒絕其他所有屬性的權限。  
  
|[屬性]|程式碼|Subcategory (更新)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|{5} Mountain Bikes|  
|Mountain-100|BK-M201|{5} Mountain Bikes|  
  
 在總管中，您可以更新 Subcategory 資料行中的任何屬性值。 如果您沒有屬性的權限，就不會顯示該屬性。  
  
> [!NOTE]  
>  在這個範例中，Subcategory 是根據 SubcategoryList 實體的網域屬性。 您可以為 Mountain-100 選取不同的子類別目錄，但是您無法從 SubcategoryList 實體中加入成員或刪除成員。  
  
## <a name="see-also"></a>另請參閱  
 [指派模型物件權限 &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
    
 [模型物件權限 &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [成員 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
