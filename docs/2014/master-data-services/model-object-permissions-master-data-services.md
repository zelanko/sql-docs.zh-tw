---
title: 模型物件權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], model objects
- models [Master Data Services], object permissions
ms.assetid: fab6335b-4cae-47de-ae7c-6c4743e0680f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 94ad81913071a3bbd4aad33515c27c68b9e268e4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482677"
---
# <a name="model-object-permissions-master-data-services"></a>模型物件權限 (Master Data Services)
  模型物件權限是強制性的。 這些權限會決定使用者可以在此 UI 的 [總管]**** 功能區域中存取的屬性。  
  
 例如，如果您將 Product 實體的 **更新** 權限指派給某個使用者，該使用者就可以更新 Product 實體的所有屬性。 如果您指派單一屬性的 **更新** 權限，使用者僅能更新該屬性。  
  
 若要判斷針對每個個別屬性值指派的安全性，可以將模型物件權限結合階層成員權限，後者可決定使用者可以存取的成員。  
  
 若要授與使用者對 [ **Explorer**] 以外功能區域的存取權，使用者必須是模型管理員，這也牽涉到指派模型物件使用權限。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
 在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]使用者介面（UI）中，會在 [**模型**] 索引標籤的 [**使用者和群組的許可權**] 功能區域中指派模型物件使用權限。在此索引標籤上，模型是以樹狀結構表示。 當您將權限指派給樹狀結構中的物件時，底下的所有物件都會繼承該權限。 您可以將權限指派給個別物件來覆寫該項繼承。  
  
 您可以將 [**唯讀**]、[**更新**] 或 [**拒絕**] 許可權指派給模型物件。 如果您未在 [模型]**** 索引標籤上指派任何權限，使用者就無法在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中檢視任何模型或資料。  
  
## <a name="best-practice"></a>最佳做法  
 一般而言，您應該指派模型物件的 [**更新**] 許可權，然後明確地將許可權指派給底下的物件。 如果您沒有指派底下物件的權限，就會繼承權限，而且使用者是管理員。  
  
## <a name="see-also"></a>另請參閱  
 [指派模型物件使用權限 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [模型許可權 &#40;Master Data Services&#41;](../../2014/master-data-services/model-permissions-master-data-services.md)   
 [功能區域許可權 &#40;Master Data Services&#41;](../../2014/master-data-services/functional-area-permissions-master-data-services.md)   
 [階層成員許可權 &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [如何決定權限 &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
