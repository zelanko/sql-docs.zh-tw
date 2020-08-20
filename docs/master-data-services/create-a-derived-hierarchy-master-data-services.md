---
description: 建立衍生階層 (Master Data Services)
title: 建立衍生階層
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies, creating
- creating derived hierarchies [Master Data Services]
ms.assetid: fec653c4-11cc-46a2-8dd8-b605341ebb40
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4ada9791d75d273bd28c516019be8cf9e7ce1088
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461880"
---
# <a name="create-a-derived-hierarchy-master-data-services"></a>建立衍生階層 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  當您需要以層級為基礎的階層，確保成員存在於正確層級時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中建立衍生階層。 衍生階層是以模型中存在的網域屬性關聯性為基礎。  
  
> [!NOTE]  
>  如果成員沒有網域屬性值，衍生階層中不會包含此成員。 若需要求所有成員的網域屬性值，請參閱[要求屬性值 &#40;Master Data Services&#41;](../master-data-services/require-attribute-values-master-data-services.md)。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-create-a-derived-hierarchy"></a>若要建立衍生階層  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列指向 [管理]****，然後按一下 [衍生階層]****。  
  
3.  在 [衍生階層維護]**** 頁面上，選取 [模型]**** 清單中的模型。  
  
4.  按一下 [新增] 。  
  
5.  在 [加入衍生階層]**** 頁面上的 [衍生階層名稱]**** 方塊中，輸入階層的名稱。  
  
    > [!TIP]  
    >  請使用名稱來描述階層中的層級，例如 **產品到子類別目錄到類別目錄**。  
  
6.  按一下 [儲存衍生階層]****。  
  
7.  在 [編輯衍生階層]**** 頁面上，按一下 [可用的實體和階層]**** 窗格中的實體或階層，並將它拖曳至 [目前層級]**** 窗格中的 [在此放置父系]****。  
  
8.  繼續拖曳實體或階層，直到完成階層為止。  
  
9. 按一下 [上一步]****。  
  
## <a name="see-also"></a>另請參閱  
 [衍生階層 &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)   
 [具有明確 Caps &#40;Master Data Services&#41;的衍生階層 ](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [網域屬性 &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)  
  
  
