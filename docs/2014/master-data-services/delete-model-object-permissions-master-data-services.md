---
title: 刪除模型物件權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting model object permissions [Master Data Services]
- permissions [Master Data Services], deleting model object permissions
- models [Master Data Services], deleting object permissions
ms.assetid: 859c5952-f600-4940-8064-1afd13f7f6dc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 1a0cb087f5a0cd429d9bc6f30ea08aaef3d07b3b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483098"
---
# <a name="delete-model-object-permissions-master-data-services"></a>刪除模型物件權限 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，刪除模型物件權限，移除所做的任何指派。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[使用者及群組的權限]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
### <a name="to-delete-model-object-permissions"></a>若要刪除模型物件權限  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  在 **[使用者]** 或 **[群組]** 頁面上，選取要編輯之使用者或群組的資料列。  
  
3.  按一下 **[編輯選取的使用者]**。  
  
4.  按一下 **[模型]** 索引標籤。  
  
5.  (選擇性) 從 **[模型]** 清單中選取模型。  
  
6.  在 [**模型許可權摘要**] 窗格中，選取您想要刪除之許可權的資料列。  
  
7.  按一下 [**刪除選取的許可權**]。  
  
    > [!NOTE]  
    >  如果權限繼承自群組，則無法從使用者移除權限。 您必須改為從群組移除權限。  
  
## <a name="see-also"></a>另請參閱  
 [模型物件使用權限 &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [指派模型物件權限 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
  
