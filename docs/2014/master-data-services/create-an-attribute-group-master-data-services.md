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
ms.openlocfilehash: 0a9959189b3ce805c7d8e97dd3b4948a3674b0cb
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971728"
---
# <a name="create-an-attribute-group-master-data-services"></a>建立屬性群組 (Master Data Services)
  當您想要在總管**** 方格的個別索引標籤上顯示屬性時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中建立屬性群組。  
  
> [!NOTE]  
>  當您建立屬性群組時，它會自動隱藏起來不讓所有使用者看到，除了建立它的使用者以外。 如需如何顯示此群組的詳細資訊，請參閱 [讓使用者看到屬性群組 &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md)。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)。  
  
-   至少有一個屬性必須存在。 如需詳細資訊，請參閱 [建立文字屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)(管理員 (Master Data Services))。  
  
### <a name="to-create-an-attribute-group"></a>若要建立屬性群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [**模型視圖**] 頁面上，從功能表列指向 [**管理**]，然後按一下 [**屬性群組**]。  
  
3.  從 **[模型]** 清單中選取模型。  
  
4.  從 [實體]**** 清單中選取實體。  
  
5.  按一下 [分葉群組]****、[合併群組]**** 或 [集合群組]****，分別為分葉成員、合併成員或集合建立屬性群組。  
  
6.  按一下 [**加入屬性群組**]。  
  
7.  在 [分**葉組名**] 方塊中，輸入群組的名稱。 這是 [ **Explorer**] 索引標籤上顯示的名稱。  
  
    > [!NOTE]  
    >  如果您在步驟5中選取了 **[合併群組**] 或 [**集合群組**]，此方塊會分別是 **[合併組名**] 或 [**集合組名**]。  
  
8.  按一下 [儲存群組]****。  
  
9. 展開群組的資料夾。  
  
10. 按一下 **[屬性]**。  
  
11. 按一下 [**編輯選取的專案**]。  
  
12. 按一下 [**可用**] 方塊中的 [屬性]，然後按一下 [**新增**] 箭號。 若要全部加入，請按一下 [全部加入]**** 箭號。  
  
13. （選擇性）按一下**向上**和**向下**箭號，變更屬性由左至右的順序。  
  
14. 按一下 [檔案] 。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [讓使用者看到屬性群組 &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [屬性群組 &#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [Master Data Services &#40;的屬性&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [變更屬性組名 &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [刪除屬性群組 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-group-master-data-services.md)   
 [分葉許可權 &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [合併的許可權 &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)  
  
  
