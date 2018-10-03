---
title: 模型物件權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], model objects
- models [Master Data Services], object permissions
ms.assetid: fab6335b-4cae-47de-ae7c-6c4743e0680f
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 9d2289a199ec54eacb42a5fce175f91872ab8133
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848860"
---
# <a name="model-object-permissions-master-data-services"></a>模型物件權限 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  模型物件權限是強制性的。 這些權限會決定使用者可以在此 UI 的 [總管] 功能區域中存取的屬性。  
  
 例如，如果您將 Product 實體的**更新**權限指派給某個使用者，該使用者就可以更新 Product 實體的所有屬性。 如果您指派單一屬性的 **更新** 權限，使用者僅能更新該屬性。  
  
 若要判斷針對每個個別屬性值指派的安全性，可以將模型物件權限結合階層成員權限，後者可決定使用者可以存取的成員。  
  
 若要授與使用者對 [總管] 以外功能區域的存取權，使用者必須是模型系統管理員，因為也需要指派物件模型的系統管理員權限。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
 您可在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者介面 (UI) 中，[使用者與群組權限] 功能區域的 [模型] 索引標籤上指派模型物件權限。在這個索引標籤上，模型是以樹狀結構來表示。 當您將權限指派給樹狀結構中的物件時，底下的所有物件都會繼承該權限。 您可以將權限指派給個別物件來覆寫該項繼承。  
  
 您可以指派模型物件的 [讀取]、[建立]、[更新] 和 [刪除] 或 [拒絕] 權限的組合。 如果您未在 [模型] 索引標籤上指派任何權限，使用者就無法在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中檢視任何模型或資料。  
  
## <a name="best-practice"></a>最佳作法  
 一般而言，您應該指派模型物件的 [全部] 權限，然後明確地指派底下物件的權限。  
  
## <a name="external-resources"></a>外部資源  
 請參考 msdn.com 上的 [Security Improvements](http://go.microsoft.com/fwlink/p/?LinkId=615376)(安全性改進) 部落格文章。  
  
## <a name="see-also"></a>另請參閱  
 [指派模型物件權限 &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [模型權限 &#40;Master Data Services&#41;](../master-data-services/model-permissions-master-data-services.md)   
 [功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)   
 [階層成員權限 &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [如何決定權限 &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
