---
title: SQL Server 2014 的安裝 |Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- sql12.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 96afef098b711c65e1bcb46d5f687c95061f2c94
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228405"
---
# <a name="installation-for-sql-server-2014"></a>SQL Server 2014 安裝
 ## <a name="download-sql-server-2014-expresshttpwwwhanselmancomblogdownloadsqlserverexpressaspx"></a>[下載 SQL Server 2014 Express](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **感謝[Scott Hanselman](http://www.hanselman.com/)在一處收集所有安裝程式套件連結！**
  
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈提供了安裝所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的單一功能樹狀目錄：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
  
-   管理工具  
  
-   連接元件  
  
 您可以個別安裝每個元件，也可以選取上面所列出元件的組合。 若要在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供的版本和元件之間做出最佳選擇，請參閱[SQL Server 2014 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2016.md)和[SQL Server 2014 版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 有 32 位元和 64 位元兩種版本。
 
 **試試看：**  
  
-   有 Azure 帳戶嗎？  然後前往**[這裡](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)** 來加速已安裝 SQL Server 2014 Service Pack 1 （SP1）的虛擬機器。 如需 SQL Server 2014 （SP1）的詳細資訊，請參閱[SQL Server 2014 Service Pack 1 版本資訊](https://support.microsoft.com/kb/3058865)。  
  
## <a name="in-this-section"></a>本節內容  
 不論您是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元來安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，安裝程序都包括下列步驟：  
  
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)  
 描述如何準備您的電腦安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]：  
  
-   硬體及軟體需求。  
  
-   系統組態檢查需求和封鎖問題。  
  
-   安全性考量。  
  
 [安裝 SQL Server 2014](install-sql-server.md)  
 說明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的安裝選項。  
  
 [升級至 SQL Server 2014](upgrade-sql-server.md)  
 說明用以升級至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的選項。  
  
 [卸載 SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)  
 說明解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]的程序。  
  
 [SQL Server 容錯移轉叢集安裝](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件集中的這一節將說明如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集。  
  
 [安裝 SQL Server 2014 BI 功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 屬於 Microsoft BI 平台的功能包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，以及用來建立或處理分析資料的數種用戶端應用程式。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件中的這一節將說明如何安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
## <a name="related-sections"></a>相關章節  
 [安裝 how to 主題](../../sql-server/install/installation-how-to-topics.md)  
 提供如何從安裝精靈、從命令提示字元、使用組態檔及使用 SysPrep 安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的程序性主題連結。  
  
 [安裝 SharePoint &#40;PowerPivot 和 Reporting Services 的 SQL Server BI 功能&#41;](../../sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)  
 本節說明如何在 SharePoint 環境中安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能， 同時也會列出特定版本 SharePoint 能使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 除此之外還會提供 PowerPivot for SharePoint 及 SharePoint 模式下的 Reporting Services 安裝程序。  
  
 [安裝 SQL Server 範例和範例資料庫](https://sqlserversamples.codeplex.com/)  
 描述如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 範例與範例資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 安裝的新功能](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
 [安裝 SQL Server 2014 的硬體和軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
