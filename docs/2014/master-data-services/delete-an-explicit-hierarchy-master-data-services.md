---
title: 刪除明確階層 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- explicit hierarchies, deleting
- deleting explicit hierarchies [Master Data Services]
ms.assetid: 4ce177b0-9884-47a2-9cea-212e845dd762
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: bfbc515c888e41d0ab216e3c0a7e56a5d2c4c8c4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103978"
---
# <a name="delete-an-explicit-hierarchy-master-data-services"></a>刪除明確階層 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，刪除不再需要的明確階層。  
  
> [!WARNING]  
>  當您刪除明確階層時，此階層中的所有合併成員也會一併刪除。 如果您刪除實體的所有明確階層，則實體的所有集合也會一併刪除，而且將不再針對明確階層和集合啟用該實體。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-delete-an-explicit-hierarchy"></a>若要刪除明確階層  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 **[模型檢視]** 頁面上，從功能表列指向 **[管理]** ，然後按一下 **[實體]**。  
  
3.  在 **[實體維護]** 頁面上，選取 **[模型]** 清單中的模型。  
  
4.  選取實體的資料列，該實體中包含您想要刪除的明確階層。  
  
5.  按一下 **[編輯選取的實體]**。  
  
6.  在 [**編輯實體**頁面上，於**明確階層**] 窗格中，按一下您想要刪除的明確階層。  
  
7.  按一下 **刪除選取的階層**。  
  
8.  在確認對話方塊中按一下 **[確定]**。  
  
9. 在另一個確認對話方塊中按一下 [確定]。  
  
## <a name="see-also"></a>另請參閱  
 [建立明確階層&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [明確階層&#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
