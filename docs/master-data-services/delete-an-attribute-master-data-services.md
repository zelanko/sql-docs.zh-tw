---
title: "刪除屬性 (Master Data Services) |Microsoft 文件"
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
helpviewer_keywords:
- attributes [Master Data Services], deleting
- deleting attributes [Master Data Services]
ms.assetid: ec3e66f7-0e35-43d7-a80d-64899948ebfe
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1d36564680430b7d35c415e23586c7fd0c47e084
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="delete-an-attribute-master-data-services"></a>刪除屬性 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中，如果您想要永久刪除某個屬性以及所有關聯的屬性值，請刪除此屬性。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-delete-an-attribute"></a>若要刪除屬性  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [管理模型]  頁面上，從方格中選取模型，然後按一下 [實體] 。  
  
3.  在 [管理實體]  頁面上，選取您要為其建立屬性之實體的資料列。  
  
4.  按一下 **[屬性]**。  
  
5.  在 [管理屬性] 頁面上，執行下列其中一項動作。  
  
    -   如果是分葉成員的屬性，請選取 [成員類型]  清單方塊的 [分葉]  。  
  
    -   如果是合併成員的屬性，請選取 [成員類型]  清單方塊的 [合併]  。  
  
    -   如果是集合的屬性，請選取 [成員類型]  清單方塊的 [集合]  。  
  
6.  選取要刪除之屬性的資料列。  
  
    > [!NOTE]  
    >  您不能刪除 Name 或 Code 屬性。  
  
7.  按一下 **[刪除]**。  
  
8.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;Master Data services& #41;](../master-data-services/attributes-master-data-services.md)   
 [網域型屬性 & #40;Master Data services& #41;](../master-data-services/domain-based-attributes-master-data-services.md)   
 [建立文字屬性 & #40;Master Data services& #41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [建立網域屬性 & #40;Master Data services& #41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
