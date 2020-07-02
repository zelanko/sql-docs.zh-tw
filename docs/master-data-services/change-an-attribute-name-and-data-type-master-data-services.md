---
title: 變更屬性名稱和類型
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], changing name
ms.assetid: d348f238-f59d-41c7-ad20-3ccd55bfd9e5
author: lrtoyou1223
ms.author: lle
manager: erikre
ms.openlocfilehash: cb7d82f63f41baa88523f97e45a65635e1d49486
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813462"
---
# <a name="change-an-attribute-name-and-data-type-master-data-services"></a>變更屬性名稱和資料類型 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以變更屬性的名稱。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-change-an-attribute-name-and-type"></a>變更屬性名稱和類型  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [**管理模型**] 頁面上，從方格中選取模型，然後按一下 [**實體**]。  
  
3.  在 [管理實體] **** 頁面上，選取您要為其建立屬性之實體的資料列。  
  
4.  按一下 **[屬性]**。  
  
5.  在 [管理屬性]**** 頁面上，執行下列其中一項動作。  
  
    -   如果是分葉成員的屬性，請選取 [成員類型] **** 清單方塊的 [分葉] **** 。  
  
    -   如果是合併成員的屬性，請選取 [成員類型] **** 清單方塊的 [合併] **** 。  
  
    -   如果是集合的屬性，請選取 [成員類型] **** 清單方塊的 [集合] **** 。  
  
6.  選取要編輯的屬性資料列，然後按一下 [編輯]****。  
  
7.  在 [名稱]**** 方塊中，輸入屬性的更新名稱。 如需不應當做屬性名稱使用的字組清單，請參閱[保留字 &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md)。  
  
8.  從 [屬性類型]**** 清單中，選取另一個類型。  
  
9. 按一下 [檔案] 。  
  
## <a name="see-also"></a>另請參閱  
 [建立 &#40;Master Data Services&#41;的文字屬性](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [刪除屬性 &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-master-data-services.md)   
 [屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
