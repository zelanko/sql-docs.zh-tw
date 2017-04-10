---
title: "模型權限 (Master Data Services) | Microsoft Docs"
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
  - "模型 [Master Data Services], 權限"
  - "權限 [Master Data Services], 模型"
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# 模型權限 (Master Data Services)
  模型權限適用於所有實體、衍生階層、明確階層及存在於模型內的集合。 可以針對任何個別的物件來覆寫指派給模型的權限。  
  
> [!NOTE]  
>  如果使用者是模型管理員，則使用者介面的所有功能區域中都會顯示此模型。 否則，此模型只會顯示在 [總管] 功能區域中。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
|權限|說明|  
|----------------|-----------------|  
|**讀取**|使用者可以讀取成員、屬性、階層成員資格或集合成員資格。|  
|**建立**|使用者可以建立成員，並在建立期間指派屬性值。|  
|**Update**|使用者可以更新成員、屬性、階層成員資格或集合成員資格。|  
|**Delete**|使用者可以刪除成員。|  
|**拒絕**|拒絕所有對模型的存取。|  
|**管理**|模型的管理員權限。 模型層級才提供管理員權限。|  
  
 讀取、建立、更新和刪除權限可以彼此合併。 指派建立、更新和刪除權限時，將會自動指派讀取權限。  
  
## 另請參閱  
 [指派模型物件權限 &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [模型物件權限 &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [實體權限 &#40;Master Data Services&#41;](../master-data-services/entity-permissions-master-data-services.md)   
 [集合權限 &#40;Master Data Services&#41;](../master-data-services/collection-permissions-master-data-services.md)  
  
  