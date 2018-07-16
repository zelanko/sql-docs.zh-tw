---
title: 根據商務規則驗證特定成員 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
caps.latest.revision: 4
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 9f3a3c6f4c812c5fc68479ef8ed3499a9e02b386
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314058"
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>根據商務規則驗證特定成員 (Master Data Services)
  如果您想要更新或依照商務規則驗證成員子集，請在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中選擇性地套用商務規則。  
  
> [!NOTE]  
>  如果您想要將商務規則套用至某版本模型中的所有成員，請參閱[根據商務規則驗證版本 &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md)。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
-   針對要套用商務規則的模型物件，您必須至少擁有 **[更新]** 權限。  
  
### <a name="to-apply-business-rules-selectively"></a>若要選擇性地套用商務規則  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取 **[模型]** 清單中的模型。  
  
2.  從 **[版本]** 清單中選取版本。  
  
3.  按一下 **[總管]**。  
  
4.  從功能表列指向 **[實體]** ，然後按一下包含要套用規則之成員的實體名稱。  
  
5.  按一下 [套用商務規則]。 商務規則只套用至方格中顯示的成員。  
  
## <a name="see-also"></a>另請參閱  
 [根據商務規則驗證版本&#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md)   
 [商務規則&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
