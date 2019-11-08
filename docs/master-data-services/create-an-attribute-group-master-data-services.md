---
title: 建立屬性群組
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], creating
- creating attribute groups [Master Data Services]
ms.assetid: 798c325e-e8d8-412a-b02e-118f2741d1c7
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 534e8bed6596c9b15e05ec179ece3d37a64b15ac
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728448"
---
# <a name="create-an-attribute-group-master-data-services"></a>建立屬性群組 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  當您想要在總管[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]**方格的個別索引標籤上顯示屬性時，可以在**  中建立屬性群組。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   至少有一個屬性必須存在。 如需詳細資訊，請參閱[建立文字屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)。  
  
### <a name="to-create-an-attribute-group"></a>若要建立屬性群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]** 。  
  
2.  在 [管理模型] 頁面上，從方格中選取模型，然後按一下 [實體]。  
  
3.  在 [管理實體] 頁面上，從方格中選取含有您想要為其建立屬性群組之實體的資料列。  
  
4.  按一下 [屬性群組]。  
  
5.  在 [管理屬性群組] 頁面上，執行下列其中一項動作，然後按一下 [加入]。  
  
     如果是分葉成員的屬性群組，請從頁面頂端的 [成員類型] 下拉式清單中選取 [分頁]。  
  
     如果是合併成員的屬性群組，請從 [成員類型] 下拉式清單中選取 [合併]。  
  
     如果是集合的屬性群組，請從 [成員類型] 下拉式清單中選取 [集合]。  
  
6.  按一下 [分葉群組]、[合併群組] 或 [集合群組]，分別為分葉成員、合併成員或集合建立屬性群組。  
  
7.  在 [名稱] 方塊中，輸入屬性群組的名稱。 這是在總管的索引標籤上所顯示的名稱。  
  
8.  若要加入屬性，請按一下 [可用的屬性] 方塊，然後按一下 [加入] 箭號。 若要加入所有屬性，請按一下 [全部加入] 箭號。  
  
9. 按一下 [向上] 或 [向下] 箭號，變更屬性由左至右的順序。  
  
10. 按一下 [可用使用者] 方塊中的使用者，然後按一下 [加入] 箭號。 若要加入全部的使用者，請按一下 [全部加入] 箭號。  
  
11. 按一下 [可用群組] 方塊中的群組，然後按一下 [加入] 箭號。 若要加入全部的群組，請按一下 [全部加入] 箭號。  
  
12. 按一下 **[儲存]** 。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [讓使用者看到屬性群組 &#40;Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [屬性群組 &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [變更屬性群組名稱 &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [刪除屬性群組 &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-group-master-data-services.md)   
 [分葉權限 &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)   
   
  
  
