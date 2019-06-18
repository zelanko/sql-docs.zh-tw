---
title: SSRS 服務應用程式的佈建訂用帳戶及警示 | Microsoft Docs
ms.date: 06/03/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Shared Service
- SharePoint Mode [Reporting Services]
- SharePoint Mode
- Reporting Services Service Application
- SSRS service application
ms.assetid: d0de3f1f-4887-47fb-bacf-46aaad74c4be
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ef70b3430cc1028b7486bf663280cfcf740d9290
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651950"
---
# <a name="provision-subscriptions-and-alerts-for-ssrs-service-applications"></a>SSRS 服務應用程式的佈建訂閱及警示
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱和資料警示需要 SQL Server Agent，並且需要 SQL Server Agent 的權限組態。 如果您看到錯誤訊息指出需要 SQL Server Agent，而您已確認 SQL Server Agent 正在執行，則請更新或驗證權限。 本主題的範圍是 SharePoint 模式的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，且本主題說明三種可以用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱來更新 SQL Server Agent 權限的方法。 在本主題中用來執行步驟的認證必須要有足夠的權限，才能針對服務應用程式、msdb 和 master 資料庫中的物件授與 RSExecRole 的執行權限。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2016 &#124; SharePoint 2013|  
  
 ![服務應用程式資料庫的 SQL Agent 權限](../../reporting-services/install-windows/media/rs-provisionsqlagent.gif "服務應用程式資料庫的 SQL Agent 權限")  
  
||Description|  
|------|-----------------|  
|**1**|主控 Reporting Services 服務應用程式資料庫的 SQL Server Database Engine 執行個體。|  
|**2**|SQL Database Engine 執行個體的 SQL Server Agent 執行個體。|  
|**3**|Reporting Services 服務應用程式資料庫。 這些名稱會以用於建立服務應用程式的資訊為基礎。 以下是範例資料庫名稱：<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0_Alerting<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0TempDB|  
|**4**|SQL Server Database Engine 執行個體的 master 和 MSDB 資料庫。|  
  
 使用下列三種方法之一來更新權限：  
  
1.  從 [條款、訂閱和警示]  頁面上鍵入認證，然後按一下 [確定]  。  
  
2.  從 [提供訂閱和警示] 頁面按一下 [下載指令碼]  按鈕，下載可用來設定權限的 Transact SQL 指令碼。  
  
3.  執行 PowerShell Cmdlet，以建立可用來設定權限的 Transact-SQL 指令碼。  
  
### <a name="to-update-permissions-using-the-provision-page"></a>若要使用佈建頁面更新權限  
  
1.  從 SharePoint 管理中心，按一下 [應用程式管理]  群組中的 [管理服務應用程式]  。  
  
2.  在清單中尋找服務應用程式，並按一下應用程式的名稱，或按一下 [類型]  欄選取服務應用程式，然後按一下 SharePoint 功能區中的 [管理]  按鈕。  
  
3.  在 [管理 Reporting Services 應用程式]  頁面上，按一下 [提供訂閱和警示]  。  
  
4.  如果 SharePoint 管理員對 Master 資料庫和服務應用程式資料庫有足夠的權限，請輸入這些認證。  
  
5.  按一下 [確定]  按鈕。  
  
##  <a name="bkmk_download"></a> 下載 Transact-SQL 指令碼  
  
1.  從 SharePoint 管理中心，按一下 [應用程式管理]  群組中的 [管理服務應用程式]  。  
  
2.  在清單中尋找服務應用程式，並按一下應用程式的名稱，或按一下 [類型]  欄選取服務應用程式，然後按一下 SharePoint 功能區中的 [管理]  按鈕。  
  
3.  在 [管理 Reporting Services 應用程式]  頁面上，按一下 [提供訂閱和警示]  。  
  
4.  在 [檢視狀態]  區域中，確認 SQL Server Agent 正在執行。  
  
5.  按一下 [下載指令碼]  ，下載您可以在 SQL Server Management Studio 中執行以授與權限的 Transact-SQL 指令碼。 建立的指令碼檔案名稱會包含 Reporting Services 服務應用程式的名稱，例如 **[服務應用程式的名稱]-GrantRights.sql**。  
  
### <a name="to-generate-the-transact-sql-statement-with-powershell"></a>使用 PowerShell 產生 Transact-SQL 陳述式  
  
1.  您也可以在 SharePoint 2016 或 SharePoint 2013 管理介面中使用 Windows PowerShell Cmdlet 建立 Transact-SQL 指令碼。  
  
2.  在 [開始]  功能表上，按一下 [所有程式]  。  
  
3.  展開 [Microsoft SharePoint 2016 產品]  ，然後按一下 [SharePoint 2016 管理命令介面]  。
  
4.  透過取代報表伺服器資料庫的名稱、應用程式集區帳戶及陳述式的路徑，來更新下列 PowerShell Cmdlet。  
  
     **Cmdlet 的語法：** `Get-SPRSDatabaseRightsScript -DatabaseName <ReportingServices database name> -UserName <app pool account> -IsWindowsUser | Out-File <path of statement>`  
  
     **範例 Cmdlet：** `Get-SPRSDatabaseRightsScript -DatabaseName ReportingService_46fd00359f894b828907b254e3f6257c -UserName "NT AUTHORITY\NETWORK SERVICE" -IsWindowsUser | Out-File c:\SQLServerAgentrights.sql`  
  
## <a name="using-the-transact-sql-script"></a>使用 Transact-SQL 指令碼  
 下列程序可搭配從佈建頁面下載的指令碼，或透過 PowerShell 建立的指令碼使用。  
  
#### <a name="to-load-the-transact-sql-script-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中載入 Transact-SQL 指令碼  
  
1.  若要開啟 SQL Server Management Studio，請在 [開始]  功能表上，按一下 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]，然後按一下 [SQL Server Management Studio]  。  
  
2.  在 [連接到伺服器]  對話方塊上，設定下列選項：  
  
    -   在 [伺服器類型]  清單中，選取 [資料庫引擎]   
  
    -   在 [伺服器名稱]  中，鍵入您要設定 SQL Server Agent 的 SQL Server 執行個體名稱。  
  
    -   選取驗證模式。  
  
    -   如果使用 SQL Server 驗證連接，請提供登入和密碼。  
  
3.  按一下 **[連接]** 。  
  
#### <a name="to-run-the-transact-sql-statement"></a>執行 Transact-SQL 陳述式  
  
1.  在 SQL Server Management Studio 的工具列上，按一下 [新增查詢]  。  
  
2.  在 [檔案]  功能表上，按一下 [開啟]  ，然後按一下 [檔案]  。  
  
3.  瀏覽至您在 SharePoint 2016 或 SharePoint 2013 管理介面中產生之 Transact-SQL 陳述式的儲存所在資料夾。  
  
4.  按一下檔案，然後按一下 [開啟]  。  
  
     陳述式隨即會加入查詢視窗。  
  
5.  按一下 **[執行]** 。  
  
  
