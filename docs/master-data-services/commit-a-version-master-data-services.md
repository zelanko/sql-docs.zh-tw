---
title: 認可版本
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- committing versions [Master Data Services]
- versions [Master Data Services], committing
ms.assetid: 6b967a39-b333-4b84-9e5f-4fb07e156826
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d5cb3ebca4ab30fdf17b40774d50f44942cba093
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812433"
---
# <a name="commit-a-version-master-data-services"></a>認可版本 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可認可模型版本，以防止模型成員及其屬性的變更。 已認可的版本無法解除鎖定。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[版本管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
-   版本的狀態必須是 [已鎖定]****。 如需詳細資訊，請參閱 [鎖定版本 &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)(管理員 (Master Data Services))。  
  
-   所有成員必須都已驗證成功。  
  
-   您必須擁有存取 [版本管理] 功能區域的權限。 如需詳細資訊，請參閱[功能區域權限 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
### <a name="to-commit-a-version"></a>若要認可版本  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[版本管理]**。  
  
2.  在 [管理版本]**** 頁面上，按一下功能表列上的 [驗證版本]****。  
  
3.  在 [驗證版本]**** 頁面上，選取要認可的模型和版本。  
  
4.  按一下 [認可]****。  
  
5.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [建立版本旗標 &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)  
  
-   [將旗標指派給版本 &#40;Master Data Services&#41;](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
-   [複製版本 &#40;Master Data Services&#41;](../master-data-services/copy-a-version-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [版本 &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
  
