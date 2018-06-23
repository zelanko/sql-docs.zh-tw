---
title: 建立訂閱檢視 (Master Data Services) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0b79bd1e50871fb921a3ce2b3fe9e43ab0995a9e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135203"
---
# <a name="create-a-subscription-view-master-data-services"></a>建立訂閱檢視 (Master Data Services)
  當您想要建立的檢視中的資料建立訂閱檢視[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]資料庫以供訂閱系統。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[整合管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-create-a-subscription-view"></a>若要建立訂閱檢視  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，按一下 **[整合管理]**。  
  
2.  按一下功能表列上的 **[建立檢視表]**。  
  
3.  在**訂閱檢視**頁面上，按一下**加入訂閱檢視**。  
  
4.  在**建立訂閱檢視**窗格，請在**訂閱檢視名稱**方塊中，輸入檢視的名稱。  
  
5.  從 **[模型]** 清單中選取模型。  
  
6.  選取 **版本**或**版本旗標**選項，然後再選取 從對應的清單。  
  
    > [!TIP]  
    >  根據版本旗標建立訂閱檢視。 當您鎖定版本時，您可以重新指派旗標給開啟的版本，而不用更新訂閱檢視。  
  
7.  選取 **實體**或**衍生階層**選項，然後再選取 從對應的清單。  
  
8.  從 **[格式]** 清單中選取訂閱檢視格式。  
  
9. 如果您從 **[格式]** 清單中選擇 **[明確層級]** 或 **[衍生層級]** ，請輸入階層內要加入檢視中的層級數。  
  
10. 按一下 **[儲存]**。  
  
## <a name="see-also"></a>另請參閱  
 [匯出資料&#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)   
 [刪除訂閱檢視 &#40;Master Data Services&#41;](delete-a-subscription-view-master-data-services.md)   
 [建立版本旗標&#40;Master Data Services&#41;](create-a-version-flag-master-data-services.md)  
  
  