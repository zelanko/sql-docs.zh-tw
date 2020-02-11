---
title: 將多個條件新增至商務規則 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 54ab01033fc65f829f2a06bb5cbad8fc9e4d08f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65480186"
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>將多個條件加入至商務規則 (Master Data Services)
  如果您想要比較複雜的規則，請在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中將多個 **AND** 或 **OR** 條件新增至商務規則。  
  
> [!NOTE]  
>  如果您建立使用 **OR** 運算子的商務規則，請考慮為每個可獨立評估的條件陳述式建立不同的規則。 然後您可以視需要排除規則，提供更多彈性和輕鬆疑難排解。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   商務規則必須存在。 如需詳細資訊，請參閱[建立及發行商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)。  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>若要將多個條件加入至商務規則  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [商務規則維護]**** 頁面上，選取 [模型]**** 清單中的模型。  
  
4.  從 [實體]**** 清單中選取實體。  
  
5.  從 [**成員類型**] 清單中，選取成員的類型。  
  
6.  從 [屬性]**** 清單中，選取屬性或保留預設值 [全部]****。  
  
7.  按一下您想要編輯之商務規則的資料列。  
  
8.  按一下 [編輯選取的商務規則]****。  
  
9. 在 [**元件**] 窗格中，展開 [**邏輯運算子**] 節點。  
  
10. 按一下 [ **and** ] 或 [ **or** ]，並將它拖曳至 [ **IF** ] 窗格的**和**標籤。  
  
11. 在 [元件]**** 窗格中，展開 [條件]**** 節點。  
  
12. 按一下條件，並將它拖曳至 [ **IF** ] 窗格，並將其拖曳至步驟10中的**and**或**or**標籤。  
  
13. 在 [**屬性**] 窗格中，按一下屬性，並將它拖曳至 [**編輯條件**] 窗格的 [**選取屬性**] 標籤。  
  
14. 在 [**編輯條件**] 窗格中，完成所有必要的欄位。  
  
15. 在 [編輯條件]**** 窗格中，按一下 [儲存項目]****。  
  
16. （選擇性）若要加入更多條件，請從 [**元件**] 窗格中，將**and** **或 or 拖曳至** **IF**窗格中的任何**and** **或 or。** 接著遵循上述步驟 13 - 15。  
  
    > [!TIP]  
    >  若要刪除條件，請按一下條件的名稱，然後在 [**編輯條件**] 窗格中，按一下 [**刪除專案**]。  
  
## <a name="see-also"></a>另請參閱  
 [商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [變更商務規則名稱 &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [設定商務規則來傳送通知 &#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
