---
title: 要求屬性值 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], requiring attribute values
- attributes [Master Data Services], requiring values
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 03f868d679f1d51dbb672cfdab5dbeaa2b4fc8a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478866"
---
# <a name="require-attribute-values-master-data-services"></a>要求屬性值 (Master Data Services)
  當您想要確保主要資料完整時，在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中要求屬性值。  
  
> [!NOTE]  
>  在以網域屬性關聯性為基礎的衍生階層中，不會顯示遺漏網域屬性值的成員。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
### <a name="to-require-attribute-values"></a>若要要求屬性值  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [商務規則維護]**** 頁面上，選取 [模型]**** 清單中的模型。  
  
4.  從 [實體]**** 清單中選取實體。  
  
5.  從 [成員類型]**** 清單中，選取要套用商務規則的成員類型。  
  
6.  從 [屬性]**** 清單中，選取屬性或保留預設值 [全部]****。  
  
7.  按一下 [加入商務規則]****。  
  
8.  按一下 [編輯選取的商務規則]****。  
  
9. 在 [元件]**** 窗格中，展開 [動作]**** 節點。  
  
10. 按一下 [**必要**]，並將它拖曳至 [ **THEN** ] 窗格的 [**動作**] 標籤。  
  
11. 在 [屬性]**** 窗格中，按一下屬性並將它拖曳至 [編輯動作]**** 窗格的 [選取屬性]**** 標籤。  
  
12. 在 [編輯動作]**** 窗格中，按一下 [儲存項目]****。  
  
13. 按一下 [上一步]****。  
  
14. (選擇性) 在 [商務規則維護]**** 頁面上，針對包含商務規則的資料列，按兩下 [名稱]****、[描述]**** 或 [通知]**** 資料行中的資料格，以更新值。  
  
15. 按一下 [發行商務規則]****。  
  
16. 在確認對話方塊中按一下 **[確定]**。 規則狀態會變更為 [作用中]****。  
  
## <a name="next-steps"></a>後續步驟  
  
-   遵循下列其中一個程序，將商務規則套用至資料：  
  
    -   [根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [根據商務規則驗證版本 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [衍生階層 &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
  
