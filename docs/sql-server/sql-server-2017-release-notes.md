---
title: "SQL Server 2017 版本資訊 | Microsoft Docs"
ms.custom: 
ms.date: 05/16/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
caps.latest.revision: 41
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 6aa73e749d4f308265dfe27a160802c15a391a3e
ms.openlocfilehash: a2950b6aef0e12653efbb9eb26fd3f1ae6cb951e
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="sql-server-2017-release-notes"></a>SQL Server 2017 版本資訊
本主題描述 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]的限制及問題。 如需相關資訊，請參閱下列各項：

- [SQL Server 2017 的新功能](../sql-server/what-s-new-in-sql-server-2017.md)。
- [SQL Server on Linux 版本資訊](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes)的限制及問題。
- [SQL Server Reporting Services 版本資訊](../reporting-services/reporting-services-release-notes.md)的限制及問題。

 **現在就試試看：**    
   -   [![從 Evaluation Center 下載](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  從 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] Evaluation Center **[下載](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="sql-server-2017-release-candidate-rc1---july-2017"></a>SQL Server 2017 候選版 (RC1 - 2017 年 7 月)

### <a name="sql-server-integration-services-ssis-rc1---july-2017"></a>SQL Server Integration Services (SSIS) (RC1 - 2017 年 7 月)
- **問題和客戶的影響：**為了一致性和可讀性，預存程序 **[catalog].[create_execution]** 的參數 *runincluster* 已重新命名為 *runinscaleout*。
- **因應措施：**如果您有現成的指令碼可在 [相應放大] 中執行套件，您必須將參數名稱從 *runincluster* 變更為 *runinscaleout*，以確保這些指令碼在 RC1 中正常運作。

- **問題和客戶的影響：**SQL Server Management Studio (SSMS) 17.1 和舊版無法在 RC1 的 [相應放大] 中觸發套件執行。 錯誤訊息為：「*@runincluster* 不是程序 **create_execution** 的參數。」 SSMS 的下一個版本 17.2 版中將會修正此問題。 SSMS 17.2 版和更新版本支援 [相應放大] 中的新參數名稱和套件執行。 
- **因應措施：**在 SSMS 17.2 版可用之前，您可以使用現有的 SSMS 版本來產生套件執行指令碼，然後將指令碼中的 *runincluster* 參數名稱變更為 *runinscaleout*，再執行此指令碼。

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1 (2017 年 5 月)
### <a name="documentation-ctp-21"></a>文件 (CTP 2.1)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以「適用於」標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **問題和客戶的影響：**如果您有 SQL Server Reporting Services 和 Power BI 報表伺服器在相同電腦上，並解除安裝其中一個，您再也無法連線到其餘的報表伺服器與報表伺服器組態管理員。
- **因應措施：**若要解決此問題，您必須在執行下列作業之後解除安裝其中一個伺服器。

    1. 以系統管理員模式啟動命令提示字元。
    2. 前往剩餘的報表伺服器安裝所在目錄。

        *Power BI 報表伺服器的預設位置：C:\Program Files\Microsoft Power BI 報表伺服器*

        *SQL Server Reporting Services 的預設位置：C:\Program Files\Microsoft SQL Server　Reporting Services*

    3. 接著移至下一個資料夾。 根據剩餘的項目，這會是 *SSRS* 或 *PBIRS*。
    4. 移至 WMI 資料夾。
    5. 執行下列命令：

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        如果您看到下列錯誤，可以加以忽略。

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP 2.1)

- **問題和客戶的影響：** 在已安裝 2016 版本的 *TSqlLanguageService.msi* (透過 SQL 安裝程式或安裝為獨立可轉散發套件) 的機器上安裝之後，即會移除 v13.* (SQL 2016) 版本的 *Microsoft.SqlServer.Management.SqlParser.dll* 和 *Microsoft.SqlServer.Management.SystemMetadataProvider.dll*。 任何相依於這些 2016 版本組件的應用程式之後會停止運作，並提供如下錯誤：*錯誤： 無法載入檔案或組件 'Microsoft.SqlServer.Management.SqlParser, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' 或其中一個相依性。系統找不到指定的檔案。*

   此外，嘗試重新安裝 2016 版本的 TSqlLanguageService.msi 將會失敗，並顯示訊息：*安裝 Microsoft SQL Server 2016 T-SQL 語言服務失敗，因為電腦上已經有較新的版本*。

- **因應措施：**若要暫時解決此問題，並修正相依於 v13 版本組件的應用程式，請遵循下列步驟：

   1. 移至**新增/移除程式**
   1. 尋找 *Microsoft SQL Server vNext T-SQL 語言服務 CTP2.1*，以滑鼠右鍵按一下，然後選取**解除安裝**。
   1. 移除元件之後，修復中斷的應用程式 (或重新安裝適當版本的 *TSqlLanguageService.MSI*)

   這個因應措施會移除這些 v14 版本組件，讓任何相依於 v14 版本的應用程式再也無法運作。 如果需要這些組件，則需要不使用並行 2016 安裝的個別安裝。

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0 (2017 年 4 月)
### <a name="documentation-ctp-20"></a>文件 (CTP 2.0)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以「適用於」標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。

### <a name="always-on-availability-groups"></a>AlwaysOn 可用性群組

- **問題和客戶的影響：**如果 SQL Server 主要版本低於裝載主要複本的執行個體，裝載可用性群組次要複本的 SQL Server 執行個體就會當機。 影響從所有裝載可用性群組的受支援版本 SQL Server 升級到 SQL server [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0 的作業。 在下列步驟中將發生此狀況。 

> 1. 使用者可根據[最佳做法](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)，升級裝載次要複本的 SQL Server 執行個體。
> 2. 升級後進行容錯移轉，在新升級的次要複本變成主要複本之後，才能完成可用性群組中的所有次要複本的升級。 舊的主要複本現在是次要複本，其版本可能低於主要複本。
> 3. 可用性群組處於不支援的組態下，因此任何剩餘的次要複本可能會很容易當機。 

- **因應措施：**連線到裝載新的主要複本的 SQL Server 執行個體，並從組態中移除錯誤的次要複本。

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   裝載次要複本的 SQL Server 執行個體即會復原。

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) 與 SQL Server 工程團隊交流 
- [堆疊溢位 (標記 sql-server) - 詢問技術性問題](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 論壇 - 詢問技術性問題](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 報告錯誤及要求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有關 R 的一般討論](https://www.reddit.com/r/SQLServer/)

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
