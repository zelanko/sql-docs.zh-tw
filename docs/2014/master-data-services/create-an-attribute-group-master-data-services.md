---
title: 建立屬性群組 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], creating
- creating attribute groups [Master Data Services]
ms.assetid: 798c325e-e8d8-412a-b02e-118f2741d1c7
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c832fe601eb7151e438d7f93c3e39e9b249ea246
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483326"
---
# <a name="create-an-attribute-group-master-data-services"></a>建立屬性群組 (Master Data Services)
  當您想要在總管  方格的個別索引標籤上顯示屬性時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中建立屬性群組。  
  
> [!NOTE]  
>  當您建立屬性群組時，它會自動隱藏起來不讓所有使用者看到，除了建立它的使用者以外。 如需如何顯示此群組的詳細資訊，請參閱 [讓使用者看到屬性群組 &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md)。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   至少有一個屬性必須存在。 如需詳細資訊，請參閱 [建立文字屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)(管理員 (Master Data Services))。  
  
### <a name="to-create-an-attribute-group"></a>若要建立屬性群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]** 。  
  
2.  在 **模型檢視**頁面上，從功能表列指向**管理**，按一下 **屬性群組**。  
  
3.  從 **[模型]** 清單中選取模型。  
  
4.  從 [實體]  清單中選取實體。  
  
5.  按一下 [分葉群組]  、[合併群組]  或 [集合群組]  ，分別為分葉成員、合併成員或集合建立屬性群組。  
  
6.  按一下 **加入屬性群組**。  
  
7.  在 **分葉群組名稱**方塊中，輸入群組的名稱。 這是在索引標籤上顯示的名稱**總管**。  
  
    > [!NOTE]  
    >  如果您選取**合併群組**或是**集合群組**在步驟 5 中，此方塊，則**合併群組名稱**或**集合群組名稱**分別。  
  
8.  按一下 [儲存群組]  。  
  
9. 展開群組的資料夾。  
  
10. 按一下 **[屬性]** 。  
  
11. 按一下 **編輯選取的項目**。  
  
12. 按一下 在 屬性**可用**方塊，然後按一下**新增**箭號。 若要全部加入，請按一下 [全部加入]  箭號。  
  
13. （選擇性） 按一下**向上**並**向下**箭號，變更由左到右的順序屬性。  
  
14. 按一下 [儲存]  。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [讓使用者看到屬性群組 &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [屬性群組 &#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [變更屬性群組名稱 &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [刪除屬性群組 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-group-master-data-services.md)   
 [分葉權限&#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [合併的權限&#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)  
  
  
