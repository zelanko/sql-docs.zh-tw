---
title: "刪除明確階層 (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- explicit hierarchies, deleting
- deleting explicit hierarchies [Master Data Services]
ms.assetid: 4ce177b0-9884-47a2-9cea-212e845dd762
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: c1e0b7164a6ca7d43c2a223839cff9df1960df60
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="delete-an-explicit-hierarchy-master-data-services"></a>刪除明確階層 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，刪除不再需要的明確階層。  
  
> [!WARNING]  
>  當您刪除明確階層時，此階層中的所有合併成員也會一併刪除。 如果您刪除實體的所有明確階層，則實體的所有集合也會一併刪除，而且將不再針對明確階層和集合啟用該實體。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-delete-an-explicit-hierarchy"></a>若要刪除明確階層  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [管理模型]  頁面上，從方格中選取模型，然後按一下 [實體] 。  
  
3.  在 [管理實體]  頁面上，從格線中選取含有您想要刪除之明確階層的實體資料列。  
  
4.  按一下 [明確階層] 。  
  
5.  在 [Manage Explicit Hierarchy]  \(管理明確階層) 頁面上，按一下您想要刪除的明確階層。  
  
6.  按一下 **[編輯]**。  
  
7.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [建立明確階層 &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [明確階層 &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  

