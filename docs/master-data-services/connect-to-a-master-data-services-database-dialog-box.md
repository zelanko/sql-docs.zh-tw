---
description: 連接到 Master Data Services 資料庫對話方塊
title: 連接到 MDS 資料庫對話方塊
ms.custom: seo-lt-2019
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.srvconnect.f1
ms.assetid: b2f8c9b9-c31e-4f0d-9095-978709423190
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 3d1186c3d0a5309886bf21082ac794ae1def5a01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430000"
---
# <a name="connect-to-a-master-data-services-database-dialog-box"></a>連接到 Master Data Services 資料庫對話方塊

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  使用 [連接到 Master Data Services 資料庫]**** 對話方塊來選取 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。  
  
 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中，下列頁面提供這個對話方塊：  
  
-   在 [資料庫組態]**** 頁面上，按一下 [選取資料庫]****。 使用此對話方塊來選取要進行系統設定的資料庫。  
  
-   在 [Web 組態]**** 頁面的 [建立應用程式與資料庫間的關聯]**** 底下，按一下 [選取]**** 來選取您希望與 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 網站或應用程式產生關聯的資料庫。  
  
## <a name="select-database"></a>選取資料庫  
 指定資訊來連接本機或遠端 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體，以主控 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。 若要連接到遠端執行個體，它必須先啟用遠端連接。  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**SQL Server 實例**|指定您想要主控 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 資料庫的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體名稱。 這可以是本機或遠端電腦上的預設或具名執行個體。 輸入以下項目來指定資訊：<br /><br /> 句點 (.)，可連接到您本機電腦上的預設執行個體。<br /><br /> 伺服器名稱或 IP 位址，可連接到指定之本機或遠端電腦上的預設執行個體。<br /><br /> 伺服器名稱或 IP 位址，以及連接到指定之本機或遠端電腦上具名執行個體的執行個體名稱。 以*server_name*instance_name 的格式指定此資訊 \\ * *。|  
|**驗證類型**|選取連接到指定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體時所要使用的驗證類型。 您用來連接的認證會決定顯示在 [Master Data Services 資料庫]**** 下拉式清單中的資料庫。<br /><br /> 驗證類型包括：<br /><br /> **目前使用者-整合式安全性**：使用整合式 Windows 驗證使用目前 Windows 使用者帳戶的認證來連接。 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 會使用登入電腦及開啟應用程式之使用者的 Windows 認證。 您不能在應用程式中指定不同的 Windows 認證。 如果您想要使用不同的 Windows 認證來連接，您必須以該使用者的身分登入電腦，然後開啟 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。<br /><br /> **SQL Server 帳戶**：使用 SQL Server 帳戶來連接。 當您選取這個選項時，將會啟用 [使用者名稱]**** 和 [密碼]**** 欄位，而且您必須為指定之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 帳戶指定認證。|  
|**使用者名稱**|指定將要用來連接指定之 SQL Server 執行個體的使用者帳戶名稱。 此帳戶必須屬於指定之 **執行個體上** 系統管理員 (sysadmin) [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 角色的一部分：<br /><br /> 當 [ **驗證類型** ] 為 [ **目前使用者-整合式安全性**] 時，[ **使用者名稱** ] 方塊會是唯讀的，而且會顯示登入電腦的 Windows 使用者帳戶的名稱。<br /><br /> [驗證類型]**** 為 [SQL Server 帳戶]**** 時，將會啟用 [使用者名稱]**** 方塊，而且您必須針對指定之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 帳戶指定認證。|  
|**密碼**|指定已與使用者帳戶建立關聯的密碼：<br /><br /> 當 [ **驗證類型** ] 為 [ **目前使用者-整合式安全性**] 時，[ **密碼** ] 方塊是唯讀的，而指定的 Windows 使用者帳戶的認證會用來連線。<br /><br /> [驗證類型]**** 為 [SQL Server 帳戶]**** 時，將會啟用 [密碼]**** 方塊，而且您必須指定與指定的使用者帳戶有關聯的密碼。|  
|**[連接]**|使用指定的認證連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。|  
|**Master Data Services 資料庫**|根據下列準則，在指定的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體上顯示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫：<br /><br /> 當使用者為該執行個體的 **系統管理員 (sysadmin)** 伺服器角色成員時，將會顯示該執行個體中的所有 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。<br /><br /> 當使用者為該執行個體中任何 **資料庫的** db_owner [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫角色成員時，將會顯示這些 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。<br /><br/> 如需 SQL Server 角色的詳細資訊，請參閱 [伺服器層級角色](../relational-databases/security/authentication-access/server-level-roles.md) 和 [資料庫層級角色](../relational-databases/security/authentication-access/database-level-roles.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [資料庫組態頁面 &#40;Master Data Services 組態管理員&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   

[Master Data Services 安裝和組態](../master-data-services/master-data-services-installation-and-configuration.md)
  
  
