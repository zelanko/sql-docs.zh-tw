---
title: "SQL Server 安裝 | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: 095a3d6d9fd7f16b337136f564fea18160b8636c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/08/2017

---
# <a name="sql-server-installation"></a>SQL Server 安裝

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈提供了安裝所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的單一功能樹狀目錄：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
-   連接元件  
  
從 [!INCLUDE[ss2016](../../includes/sssql15-md.md)] 開始，SQL Server 管理工具已不再從主要功能樹狀目錄中安裝。如需詳細資料，請參閱[下載 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。  
  
您可以個別安裝每個元件，也可以選取上面所列出元件的組合。 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的可用版本與元件之間做出最佳選擇，請參閱 SQL Server 版本所支援的功能：

- [[!INCLUDE[ss2017](../../includes/sssqlv14-md.md)] 的版本和支援的功能](~/sql-server/editions-and-components-of-sql-server-2017.md).  
- [[!INCLUDE[ss2016](../../includes/sssql15-md.md)] 的版本和支援的功能](~/sql-server/editions-and-components-of-sql-server-2016.md).  
- [[!INCLUDE[ss2014](../../includes/sssql14-md.md)] 的版本和支援的功能](http://technet.microsoft.com/library/cc645993(v=sql.120).aspx)
  
## <a name="in-this-section"></a>本節內容  
不論您是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元來安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，安裝程序都包括下列步驟：  
  
[規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)  
描述如何準備您的電腦安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]：  
  
-   硬體及軟體需求。  
-   系統組態檢查需求和封鎖問題。  
-   安全性考量。  
  
[安裝 SQL Server](../../database-engine/install-windows/install-sql-server.md)  
 說明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的安裝選項。  
  
[SQL Server 安裝程式使用者介面參考](http://msdn.microsoft.com/library/183b5cdd-962e-41ca-8064-ea44f622c77d)  
 描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈所顯示的安裝選項。  
  
[升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
 說明用以升級至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的選項。  
  
[將 SQL Server 解除安裝](../../sql-server/install/uninstall-sql-server.md)  
 說明解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]的程序。  
  
[SQL Server 容錯移轉叢集安裝](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件集中的這一節將說明如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集。  
  
[安裝 SQL Server Business Intelligence 功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 屬於 Microsoft BI 平台的功能包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，以及用來建立或處理分析資料的數種用戶端應用程式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件中的這一節將說明如何安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
## <a name="more-information"></a>其他資訊
[安裝具有 SharePoint 的 SQL Server BI 功能 &#40;PowerPivot 和 Reporting Services&#41;](http://msdn.microsoft.com/library/3166107c-30c2-468e-bb1b-bb42b79b37c3)  
 本節說明如何在 SharePoint 環境中安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能， 同時也會列出特定版本 SharePoint 能使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 除此之外還會提供 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 及 SharePoint 模式下的 Reporting Services 安裝程序。  
  
![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) 安裝新的範例資料庫， [Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)。 
  
[其他 SQL Server 範例和範例資料庫](http://sqlserversamples.codeplex.com/)  
 描述如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 範例與範例資料庫。  
  
請參閱 [SQL Server 更新中心](https://msdn.microsoft.com/library/ff803383.aspx) 連結和資訊，所有支援的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]版本。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server 安裝的新增功能](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
[安裝 SQL Server 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
