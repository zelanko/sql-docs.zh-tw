---
title: 建立網域屬性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5323072d5c58fcbe37becd00daacaac6ed3fb161
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031460"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>建立網域屬性 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，建立網域屬性，以使用實體成員來擴展屬性值。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   屬性值的來源實體必須存在。 例如，若要根據色彩實體建立網域屬性，您必須先建立色彩實體。 如需詳細資訊，請參閱[建立實體 &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md)。  
  
-   建立屬性的實體必須存在。 如需詳細資訊，請參閱[建立實體 &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md)。  
  
### <a name="to-create-a-domain-based-attribute"></a>若要建立網域屬性  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 **[模型檢視]** 頁面上，從功能表列指向 **[管理]** ，然後按一下 **[實體]**。  
  
3.  在 **[實體維護]** 頁面上，選取 **[模型]** 清單中的模型。  
  
4.  針對要建立屬性的實體選取資料列。  
  
5.  按一下 **[編輯選取的實體]**。  
  
6.  在 **[編輯實體]** 頁面上：  
  
    -   如果是分葉成員的屬性，則按一下 **[分葉成員屬性]** 窗格中的 **[加入分葉屬性]**。  
  
    -   如果是合併成員的屬性，則按一下 **[合併成員屬性]** 窗格中的 **[加入合併屬性]**。  
  
    -   如果是集合的屬性，則按一下 **[集合屬性]** 窗格中的 **[加入集合屬性]**。  
  
7.  在**加入屬性**頁面上，選取**網域**選項。  
  
8.  在 **[名稱]** 方塊中，輸入屬性的名稱。 它不需要和屬性值的來源實體同名。  
  
9. 在 **[顯示像素寬度]** 方塊中，輸入要在 **[總管]** 方格中顯示的屬性資料行寬度。  
  
10. 從**實體**清單中，選擇要用來擴展屬性值的實體。  
  
11. 選擇性。 選取 [啟用變更追蹤] 以追蹤屬性群組的變更。 如需詳細資訊，請參閱[將屬性加入至變更追蹤群組 &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。  
  
12. 按一下 **[儲存屬性]**。  
  
13. 按一下 **[實體維護]** 頁面上的 **[儲存實體]**。  
  
## <a name="see-also"></a>另請參閱  
 [網域型屬性&#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)   
 [建立衍生的階層&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [變更屬性名稱&#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [刪除屬性&#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-master-data-services.md)  
  
  