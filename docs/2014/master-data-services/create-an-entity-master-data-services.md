---
title: 建立實體 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 23e267d78091895e5d0ec899835ce7aa09e8c9d3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023569"
---
# <a name="create-an-entity-master-data-services"></a>建立實體 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，建立實體以包含成員及其屬性。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   模型必須存在。 如需詳細資訊，請參閱[建立模型 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-model-master-data-services.md)。  
  
### <a name="to-create-an-entity"></a>若要建立實體  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 **[模型檢視]** 頁面上，從功能表列指向 **[管理]** ，然後按一下 **[實體]**。  
  
3.  在 **[實體維護]** 頁面上，選取 **[模型]** 清單中的模型。  
  
4.  按一下**加入實體**。  
  
5.  在**實體名稱**方塊中，輸入實體的名稱。  
  
6.  在**暫存資料表名稱**方塊中，輸入暫存資料表的名稱。  
  
    > [!TIP]  
    >  使用模型名稱當做暫存資料表名稱的一部分，例如 *Modelname_Entityname*。 這樣會更容易在資料庫中找到資料表。 如需暫存資料表的詳細資訊，請參閱[資料匯入&#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。  
  
7.  選擇性。 選取 **[自動建立字碼值]** 核取方塊。 如需詳細資訊，請參閱[自動建立代碼 &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md)。  
  
8.  從**啟用明確階層和集合**清單中，選取下列選項之一：  
  
    -   **否**。 如果不需要啟用明確階層和集合的實體，請選取這個選項。 您稍後可以視需要加以變更。  
  
    -   **[是]**。 如果想要啟用明確階層和集合的實體，請選取這個選項。 在**明確階層名稱**方塊中輸入名稱。 （選擇性） 選取**強制階層 (已包含所有分葉成員**，讓明確階層成為強制階層。  
  
9. 按一下**儲存實體**。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [建立文字屬性&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [建立網域屬性&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [建立檔案屬性&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [實體&#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)   
 [明確階層&#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [變更實體名稱&#40;Master Data Services&#41;](edit-an-entity-master-data-services.md)   
 [刪除實體&#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-entity-master-data-services.md)  
  
  