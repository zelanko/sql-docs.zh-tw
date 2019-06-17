---
title: 建立及發行商務規則 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], creating
- creating business rules [Master Data Services]
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2b52be0b8c76333b069c018415ff698f13f824ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479889"
---
# <a name="create-and-publish-a-business-rule-master-data-services"></a>建立及發行商務規則 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，建立商務規則，確保主要資料的正確性。 建立規則之後，您必須發行它，才能將它套用至資料。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
### <a name="to-create-and-publish-a-business-rule"></a>若要建立及發行商務規則  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]** 。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]** 。  
  
3.  在 [商務規則維護]  頁面上，選取 [模型]  清單中的模型。  
  
4.  從 [實體]  清單中選取實體。  
  
5.  從 [成員類型]  清單中，選取要套用商務規則的成員類型。  
  
6.  從 [屬性]  清單中，選取屬性或保留預設值 [全部]  。  
  
7.  按一下 [加入商務規則]  。  
  
8.  按一下 [編輯選取的商務規則]  。  
  
9. 在 [元件]  窗格中，展開 [條件]  節點。  
  
10. 按一下條件並將它拖曳至**IF**窗格中的**條件**標籤。  
  
    > [!TIP]  
    >  您也可以從您的商務規則刪除項目上按一下滑鼠右鍵，然後選擇**刪除**。  
  
11. 在 **屬性**窗格中，按一下屬性，並將它拖曳至**編輯條件**窗格的**選取屬性**標籤。  
  
12. 在 [**編輯條件**] 窗格中，完成任何必要的欄位。  
  
13. 在 [編輯條件]  窗格中，按一下 [儲存項目]  。  
  
14. 在 [元件]  窗格中，展開 [動作]  節點。  
  
15. 按一下動作並將它拖曳至 [THEN]  窗格的 [動作]  標籤。  
  
16. 在 [屬性]  窗格中，按一下屬性並將它拖曳至 [編輯動作]  窗格的 [選取屬性]  標籤。  
  
17. 在 [編輯動作]  窗格中，完成任何必要欄位。  
  
18. 在 [編輯動作]  窗格中，按一下 [儲存項目]  。  
  
19. 選擇性地將多個條件加入至規則。 如需詳細資訊，請參閱 [將多個條件加入至商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)(管理員 (Master Data Services))。  
  
20. 按一下 [上一步]  。  
  
21. (選擇性) 在 [商務規則維護]  頁面上，針對包含商務規則的資料列，按兩下 [名稱]  、[描述]  或 [通知]  資料行中的資料格，以更新值。  
  
    > [!NOTE]  
    >  只針對包含驗證動作的規則才傳送通知。  
  
22. 按一下 [發行商務規則]  。  
  
23. 在確認對話方塊中按一下 **[確定]** 。 規則狀態會變更為 [作用中]  。  
  
## <a name="next-steps"></a>後續步驟  
  
-   遵循下列其中一個程序，將商務規則套用至資料：  
  
    -   [根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [根據商務規則驗證版本 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [設定商務規則來傳送通知 &#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [變更商務規則名稱 &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [將多個條件加入至商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  
