---
title: 硬體和軟體需求的 Reporting Services SharePoint 模式 |Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ed91877d-4f74-4266-a932-b824b4810c99
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5b70a6a736d9a7f566eb4aa60a37ed7b5151168e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63295414"
---
# <a name="hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode"></a>SharePoint 模式的 Reporting Services 之硬體和軟體需求

  本主題描述以 SharePoint 模式執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的必要條件、硬體需求和安裝考量。 由於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式需要 SharePoint 伺服器，因此大部分需求都是以 SharePoint 環境為基礎。 若是原生模式報表伺服器，您的硬體應符合執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的最低硬體和軟體需求。 如需詳細資訊，請參閱＜ [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)＞。  
  
-   [必要條件](#bkmk_prereq)  
  
-   [報表伺服器資料庫需求](#bkmk_report_server_database)  
  
-   [Power View 需求](#bkmk_powerview)  
  
-   [詳細資訊](#bkmk_more_information)  
  
##  <a name="bkmk_prereq"></a> 必要條件  
  
-   若為本機安裝，在 SharePoint 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝時登入的帳戶必須是本機作業系統中系統管理員群組的成員。 安裝程式帳戶不必是 SharePoint 伺服器陣列管理員群組的成員。  
  
     如需詳細資訊，請參閱 [SharePoint 2013 中的帳戶權限及安全性設定](https://technet.microsoft.com/library/cc678863.aspx)。  
  
-   以 SharePoint 模式執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 需要 SharePoint Server。 如需有關 SharePoint 需求和組態的詳細資訊，請參閱下列主題：  
  
    -   [硬體和軟體需求 (SharePoint 2013)](https://go.microsoft.com/fwlink/p/?LinkId=256365) (https://go.microsoft.com/fwlink/p/?LinkId=256365)  
  
    -   [SharePoint Server 2013 的容量管理和調整大小](https://technet.microsoft.com/library/cc261700.aspx)  
  
    -   [商業智慧的軟體需求 (SharePoint 2013)](https://go.microsoft.com/fwlink/p/?LinkId=256367)  
  
    -   [硬體和軟體需求 (SharePoint Server 2010)](https://technet.microsoft.com/library/cc262485\(v=office.14\))  
  
    -   [SharePoint Server 2010 的容量管理和調整大小](https://technet.microsoft.com/library/cc261700.aspx\(v=office.14\))  
  
-   如果您要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 升級或更新現有的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]SharePoint 安裝，請參閱＜ [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)的最低硬體和軟體需求。  
  
-   確認已在 Windows 伺服器管理員中啟動 **[SharePoint 2013 Administration]** 服務。  
  
###  <a name="bkmk_report_server_database"></a> 報表伺服器資料庫需求  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 SharePoint 產品及技術都使用 SQL Server 關聯式資料庫儲存應用程式資料。  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 需要相容 SQL Server 版本的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體。 如需有關硬體和軟體需求的詳細資訊，請參閱＜ [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)＞。  
  
-   SharePoint 產品可以使用現有的資料庫執行個體。 如果沒有安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，SharePoint 產品安裝程式會安裝 SQL Server Express Edition 做為 SharePoint 應用程式資料庫。  
  
-   報表伺服器執行個體無法使用 SQL Server Express Edition 做為其資料庫； 但是，由 SharePoint 產品所安裝的 SQL Server Express Edition 執行個體可以與其他 Database Engine 版本並存。  
  
##  <a name="bkmk_powerview"></a> [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 需求

 請檢閱 Office.Microsoft.com 上最新的 [Power View 文件集](http://office.microsoft.com/excel-help/power-view-explore-visualize-and-present-your-data-HA102835634.aspx) 。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 是 Microsoft Excel 2013 的一項功能，而且屬於適用於 Microsoft SharePoint Server 2010 和 2013 Enterprise 版之 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services 增益集的一部分。  
  
##  <a name="bkmk_more_information"></a> 其他資訊

 如需 SharePoint 變更的詳細資訊，請參閱[SharePoint 2013 會從 SharePoint 2010 變成](https://technet.microsoft.com/library/ff607742\(office.15\).aspx)(https://technet.microsoft.com/library/ff607742(office.15).aspx)。  
  
 [SQL Server 2014 版本資訊](https://go.microsoft.com/fwlink/?LinkID=296445)。  
  
  
