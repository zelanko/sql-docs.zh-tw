---
title: 建立模型管理員 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], creating
ms.assetid: dae17afc-3b39-490e-b51f-2d8da26d429e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bccf908359fa0cb75a8ae0bcfe7a601ccbfd6618
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483417"
---
# <a name="create-a-model-administrator-master-data-services"></a>建立模型管理員 (Master Data Services)
  在  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]，建立模型管理員，當您希望群組或使用者擁有**更新**一或多個模型中的所有物件的權限。  
  
> [!TIP]  
>  若要簡化管理，請建立 Windows 或本機群組，然後將此群組設定為模型管理員。 然後不需存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]，您就可以在群組中加入及移除使用者。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 [使用者及群組的權限] 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
### <a name="to-create-a-model-administrator"></a>若要建立模型管理員  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  在 **[使用者]** 或 **[群組]** 頁面上，選取要編輯之使用者或群組的資料列。  
  
3.  按一下 **[編輯選取的使用者]**。  
  
4.  按一下 **[模型]** 索引標籤。  
  
5.  (選擇性) 從 **[模型]** 清單中選取模型。  
  
6.  按一下 **[編輯]**。  
  
7.  按一下您要授與權限的模型。  
  
8.  從功能表中，選取**更新**。  
  
9. 針對您希望群組或使用者成為其管理員的每個模型，完成步驟 7 和 8。  
  
10. 按一下 [儲存] 。  
  
## <a name="remarks"></a>備註  
 請不要指派模型物件或階層成員的任何其他權限。 如果您這樣做，使用者不再是系統管理員，並且無法檢視模型中的任何功能區域以外**總管**。  
  
 以下情況除外： 如果使用者擁有**更新**權限指派給階層**根**上**階層成員**索引標籤上，使用者仍然會視為一個模型系統管理員。  
  
## <a name="see-also"></a>另請參閱  
 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)   
 [指派模型物件權限 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [指派階層成員權限 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [模型物件權限 &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [階層成員權限 &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
