---
title: "建立及發行商務規則 (Master Data Services) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], creating
- creating business rules [Master Data Services]
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
caps.latest.revision: 14
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b8ea50a2feb5c35e431422c1786d7731bf97d8fb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="create-and-publish-a-business-rule-master-data-services"></a>建立及發行商務規則 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，建立商務規則，確保主要資料的正確性。 建立規則之後，您必須發行它，才能將它套用至資料。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-create-and-publish-a-business-rule"></a>若要建立及發行商務規則  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 [管理]，然後按一下 [商務規則]。  
  
3.  在 [商務規則] 頁面上，從 [模型] 下拉式清單選取模型。  
  
4.  從 [實體] 下拉式清單中，選取實體。  
  
5.  從 [成員類型]  下拉式清單中，選取要套用商務規則的成員類型。  
  
6.  按一下 **[加入]**。  
  
7.  在 [名稱]  方塊中，輸入商務規則的名稱。  
  
8.  (選擇性) 在 [描述] 欄位中，輸入商務規則描述。  
  
9. 或者選取 [傳送通知] 選項，然後從下拉式清單選取要向其傳送電子郵件通知的使用者或群組。  
  
    > [!NOTE]  
    >  只針對包含驗證動作的規則才傳送通知。  
  
10. 在 [If] 區塊下，按一下 [新增]。 面板隨即出現。  
  
11. 從 [屬性] 下拉式清單中選取屬性。  
  
12. 從 [運算子] 下拉式清單中選取條件。  
  
13. 完成所有必要的欄位。  
  
14. 按一下 [儲存] 按鈕。 新的資料列就會新增至 [If] 方格中。  
  
    > [!TIP]  
    >  您可以刪除商務規則中的項目，方法是以滑鼠右鍵按一下各項目，然後選擇 [刪除]。  
  
15. 選擇性地將多個條件加入至規則。 如需詳細資訊，請參閱[將多個條件加入至商務規則 &#40;Master Data Services&#41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)。  
  
16. 在 [Then] 區塊下，按一下 [新增]。 面板隨即出現。  
  
17. 從 [屬性] 下拉式清單中選取屬性。  
  
18. 從 [運算子] 下拉式清單中選取動作。  
  
19. 完成所有必要的欄位。  
  
20. 按一下 **[儲存]**。 新的資料列就會新增至 [Then] 方格中。  
  
21. 或者，若要新增 **Else** 動作，請完成下列步驟。  
  
    1.  在 [Else] 區塊下，按一下 [新增]。 面板隨即出現。  
  
    2.  從 [屬性] 下拉式清單中選取屬性。  
  
    3.  從 [運算子] 下拉式清單中選取動作。  
  
    4.  完成所有必要的欄位。  
  
    5.  按一下 **[儲存]**。 新的資料列就會新增至 [Else] 方格中。  
  
22. 按一下 **[儲存]**。 新的資料列就會加入商務規則方格中。  
  
23. 按一下 [全部發行]。  
  
24. 在確認對話方塊中按一下 **[確定]**。 [商務規則狀態] 資料行中的值是 [使用中]。  
  
## <a name="grid-columns"></a>方格資料行  
 對於每個建立的商務規則，會將含有六個資料行的資料列加入方格中。 以下是資料行。  
  
|名稱|說明|  
|----------|-----------------|  
|狀態|當您按一下 [儲存]，下列影像隨即顯示，指出正在更新商務規則。<br /><br /> ![mds_BR_refresh](../master-data-services/media/mds-br-refresh.png "mds_BR_refresh")<br /><br /> 如果建立或編輯商務規則時發生錯誤，則會顯示下列影像。<br /><br /> ![mds_br_error](../master-data-services/media/mds-br-error.png "mds_br_error")<br /><br /> 如果狀態正常，則會顯示下列影像。<br /><br /> ![mds_BR_success](../master-data-services/media/mds-br-success.png "mds_BR_success")|  
|名稱|商務規則名稱。|  
|說明|商務規則描述。|  
|商務規則狀態|下列商務規則狀態之一：未定義規則、使用中、排除、暫止變更、暫止排除及暫止刪除。|  
|已排除|指定商務規則是否已排除。|  
|通知|指定選取傳送電子郵件通知的使用者或群組。|  
  
## <a name="next-steps"></a>後續步驟  
  
-   遵循下列其中一個程序，將商務規則套用至資料：  
  
    -   [根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [根據商務規則 &#40; 驗證版本Master Data services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [設定商務規則來傳送通知 &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [變更商務規則名稱 &#40;Master Data services&#41;](../master-data-services/change-a-business-rule-name-master-data-services.md)   
 [將多個條件加入至商務規則 &#40;Master Data services&#41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  
