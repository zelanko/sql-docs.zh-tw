---
title: "管理服務的安全性需求 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent service, security
- services [SQL Server], security
- SQL Server services, security
- WMI Providers [SQL Server]
- server configuration [SQL Server]
- security [SQL Server], services
- services [SQL Server], WMI
ms.assetid: 1874a317-ddb2-425d-98d9-b53e1be6fc6a
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cf5902f634cb69689388cadf26c0c53fed607519
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="security-requirements-for-managing-services"></a>管理服務的安全性需求
  若要管理 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務，請使用「SQL Server 組態管理員」或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 請使用「叢集管理員」來管理叢集伺服器的服務。  
  
 若要管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務和設定伺服器組態選項，您必須是 **伺服器管理員 (serveradmin)** 固定伺服器角色或 **系統管理員 (sysadmin)** 固定伺服器角色的成員。 Windows **Administrators** 群組的成員可以啟動和停止服務，還能設定 Windows 提供的伺服器選項。  
  
> [!NOTE]  
>  服務使用的帳戶必須設定正確的網域、檔案系統和登錄權限，才能正確運作。 如需必要權限的資訊，請參閱 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
## <a name="windows-management-instrumentation"></a>Windows Management Instrumentation  
 「SQL Server 組態管理員」與 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會使用 Windows Management Instrumentation (WMI)，來顯示和修改部份伺服器屬性。 若要管理服務和取得服務狀態，使用者必須擁有存取 WMI 物件的權限。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，以下伺服器屬性頁面會使用 WMI：  
  
-   自動啟動服務  
  
-   啟動參數  
  
-   安全性  
  
-   其他伺服器設定  
  
## <a name="related-tasks"></a>相關工作  
 [設定 WMI 在 SQL Server 工具中顯示伺服器狀態](http://msdn.microsoft.com/library/7e97197b-ed4d-40d1-9a52-9ab1d92401d7)  
  
## <a name="related-content"></a>相關內容  
 [組態管理的 WMI 提供者概念](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
