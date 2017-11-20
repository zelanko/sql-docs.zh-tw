---
title: "刪除模型 (Master Data Services) | Microsoft Docs"
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
- deleting models [Master Data Services]
- models [Master Data Services], deleting models
ms.assetid: f0ad3cc4-aed7-47c8-94bc-2971fe9fe871
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: f1ac3250d2d1f852ec43bf88fb206b2009fc0430
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="delete-a-model-master-data-services"></a>刪除模型 (Master Data Services)
  刪除模型，從 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]移除模型及其所有資料。  
  
> [!NOTE]  
>  完成這個程序時，模型中所有版本的所有物件和所有資料都會永久刪除。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-delete-a-model"></a>若要刪除模型  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 **[模型檢視]** 頁面上，從功能表列指向 **[管理]** ，然後按一下 **[模型]**。  
  
3.  從 [管理模型] 頁面的方格中，選取您要刪除之模型的資料列。  
  
4.  按一下 **[刪除]**。  
  
5.  在確認對話方塊中按一下 **[確定]**。  
  
6.  在另一個確認對話方塊中按一下 [確定]。  
  
 方格中的 [狀態]  資料行會顯示模型上的作業狀態。 當您按一下 [儲存模型] 按鈕時，會顯示![正在更新](../master-data-services/media/mds-model-status-updating.png "正在更新")影像，表示正在更新模型。 如果建立或編輯模型時發生錯誤，則會顯示![錯誤](../master-data-services/media/mds-model-status-error.png "錯誤")影像。 否則，狀態為正常並顯示 ![[確定]](../master-data-services/media/mds-model-status-ok.png "[確定]") 影像。  
  
## <a name="see-also"></a>另請參閱  
 [模型 &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)   
 [建立模型 &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)  
  
  

