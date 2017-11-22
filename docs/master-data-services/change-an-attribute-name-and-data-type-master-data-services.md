---
title: "變更屬性名稱和資料類型 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: attributes [Master Data Services], changing name
ms.assetid: d348f238-f59d-41c7-ad20-3ccd55bfd9e5
caps.latest.revision: "9"
author: smartysanthosh
ms.author: nagavo
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a5f5873fe266f484f27af64e7a7833e496cf0696
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="change-an-attribute-name-and-data-type-master-data-services"></a>變更屬性名稱和資料類型 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以變更屬性的名稱。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-change-an-attribute-name-and-type"></a>變更屬性名稱和類型  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [管理模型]  頁面上，從方格中選取模型，然後按一下 [實體] 。  
  
3.  在 [管理實體]  頁面上，選取您要為其建立屬性之實體的資料列。  
  
4.  按一下 **[屬性]**。  
  
5.  在 [管理屬性] 頁面上，執行下列其中一項動作。  
  
    -   如果是分葉成員的屬性，請選取 [成員類型]  清單方塊的 [分葉]  。  
  
    -   如果是合併成員的屬性，請選取 [成員類型]  清單方塊的 [合併]  。  
  
    -   如果是集合的屬性，請選取 [成員類型]  清單方塊的 [集合]  。  
  
6.  選取要編輯的屬性資料列，然後按一下 [編輯]。  
  
7.  在 [名稱] 方塊中，輸入屬性的更新名稱。 如需不應該當做屬性名稱使用的字詞清單，請參閱[保留字 &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md)。  
  
8.  從 [屬性類型] 清單中，選取另一個類型。  
  
9. 按一下 **[儲存]**。  
  
## <a name="see-also"></a>另請參閱  
 [建立文字屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [刪除屬性 &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-master-data-services.md)   
 [屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
