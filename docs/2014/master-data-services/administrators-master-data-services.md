---
title: 管理員 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], about administrators
- administrators [Master Data Services]
- models [Master Data Services], administrators
ms.assetid: d330aa4e-6ade-4b09-b376-1b15d6c78f7d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c47d1905602f5cd96b58265963072cdd2dc01939
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52778240"
---
# <a name="administrators-master-data-services"></a>管理員 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中，有兩種管理員類型：模型管理員及 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 系統管理員。  
  
## <a name="model-administrators"></a>模型管理員  
 在 [ [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]，模型管理員是具有的使用者**更新**上指派的最上層模型物件權限**模型物件**] 索引標籤上，而且沒有其他指派權限。  
  
-   如果使用者可以存取總管 功能區域，即可加入、刪除及更新此區域中的所有主要資料。  
  
-   如果使用者可以存取其他功能區域，即可執行該功能區域中的所有管理工作。  
  
 每個模型可以有多個管理員。 每個使用者都可以是 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 部署中一個、數個或所有模型的模型管理員。  
  
 使用者可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中或透過程式設計方式設定為模型管理員。 如需詳細資訊，請參閱 [建立模型管理員 &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md)。  
  
## <a name="master-data-services-system-administrator"></a>Master Data Services 系統管理員  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 系統管理員只有一個。 系統管理員會為指定的使用者**系統管理員帳戶**當您建立[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]資料庫。  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 系統管理員：  
  
-   自動擁有所有功能區域的存取權。  
  
-   可以新增、 刪除和更新所有模型中的所有主要資料**總管**功能區域。  
  
 您可以變更指定為系統管理員的使用者。 如需詳細資訊，請參閱 <<c0> [ 變更系統管理員帳戶&#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)。</c0>  
  
## <a name="comparing-administrator-types"></a>比較管理員類型  
  
|管理員類型|描述|  
|------------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 系統管理員|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中所指派權限不會影響系統管理員的存取。<br /><br /> 自動擁有**更新**所有模型的權限。<br /><br /> 自動擁有所有功能區域的存取權。<br /><br /> 在 mdm.tblUser 中的值**識別碼**資料行是**1**。|  
|模型管理員|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中指派的權限會決定使用者是否為模型管理員。<br /><br /> 根據明確指派的權限或繼承自群組的權限，使用者可以是模型管理員。<br /><br /> 只有具有模型的系統管理員**更新**指派給最上層模型物件權限並沒有其他權限。<br /><br /> 只能存取被授與存取權的功能區域。<br /><br /> 在 mdm.tblUser 中的值**識別碼**資料行不是**1**。|  
  
## <a name="see-also"></a>另請參閱  
 [建立模型管理員 &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md)   
 [變更系統管理員帳戶&#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)   
 [建立 Master Data Services 資料庫](install-windows/create-a-master-data-services-database.md)   
 [通知 &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)  
  
  
