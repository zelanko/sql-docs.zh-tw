---
title: 將屬性新增至變更追蹤群組 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 6d215fe6a1b0c41868816e09e64927b8f736f8c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877483"
---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>將屬性加入至變更追蹤群組 (Master Data Services)
  當您想要追蹤屬性值變更時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中將屬性新增至變更追蹤群組。  
  
> [!NOTE]  
>  將屬性加入至變更追蹤群組之後，當屬性值變更時， [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中的屬性會標示為已變更。 建立商務規則，以根據變更來執行動作。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   屬性必須存在，才能加入至變更追蹤群組。 如需詳細資訊，請參閱[建立文字屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)。  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>若要將屬性加入至變更追蹤群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在上**模型總管**頁面上，從功能表列指向**管理**，按一下 **實體**。  
  
3.  在 **[實體維護]** 頁面上，選取 **[模型]** 清單中的模型。  
  
4.  針對要追蹤屬性值的實體選取資料列。  
  
5.  按一下 **[編輯選取的實體]**。  
  
6.  在 **[編輯實體]** 頁面上：  
  
    -   如果屬性是在分葉成員**屬性的分葉**窗格中，選取屬性，然後按一下**編輯分葉屬性**。  
  
    -   如果屬性是合併成員，在**合併屬性**窗格中，選取屬性，然後按一下**編輯合併屬性**。  
  
    -   如果屬性是集合，在**集合屬性**窗格中，選取屬性，然後按一下**編輯集合屬性**。  
  
7.  選取 [啟用變更追蹤] 核取方塊。  
  
8.  在 [變更追蹤群組] 方塊中，輸入群組的編號。  
  
9. 按一下 **[儲存屬性]**。  
  
10. 按一下 **[實體維護]** 頁面上的 **[儲存實體]**。  
  
11. 重複此程序，加入要包含在群組中的所有屬性。 對群組中的每個屬性，使用相同的變更追蹤群組編號。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [根據屬性值變更來起始動作 &#40;Master Data Services&#41;](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [建立文字屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)   
 [建立網域屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
