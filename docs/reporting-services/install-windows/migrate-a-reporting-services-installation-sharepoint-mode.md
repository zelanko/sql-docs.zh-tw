---
title: "移轉 Reporting Services 安裝 （SharePoint 模式） |Microsoft 文件"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 61290949-690a-4e19-b078-57c99b6b30fa
caps.latest.revision: 23
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 75bce56e88ef80a33d13e188ad0ecbf3e8b453ec
ms.contentlocale: zh-tw
ms.lasthandoff: 08/17/2017

---

# <a name="migrate-a-reporting-services-installation-sharepoint-mode"></a>移轉 Reporting Services 安裝 (SharePoint 模式)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  本主題概述將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式部署從一個 SharePoint 環境移轉至另一個 SharePoint 環境所需的步驟。 特定的步驟可能會因為您移轉的來源版本而有所不同。 如需有關 SharePoint 模式升級及移轉案例的詳細資訊，請參閱＜ [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)＞。 如果您只是要將報表項目從某部伺服器複製到另一部，請參閱 [在報表伺服器之間複製內容的範例 Reporting Services rs.exe 指令碼](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)。  
  
 如需移轉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式部署的資訊，請參閱 [移轉 Reporting Services 安裝 &#40;原生模式&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)＞。  
  
 執行移轉的一個常見原因，是因為您想要將 SharePoint 2010 部署升級至 SharePoint 2013/2016。 SharePoint 2013/2016 不支援從 SharePoint 2010 執行就地升級，您必須完成 **資料庫附加升級** 程序，或是僅限內容移轉。  
  
 如需升級 SharePoint 2013/2016 的詳細資訊，請參閱下列主題：  

-   [升級到 SharePoint 2016 的程序概觀](https://technet.microsoft.com/library/cc262483\(v=office.16\))。

-   [升級到 SharePoint 2013 的程序概觀](http://go.microsoft.com/fwlink/p/?LinkId=256688)。
  
-   [升級到 SharePoint 2013 之前的清除準備工作](http://go.microsoft.com/fwlink/p/?LinkId=256689)。  
  
-   [將資料庫從 SharePoint 2013 升級到 SharePoint 2016](https://technet.microsoft.com/library/cc303436\(v=office.16\))。

-   [將資料庫從 SharePoint 2010 升級到 SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690)。
  
-   [在 SharePoint 2016 中移動內容資料庫](https://technet.microsoft.com/library/cc262792\(v=office.16\).aspx)。

-   [在 SharePoint 2013 中移動內容資料庫](http://technet.microsoft.com/library/cc262792.aspx)。
  
##  <a name="bkmk_prior_versions"></a> 從 SQL Server 2012 之前的 Reporting Services SharePoint 模式版本移轉  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中變更的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SharePoint 模式架構，包括服務應用程式資料庫結構描述。 如果您想要移轉至[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]從之前的版本的 SharePoint 模式[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，先安裝 SharePoint 和 SQL Server 2016 Reporting Services SharePoint 模式中建立新的 SharePoint 環境。 如需詳細資訊，請參閱 [安裝 Reporting Services SharePoint 模式](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。  
  
 新的 SharePoint 環境開始執行之後，可以在包含內容資料庫的資料庫層級選擇僅限內容移轉或完整移轉。  
  
###  <a name="bkmk_content_only_migration"></a> 僅限內容移轉  
 **Reporting Services 僅限內容移轉：** 若要將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 內容複製到新的伺服器陣列，您需要使用類似 **rs.exe** 的工具將內容複製到新的 SharePoint 安裝。 如需有關僅限內容移轉的詳細資訊，請參閱以下主題：  
  
-   **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] RSS 指令碼：** 這些指令碼可以在原生模式與 SharePoint 模式報表伺服器之間移轉內容及資源。 如需詳細資訊，請參閱 [在報表伺服器之間複製內容的範例 Reporting Services rs.exe 指令碼](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md) 和 [Reporting Services RS.exe script migrates content](http://azuresql.codeplex.com/releases/view/115207)(可移轉內容的 Reporting Services RS.exe 指令碼)。  
  
-   **Reporting Services 移轉工具：** 此工具可以將報表項目從原生模式伺服器複製到 SharePoint 模式伺服器。 如需詳細資訊，請參閱 [Reporting Services 移轉工具](http://www.microsoft.com/download/details.aspx?id=29560) (http://www.microsoft.com/download/details.aspx?id=29560)。  
  
###  <a name="bkmk_full_migration"></a> 完整移轉  
 **完整移轉：** 若要隨 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 目錄資料庫一併將 SharePoint 內容資料庫 移轉到新的伺服器陣列，可以執行本主題摘錄的一系列備份及還原選項。 在某些情況下，還原階段所使用的工具必須與備份階段所使用的工具不同。 例如，您可以使用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]組態管理員來備份加密金鑰從舊版的[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]但您需要使用 SharePoint 管理中心或 PowerShell 將加密金鑰還原到 SQL Server 2016 Reporting Services SharePoint 模式安裝。  
  
####  <a name="bkmk_databases"></a> 完成的移轉中將會看到的資料庫  
 下表描述在您成功移轉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 安裝之後，與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 相關的 SQL Server 資料庫：  
  
|資料庫|範例名稱||  
|--------------|------------------|-|  
|目錄資料庫|ReportingService_ [服務應用程式 GUID] **(\*)**|使用者移轉。|  
|暫存資料庫|ReportingService_ [服務應用程式 GUID] TempDB **(\*)**|使用者移轉。|  
|警示資料庫|ReportingService_[服務應用程式 GUID]_Alerting|在建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式時建立。|  
  
 **(\*)**表所示的範例名稱會遵循當您建立新的 SSRS 服務應用程式時，會使用 SSRS 的命名慣例。 如果您從不同的伺服器移轉，您的目錄和 tempDB 所擁有的名稱將會來自原始安裝。  
  
####  <a name="bkmk_backup_operations"></a> 備份作業  
 本節描述您需要移轉的資訊類型，以及完成備份所使用的工具或程序。  
  
 ![SSRS SharePoint 移轉的基本圖表](../../reporting-services/install-windows/media/rs-sharepoint-migration.gif "SSRS SharePoint 移轉的基本圖表")  
  
||物件|方法|注意|  
|-|-------------|------------|-----------|  
|**1**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密金鑰。|**Rskeymgmt.exe** 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員。 請參閱 [備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。|所指的工具可用於備份，但是在還原作業中，您將使用 Reporting Services [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式管理頁面或 PowerShell。|  
|**2**|SharePoint 內容資料庫。||備份資料庫，並卸離資料庫。<br /><br /> 請參閱 [決定升級方法 (SharePoint Server 2010) (http://technet.microsoft.com/library/cc263447.aspx)](http://technet.microsoft.com/library/cc263447.aspx)中的＜資料庫附加升級＞一節。|  
|**3**|屬於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]目錄資料庫的 SQL Server 資料庫。|SQL Server 資料庫備份和還原<br /><br /> 或<br /><br /> SQL Server 資料庫卸離和附加。||  
|**4**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態檔。|簡單檔案複製。|只有當您對 rsreportserver.config 做了自訂之後，才需要複製這個檔案。 檔案的範例預設位置如下：C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting\\*：<br /><br /> <br /><br /> Rsreportserver.config<br /><br /> Rssvrpolicy.config<br /><br /> 報表伺服器 ASP.NET 應用程式的 Web.config。<br /><br /> ASP.NET 的 Machine.config。|  
  
####  <a name="bkmk_restore_operations"></a> 還原作業  
 本節描述您需要移轉的資訊類型，以及完成還原所使用的工具或程序。 您用於還原的工具可能與備份所使用的工具不同。  
  
 在您完成還原步驟之前，您需要安裝及設定新的 SharePoint 伺服器陣列和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。 如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式基本安裝的詳細資訊，請參閱 [安裝 Reporting Services SharePoint 模式](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。  
  
||物件|方法|注意|  
|-|-------------|------------|-----------|  
|**1**|將 SharePoint 內容資料庫還原到新的伺服器陣列。|SharePoint 的「資料庫附加升級」方法。|基本步驟：<br /><br /> 1) 在新的伺服器上還原資料庫。<br /><br /> 2) 藉由指示 URL 將內容資料庫附加到 Web 應用程式。<br /><br /> 3) Get-SPWebapplication 會列出所有 Web 應用程式和 URL。<br /><br /> <br /><br /> 請參閱 [決定升級方法 (SharePoint Server 2010) (http://technet.microsoft.com/library/cc263447.aspx)](http://technet.microsoft.com/library/cc263447.aspx)中的＜資料庫附加升級＞一節及 [連結資料庫並升級為 SharePoint Server 2010 (http://technet.microsoft.com/library/cc263299.aspx)](http://technet.microsoft.com/library/cc263299.aspx)。|  
|**2**|還原原本為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 目錄資料庫 (ReportServer) 的 SQL Server 資料庫。|SQL 資料庫備份及還原。<br /><br /> **或**<br /><br /> 附加及卸離的 SQL Server 資料庫。|使用資料庫時，第一次[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]會視需要更新資料庫結構描述以便讓它將會搭配 SQL Server 2016 環境。|  
|**3**|建立新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。|建立新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。|當您建立新的服務應用程式時，請將它設定為使用複製的報表伺服器資料庫。<br /><br /> 如需使用 SharePoint 管理中心的詳細資訊，請參閱 [在 SharePoint 模式中安裝第一部報表伺服器](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md)中的＜步驟 3：建立 Reporting Services 服務應用程式＞一節。<br /><br /> 如需使用 PowerShell 的範例，請參閱 [Reporting Services SharePoint Service and Service Applications](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)中的＜使用 PowerShell 建立 Reporting Services 服務應用程式＞一節。|  
|**4**|還原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態檔。|簡單檔案複製。|檔案的範例預設位置如下：C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting。|  
|||||  
|**5**|還原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]加密金鑰。|使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的 “SystemSettings” 頁面還原金鑰備份檔。<br /><br /> **或**<br /><br /> PowerShell。|請參閱 [管理 Reporting Services SharePoint 服務應用程式](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)主題中的＜金鑰管理＞一節。|   
  
##  <a name="bkmk_migrate_from_ctp"></a> 從 SQL Server 2012 或 SQL Server 2014 部署移轉  
 在多伺服器陣列中，使用者在不同電腦上可能會擁有內容資料庫和目錄資料庫，此時您只需要將已安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務的新伺服器加入至 SharePoint 伺服器陣列，然後移除舊的伺服器。 您應該不需要複製資料庫。  
  
### <a name="backup-operations"></a>備份作業  
  
1.  備份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密金鑰。  
  
2.  使用 SharePoint 管理中心 (或 PowerShell) 備份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。 這樣也會在 SharePoint 中備份服務應用程式資料庫。 請參閱  [備份與還原 Reporting Services SharePoint 服務應用程式](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)主題。  
  
3.  如果您擁有自動執行帳戶 (UEA) 和 Windows 驗證，請記下認證，好讓您在還原程序中使用認證。  
  
4.  如需詳細資訊，請參閱＜ [在 SharePoint 2013 中備份服務應用程式](http://technet.microsoft.com/library/ee428318.aspx)＞。  
  
### <a name="restore-operations"></a>還原作業  
  
1.  使用 SharePoint 管理中心還原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。 您也可以使用 PowerShell。  
  
2.  還原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密金鑰。  
  
     請參閱 [管理 Reporting Services SharePoint 服務應用程式](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)主題中的＜金鑰管理＞一節。  
  
3.  在服務應用程式上設定 UEA 和 Windows 認證。  
  
4.  如需詳細資訊，請參閱＜ [在 SharePoint 2013 中還原服務應用程式](http://technet.microsoft.com/library/ee428305.aspx)＞。  
  
##  <a name="bkmk_additional_resources"></a> 其他資源  
  
-   [開始升級到 SharePoint 2013 (http://technet.microsoft.com/library/ee833948.aspx)](http://technet.microsoft.com/library/ee833948.aspx)。  
  
-   [升級到 SharePoint 2013 的程序概觀 (http://technet.microsoft.com/library/cc262483.aspx)](http://technet.microsoft.com/library/cc262483.aspx)。  

## <a name="next-steps"></a>後續的步驟

[升級和移轉 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[移轉 Reporting Services 安裝](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

