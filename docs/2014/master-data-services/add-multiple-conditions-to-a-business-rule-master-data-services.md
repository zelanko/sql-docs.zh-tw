---
title: 將多個條件新增至商務規則 (Master Data Services) | Microsoft Docs
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
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e5ac7bab7712a268e3fe8fd37f1a5ae799ef55dc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131531"
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>將多個條件加入至商務規則 (Master Data Services)
  如果您想要比較複雜的規則，請在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中將多個 **AND** 或 **OR** 條件新增至商務規則。  
  
> [!NOTE]  
>  如果您建立使用 **OR** 運算子的商務規則，請考慮為每個可獨立評估的條件陳述式建立不同的規則。 然後您可以視需要排除規則，提供更多彈性和輕鬆疑難排解。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   商務規則必須存在。 如需詳細資訊，請參閱[建立及發行商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)。  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>若要將多個條件加入至商務規則  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [商務規則維護] 頁面上，選取 [模型] 清單中的模型。  
  
4.  從 [實體] 清單中選取實體。  
  
5.  從**成員型別**清單中，選取 成員類型。  
  
6.  從 [屬性] 清單中，選取屬性或保留預設值 [全部]。  
  
7.  按一下您想要編輯之商務規則的資料列。  
  
8.  按一下 [編輯選取的商務規則]。  
  
9. 在**元件**] 窗格中，展開 [**邏輯運算子**節點。  
  
10. 按一下**AND**或**OR**將它拖曳到**如果**窗格的**AND**標籤。  
  
11. 在 [元件] 窗格中，展開 [條件] 節點。  
  
12. 按一下條件並將它拖曳至**如果**窗格為**AND**或**OR**步驟 10 中的標籤。  
  
13. 在**屬性** 窗格中，按一下屬性，並將它拖曳至**編輯條件**窗格的**Select 屬性**標籤。  
  
14. 在**編輯條件** 窗格中，完成任何必要的欄位。  
  
15. 在 [編輯條件] 窗格中，按一下 [儲存項目]。  
  
16. （選擇性） 若要加入多個條件，從**元件**窗格拖曳**AND**或**OR**任何**AND**或**OR**中**如果**窗格。 接著遵循上述步驟 13 - 15。  
  
    > [!TIP]  
    >  若要刪除條件，按一下 名稱的條件，然後在**編輯條件** 窗格中，按一下 **刪除項目**。  
  
## <a name="see-also"></a>另請參閱  
 [商務規則&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [變更商務規則名稱 &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [設定商務規則來傳送通知&#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  