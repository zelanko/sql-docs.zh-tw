---
title: "要求屬性值 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], requiring attribute values
- attributes [Master Data Services], requiring values
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
caps.latest.revision: 9
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: c80f990580f849dcee4038ec0ca45ea1c18ffff5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="require-attribute-values-master-data-services"></a>要求屬性值 (Master Data Services)
  當您想要確保主要資料完整時，在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中要求屬性值。  
  
> [!NOTE]  
>  在以網域屬性關聯性為基礎的衍生階層中，不會顯示遺漏網域屬性值的成員。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-require-attribute-values"></a>若要要求屬性值  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [商務規則]  頁面上，從 [模型]  下拉式清單選取模型。  
  
4.  從 [實體]  下拉式清單選取實體。  
  
5.  從 [成員類型]  下拉式清單中，選取要套用商務規則的成員類型。  
  
6.  按一下 **[加入]**。  
  
7.  在 [名稱]  方塊中，輸入商務規則的名稱。  
  
8.  (選擇性) 在 [描述]  欄位中，輸入商務規則描述。  
  
9. 在 [Then]\(則)  區塊下，按一下 [加入] 。 面板隨即顯示。  
  
10. 從 [運算子]  下拉式清單中，選取 [required action]\(必要動作) 。  
  
11. 從 [屬性]  下拉式清單中，選取屬性。  
  
12. 按一下 **[儲存]**。 新的資料列就會加入 [Then]\(則)  方格中。  
  
13. 按一下 **[儲存]**。  
  
14. 按一下 [全部發行] 。  
  
15. 在確認對話方塊中按一下 **[確定]**。 [商務規則狀態] 資料行中的值是 [使用中]。  
  
## <a name="next-steps"></a>後續步驟  
  
-   遵循下列其中一個程序，將商務規則套用至資料：  
  
    -   [根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [根據商務規則驗證版本 &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [衍生階層 &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  

