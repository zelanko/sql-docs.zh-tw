---
title: 建立模型管理員
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], creating
ms.assetid: dae17afc-3b39-490e-b51f-2d8da26d429e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1a81be69eee7a0fa8ea61b4491a296552aca51ff
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814031"
---
# <a name="create-a-model-administrator-master-data-services"></a>建立模型管理員 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  當您希望群組或使用者擁有一個或多個模型中所有物件的所有權限時，請在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中建立模型管理員。  
  
> [!TIP]  
>  若要簡化管理，請建立 Windows 或本機群組，並將它設定為模型管理員。 然後不需存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]，您就可以在群組中加入及移除使用者。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 [使用者及群組的權限]**** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-create-a-model-administrator"></a>若要建立模型管理員  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  在 **[使用者]** 或 **[群組]** 頁面上，選取要編輯之使用者或群組的資料列。  
  
3.  按一下 **[編輯選取的使用者]**。  
  
4.  按一下 **[模型]** 索引標籤。  
  
5.  (選擇性) 從 **[模型]** 清單中選取模型。  
  
6.  按一下 **[編輯]** 。  
  
7.  按一下您要授與權限的模型。  
  
8.  選取功能表上的 [管理員]****。  
  
9. 針對您希望群組或使用者成為其管理員的每個模型，完成步驟 7 和 8。  
  
10. 按一下 [檔案] 。  
  
## <a name="see-also"></a>另請參閱  
 [系統管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [指派模型物件使用權限 &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [指派階層成員許可權 &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [模型物件使用權限 &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [階層成員權限 &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
