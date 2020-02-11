---
title: 將旗標指派給版本
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- version flags [Master Data Services], assigning flags
- versions [Master Data Services], assigning flags
ms.assetid: 6629ec7e-32e7-4a1e-8b31-eb43c5923766
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4e8f69d473ff15be3105c8dcef5f51edf30f4302
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73729786"
---
# <a name="assign-a-flag-to-a-version-master-data-services"></a>將旗標指派給版本 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，將旗標指派給版本，指出使用者或訂閱系統應該使用的版本。  
  
> [!NOTE]  
>  版本旗標一次只能指派給一個版本。 如果指派的旗標已指派給另一個版本，該旗標會移至選取的版本。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[版本管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   您必須已建立要指派的版本旗標。 如需詳細資訊，請參閱 [建立版本旗標 &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)(管理員 (Master Data Services))。  
  
-   您必須具有存取 [版本管理] 功能區域的權限。 如需詳細資訊，請參閱[功能區域許可權 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
### <a name="to-assign-a-flag-to-a-version"></a>若要將旗標指派給版本  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[版本管理]**。  
  
2.  在 [管理版本]**** 頁面上，於您要指派旗標之版本的資料列，按兩下 [旗標]**** 資料行中的資料格。  
  
3.  從清單中選取您要指派的旗標。  
  
    > [!NOTE]  
    >  如果您要的旗標無法使用，此旗標可能只適用於 [已認可]**** 版本。 若要確認，請移至 [管理版本旗標]**** 頁面並檢視旗標的 [僅限認可的版本]**** 欄位。  
  
4.  按下 ENTER 鍵儲存變更。  
  
## <a name="see-also"></a>另請參閱  
 [建立 &#40;Master Data Services 的版本旗標&#41;](../master-data-services/create-a-version-flag-master-data-services.md)   
 [版本 &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
  
