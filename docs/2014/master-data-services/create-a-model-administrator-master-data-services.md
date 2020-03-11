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
ms.openlocfilehash: 464e82ea23aa724d84af25c69a7168f95d09afe1
ms.sourcegitcommit: 39d8d2d504d0ab70bac5ae3e981657e15dfb7bee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/10/2020
ms.locfileid: "78964363"
---
# <a name="create-a-model-administrator-master-data-services"></a>建立模型管理員 (Master Data Services)
  當[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]您希望群組或使用者擁有一或多個模型中所有物件的 [**更新**] 許可權時，可以在中建立模型管理員。  
  
> [!TIP]  
>  若要簡化管理，請建立 Windows 或本機群組，並將它設定為模型管理員。 然後不需存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]，您就可以在群組中加入及移除使用者。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 [使用者及群組的權限]**** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
### <a name="to-create-a-model-administrator"></a>若要建立模型管理員  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  在 **[使用者]** 或 **[群組]** 頁面上，選取要編輯之使用者或群組的資料列。  
  
3.  按一下 **[編輯選取的使用者]**。  
  
4.  按一下 **[模型]** 索引標籤。  
  
5.  (選擇性) 從 **[模型]** 清單中選取模型。  
  
6.  按一下 **[編輯]**。  
  
7.  按一下您要授與權限的模型。  
  
8.  從功能表中，選取 [**更新**]。  
  
9. 針對您希望群組或使用者成為其管理員的每個模型，完成步驟 7 和 8。  
  
10. 按一下 [檔案]  。  
  
## <a name="remarks"></a>備註  
 請不要指派模型物件或階層成員的任何其他權限。 如果您這樣做，使用者就不再是系統管理員，也無法在**Explorer**以外的任何功能區域中查看模型。  
  
 有一個例外狀況：如果使用者在 [階層**成員**] 索引標籤上，將 [**更新**] 許可權指派給階層**根**，則使用者仍然會被視為模型管理員。  
  
## <a name="see-also"></a>另請參閱  
 [系統管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)   
 [指派模型物件使用權限 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [指派階層成員許可權 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [模型物件使用權限 &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [階層成員許可權 &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
