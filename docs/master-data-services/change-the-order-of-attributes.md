---
title: "變更屬性的順序 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 835a032c-e37c-4f35-8ab0-5e4ae25c2e9b
caps.latest.revision: 5
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 706bb911a55ff319cf8fdceb9ac31fed419ef960
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="change-the-order-of-attributes"></a>變更屬性的順序
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以變更屬性的順序。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-change-the-order-of-an-attribute"></a>若要變更屬性的順序  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [管理模型]  頁面上，從方格中選取模型，然後按一下 [實體] 。  
  
3.  在 [管理實體]  頁面上，選取您要為其建立屬性之實體的資料列。  
  
4.  按一下 **[屬性]**。  
  
5.  在 [管理屬性] 頁面上，執行下列其中一項動作。  
  
    -   如果是分葉成員的屬性，請選取 [成員類型]  清單方塊的 [分葉]  。  
  
    -   如果是合併成員的屬性，請選取 [成員類型]  清單方塊的 [合併]  。  
  
    -   如果是集合的屬性，請選取 [成員類型]  清單方塊的 [集合]  。  
  
6.  選取您想要變更順序之屬性的資料列。  
  
    > [!NOTE]  
    >  無法變更 Name 或 Code 屬性的順序。  
  
7.  按一下 [上移] 或 [下移]。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  

