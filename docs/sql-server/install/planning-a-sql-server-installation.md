---
title: "規劃 SQL Server 安裝 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/23/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- installing SQL Server, planning
ms.assetid: b1d56f2f-603f-48f2-b902-c715f14a6db9
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 21f4d7344c22a3426e343ff6e3682029a863369f
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="planning-a-sql-server-installation"></a>規劃 SQL Server 安裝
  若要安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請遵循以下步驟：  
  
-   檢閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的安裝需求、系統組態檢查與安全性考量。  
  
-   執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式來安裝或升級至更新版本。 升級之前，請先檢閱[升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 除非軟體的使用方式受到個別的合約 (例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 大量授權合約或與 ISV 或 OEM 簽訂的協力廠商合約) 所管制，否則不論安裝方法為何，您都必須確認以個人身分或代表實體接受軟體授權條款。  
  
 這些授權條款會顯示在安裝程式使用者介面中，供您檢閱和接受。 自動安裝 (使用 `/Q` 或 `/QS` 參數) 必須包含 `/IAcceptSQLServerLicenseTerms` 參數。 在 [Microsoft SQL Server 授權條款與資訊](http://www.microsoft.com/Licensing/product-licensing/sql-server.aspx)分別下載與檢閱授權條款。 若為大量授權條款，請參閱[授權條款與文件](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53)。 若為舊版 SQL Server，請參閱 [Microsoft 軟體授權條款](http://go.microsoft.com/fwlink/?LinkID=148209)。  
  
> [!NOTE]  
>  根據您收到本軟體的方式 (例如，透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 大量授權)，軟體的使用方式可能會受到其他條款與條件的限制。  
  
## <a name="in-this-section"></a>本節內容  
 [SQL Server 安裝的新增功能](../../sql-server/install/what-s-new-in-sql-server-installation.md)  
 本主題描述有關這一版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中新增或改進安裝功能的詳細資料。  
  
 [安裝 SQL Server 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
 本主題列出安裝和執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體的最低軟硬體需求。  
  
 [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 本主題說明您在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前及安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之後應該考慮的一些安全性最佳做法。  
  
 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
 本主題描述此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本的預設服務組態，以及可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間和安裝完成後設定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務組態選項。  
  
 [網路通訊協定和網路程式庫](../../sql-server/install/network-protocols-and-network-libraries.md)  
 本主題描述這一版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中網路通訊協定的預設組態，以及可用的組態選項。  
  
 [使用 SQL Server 的多個版本和執行個體](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
 本主題描述安裝多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本及執行個體的考量。  
  
 [SQL Server 中的地區語言版本](../../sql-server/install/local-language-versions-in-sql-server.md)  
 本主題描述有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的當地語系化版本。  
  
## <a name="related-sections"></a>相關章節  
 [安裝 SQL Server](../../database-engine/install-windows/install-sql-server.md)  
 本節提供可以用於安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之不同安裝選項的概觀。  
  
 [安裝 SQL Server Business Intelligence 功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件集的這一節說明如何安裝屬於 Microsoft BI 平台一部分的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。  
  
 [升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
 本節提供將舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的概觀。  
  
 [將 SQL Server 解除安裝](../../sql-server/install/uninstall-sql-server.md)  
 請參閱本節完整解除安裝現存的 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 執行個體，並將系統準備好重新安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 [SQL Server 容錯移轉叢集安裝](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件集中的這一節將說明如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集。  
  
## <a name="see-also"></a>另請參閱  
 [從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [高可用性解決方案 &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [安裝容錯移轉叢集之前](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)   
 [使用安裝精靈升級 SQL Server &#40;安裝程式&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  

