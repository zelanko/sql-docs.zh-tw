---
title: "SQL Server 2017 版本資訊 |Microsoft 文件"
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 67c1c0f3a9da6cc5d050da5db8a493f5da934c2a
ms.openlocfilehash: fa45fea4ebb378f035b4b4af2b1fa8a20bc152a5
ms.contentlocale: zh-tw
ms.lasthandoff: 06/23/2017

---
# <a name="sql-server-2017-release-notes"></a>SQL Server 2017 版本資訊
本主題描述 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的限制及問題。 相關資訊，請參閱下列各項：

- [新功能 SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)。
- [SQL Server 上的 Linux 版本資訊](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes)。
- [SQL Server Reporting Services 版本資訊](../reporting-services/reporting-services-release-notes.md)。

 **現在就試試看：**    
   -   [![從 Evaluation Center 下載](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  從 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] Evaluation Center **[下載](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1 (可能 2017)
### <a name="documentation-ctp-21"></a>文件 (CTP 2.1)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以「適用於」標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **問題和客戶的影響：**如果您有 SQL Server Reporting Services 和 Power BI 報表伺服器在相同電腦，並解除安裝其中一個，您將不再能夠連線到其餘的報表伺服器與報表伺服器組態管理員。
- **因應措施**若要解決此問題，您必須執行下列作業之後解除安裝其中一個伺服器。

    1. 啟動命令提示字元，以系統管理員模式。
    2. 前往剩餘的報表伺服器安裝所在目錄。

        *Power BI 報表伺服器的預設位置： C:\Program Files\Microsoft Power BI 報表伺服器*

        *SQL Server Reporting Services 的預設位置： C:\Program Files\Microsoft SQL Server 報告的服務*

    3. 接著移至下一個資料夾。 這會是*SSRS*或*PBIRS*根據剩餘的項目。
    4. 移至 WMI 資料夾。
    5. 執行下列命令：

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        您可以忽略下列錯誤，如果您看到它。

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP 2.1)

- **問題和客戶的影響：** 2016年的版本的電腦上安裝之後*TSqlLanguageService.msi* （透過 SQL 安裝程式或安裝為獨立可轉散發套件） v13.* (SQL 2016) 的版本*Microsoft.SqlServer.Management.SqlParser.dll*和*Microsoft.SqlServer.Management.SystemMetadataProvider.dll*會移除。 任何有相依的這些組件的 2016年版本的應用程式將會再停止運作，提供類似的錯誤：*錯誤： 無法載入檔案或組件 ' Microsoft.SqlServer.Management.SqlParser，Version = 13.0.0.0，Culture = neutral，PublicKeyToken = 89845dcd8080cc91' 或其中一個相依性。系統找不到指定的檔案。*

   此外，嘗試重新安裝 TSqlLanguageService.msi 2016 版本將會失敗並出現訊息：*安裝的 Microsoft SQL Server 2016 T-SQL 語言服務失敗，因為較高的版本已經存在電腦上*。

- **因應措施**暫時解決此問題，並修正應用程式相依於 v13 版本的組件請遵循下列步驟：

   1. 移至**新增/移除程式**
   1. 尋找*Microsoft SQL Server vNext T-SQL 語言服務 CTP2.1*，以滑鼠右鍵按一下，然後選取**解除安裝**。
   1. 移除元件之後，修復就會中斷應用程式 (或重新安裝適當版本的*TSqlLanguageService.MSI*)

   這個因應措施會移除這些組件，v14 版本，以便任何相依於 v14 版本的應用程式將無法再運作。 如果需要這些組件，而任何由並行 2016年安裝不是個別安裝不需要的。

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0 (第 2017 年 4 月)
### <a name="documentation-ctp-20"></a>文件 (CTP 2.0)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以「適用於」標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。

### <a name="always-on-availability-groups"></a>AlwaysOn 可用性群組

- **問題和客戶的影響：**裝載可用性群組次要複本的 SQL Server 執行個體當機，如果 SQL Server 主要版本低於裝載主要複本的執行個體。 會影響所有受支援版本的 SQL Server 裝載 SQL server 的可用性群組升級[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]CTP 2.0。 發生這種情況下的下列步驟。 

> 1. 使用者可升級 SQL Server 執行個體裝載次要複本根據[最佳做法](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)。
> 2. 升級之後，容錯移轉，而且新升級的次要變成主要複本之前完成可用性群組中的所有次要複本的升級。 舊的主要現在是次要複本，這可能會比主要更舊版本。
> 3. 可用性群組處於不支援的組態和任何剩餘的次要複本可能會很容易損毀。 

- **因應措施**連接到裝載的新的主要複本並移除從組態錯誤的次要複本的 SQL Server 執行個體。

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   裝載次要複本的 SQL Server 執行個體復原。


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-14-march--2017"></a>SQL Server 2017 CTP 1.4 (第 2017 年 3 月)

### <a name="documentation-ctp-14"></a>文件 (CTP 1.4)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以「適用於」標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-13-february--2017"></a>SQL Server 2017 CTP 1.3 (第 2017 年 2 月)
### <a name="supported-installation-scenarios-ctp-13"></a>支援的安裝案例 (CTP 1.3)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 僅為測試版本。  不支援生產環境部署。 建議您在虛擬機器上安裝並測試 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 。

### <a name="documentation-ctp-13"></a>文件 (CTP 1.3)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以「適用於」標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。

### <a name="sql-server-integration-services-ssis-ctp-13"></a>SQL Server Integration Services (SSIS) (CTP 1.3)
#### <a name="cdc-components-not-supported-in-this-ctp-release"></a>這個 CTP 版本不支援 CDC 元件
-   **問題和對客戶的影響**︰這個 CTP 版本不支援 CDC 控制工作、CDC 來源和 CDC 分隔器。
-   **因應措施：**沒有因應措施。


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-12-january--2017"></a>SQL Server 2017 CTP 1.2 (第 2017 年 1 月)
### <a name="supported-installation-scenarios-ctp-12"></a>支援的安裝案例 (CTP 1.2)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 僅為測試版本。  不支援生產環境部署。 建議您在虛擬機器上安裝並測試 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 。

### <a name="sql-server-database-engine-ctp-12"></a>SQL Server Database Engine (CTP 1.2)
- **問題和對客戶的影響︰** 在某些情況下，MSSQLSERVER 服務將會停滯在「開始」狀態。
- **因應措施：** 若要解決此問題：
  -  建立 `mssqlserver` 服務和 `keyiso` 服務之間的相依性。 其中一個方法是在已提升權限的命令提示字元中執行下列命令： `sc config mssqlserver depend= keyiso`
  - 重新啟動電腦。

### <a name="documentation-ctp-12"></a>文件 (CTP 1.2)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以「適用於︰」標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。
 
### <a name="sql-server-integration-services-ssis-ctp-12"></a>SQL Server Integration Services (SSIS) (CTP 1.2)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>安裝 SSIS 相應放大時刪除 SSIS 目錄可能會失敗
**問題和對客戶的影響︰**將 SSIS 相應放大功能安裝在電腦上，刪除 SSISDB 目錄資料庫可能會因下列錯誤而失敗：「無法卸除目前使用者已登入的登入 *'login'* 」。
   
**因應措施**：
-   在相應放大主機電腦上，執行命令 "services.msc" 以開啟 [服務] 視窗。 停止 SQL Server Integration Services 叢集主機服務。
-   在連接到主機的相應放大背景工作電腦上，執行命令 "services.msc" 以開啟 [服務] 視窗。 停止 SQL Server Integration Services 叢集背景工作服務。

您現在可以刪除 SSISDB 目錄資料庫。

### <a name="sql-server-master-data-services-ctp-12"></a>SQL Server Master Data Services (CTP 1.2)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>交易在實體交易記錄檔類型設為屬性時可能無法使用
**問題和對客戶的影響︰** 當實體交易記錄檔類型在 **中設為 [屬性]**[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 時 (預設值是 [成員] )，下列案例會失敗︰

* 網站不會顯示實體變更的交易。
* 無法開啟 [交易]  網頁反轉交易。
* 網站中無法更新有交易註解的實體。

**因應措施：**沒有因應措施。

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>當 [Copy only committed version (僅複製認可的版本)]  設為 false 時，無法使用複製版本。
-  **問題和對客戶的影響︰** 當 [Copy only committed version (僅複製認可的版本)]  設定設為 [否]  時 (預設值為 [是] )，複製版本作業可能會失敗。 沒有任何錯誤訊息。
-  **因應措施：**沒有因應措施。

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) 與 SQL Server 工程團隊交流 
- [堆疊溢位 (標記 sql-server) - 詢問技術性問題](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 論壇 - 詢問技術性問題](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 報告錯誤及要求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有關 R 的一般討論](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)


