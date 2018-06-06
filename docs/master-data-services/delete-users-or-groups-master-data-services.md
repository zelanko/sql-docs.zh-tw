---
title: 刪除使用者或群組 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting groups [Master Data Services]
- groups [Master Data Services], deleting
- users [Master Data Services], deleting
- deleting users [Master Data Services]
ms.assetid: 0bbf9d2c-b826-48bb-8aa9-9905db6e717f
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a14e55ddf7002ab2afc32372f3aae2b6c8abd0ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="delete-users-or-groups-master-data-services"></a>刪除使用者或群組 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  當您不再希望使用者或群組存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]時，可以刪除他們。  
  
 在刪除使用者和群組時，請注意下列行為：  
  
-   如果刪除有 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]存取權之群組成員的使用者，該使用者仍然可以存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ，直到從 Active Directory 或本機群組移除使用者為止。  
  
-   如果刪除群組，群組中已存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 的所有使用者都會顯示在 **[使用者]** 清單，直到刪除使用者為止。  
  
-   對安全性的變更不會傳播至 MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 20 分鐘。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[使用者及群組的權限]** 功能區域的權限。  
  
### <a name="to-delete-users-or-groups"></a>若要刪除使用者或群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  若要刪除使用者，請停留在 **[使用者]** 頁面。 若要刪除群組，請按一下功能表列上的 [管理群組]。  
  
3.  在方格中，選取要刪除之使用者或群組的資料列。  
  
4.  按一下 **[刪除選取的使用者]** 或 **[刪除選取的群組]**。  
  
5.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [安全性 &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
