---
title: 建立版本旗標
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating version flags [Master Data Services]
- version flags [Master Data Services], creating
- versions [Master Data Services], creating flags
ms.assetid: 3067e1e3-05b7-4f11-9206-c612ef4e7e42
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 373e915a2a0a2c75894698df943b0d8a3df955c9
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812732"
---
# <a name="create-a-version-flag-master-data-services"></a>建立版本旗標 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，建立要指派給版本的版本旗標。 此旗標可以指出使用者或訂閱系統應該使用的版本。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[版本管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
-   您必須擁有存取 [版本管理] 功能區域的權限。 如需詳細資訊，請參閱[功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
### <a name="to-create-a-version-flag"></a>若要建立版本旗標  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[版本管理]**。  
  
2.  在 **[管理版本]** 頁面上，從功能表列指向 **[管理]** ，然後按一下 **[旗標]**。  
  
3.  在 **[管理版本旗標]** 頁面上，從 **[模型]** 欄位選取您要建立旗標的模型。  
  
4.  按一下 **[新增]** 。  
  
5.  在 **[名稱]** 方塊中，輸入名稱。  
  
6.  在 **[描述]** 方塊中，輸入描述。  
  
7.  在 **[僅限認可的版本]** 欄位中，選取 **[True]** 表示旗標只能指派給狀態為 **[已認可]** 的版本。 選取 **[False]** 表示旗標可以指派給任何狀態的版本。  
  
8.  按一下 [檔案] 。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [將旗標指派給版本 &#40;Master Data Services&#41;](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [版本 &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [變更版本旗標名稱 &#40;Master Data Services&#41;](../master-data-services/change-a-version-flag-name-master-data-services.md)  
  
  
