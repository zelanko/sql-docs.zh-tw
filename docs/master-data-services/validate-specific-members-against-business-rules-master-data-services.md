---
title: 根據商務規則驗證特定成員
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 885d0c1018c1d30fd4ea5d10276c971dbbf0a114
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73728854"
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>根據商務規則驗證特定成員 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  如果您想要更新或依照商務規則驗證成員子集，請在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中選擇性地套用商務規則。  
  
> [!NOTE]  
>  如果您想要將商務規則套用至某版本模型中的所有成員，請參閱 [根據商務規則驗證版本 &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
-   針對要套用商務規則的模型物件，您必須至少擁有 **[更新]** 權限。  
  
### <a name="to-apply-business-rules-selectively"></a>若要選擇性地套用商務規則  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取 [模型]**** 下拉式清單中的模型。  
  
2.  從 [版本]**** 下拉式清單中，選取版本。  
  
3.  按一下 [總管] **** 索引標籤。  
  
4.  從功能表列指向 **[實體]** ，然後按一下包含要套用規則之成員的實體名稱。  
  
5.  按一下 [套用規則] ****。 商務規則只套用至方格中顯示的成員。  
  
## <a name="see-also"></a>另請參閱  
 [根據商務規則驗證版本 &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
