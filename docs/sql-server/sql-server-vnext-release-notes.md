---
title: "SQL Server vNext 版本資訊 | Microsoft Docs"
ms.custom: ""
ms.date: "03/12/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
caps.latest.revision: 41
author: "craigg-msft"
ms.author: "craigg"
manager: "jhubbard"
caps.handback.revision: 39
---
# SQL Server vNext 版本資訊
本主題描述 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的限制及問題。

- 若要讀取本版的新功能，請參閱 [SQL Server vNext 的新功能](../sql-server/what-s-new-in-sql-server-vnext.md)。
- [SQL Server on Linux 版本資訊](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes) 會發佈在新的擴建文件平台。
- [SQL Server Reporting Services 版本資訊](../reporting-services/reporting-services-版本資訊.md)發佈於 Reporting Services 小節。

 **現在就試試看：**    
   -   [![從 Evaluation Center 下載](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) 從 **[Evaluation Center](http://go.microsoft.com/fwlink/?LinkID=829477)** 下載 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]


## <a name="sql-server-vnext-ctp-13-february--2017"></a>SQL Server vNext CTP 1.3 (2017 年 2 月)
### <a name="supported-installation-scenarios-ctp-13"></a>支援的安裝案例 (CTP 1.3)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 僅為測試版本。  不支援生產環境部署。 建議您在虛擬機器上安裝並測試 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]。

### <a name="documentation-ctp-13"></a>文件 (CTP 1.3)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以「適用於」標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。

### <a name="sql-server-integration-services-ssis-ctp-13"></a>SQL Server Integration Services (SSIS) (CTP 1.3)
#### <a name="cdc-components-not-supported-in-this-ctp-release"></a>這個 CTP 版本不支援 CDC 元件
-   **問題和對客戶的影響**︰這個 CTP 版本不支援 CDC 控制工作、CDC 來源和 CDC 分隔器。
-   **因應措施：** 沒有因應措施。


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-12-january--2017"></a>SQL Server vNext CTP 1.2 (2017 年 1 月)
### <a name="supported-installation-scenarios-ctp-12"></a>支援的安裝案例 (CTP 1.2)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 僅為測試版本。  不支援生產環境部署。 建議您在虛擬機器上安裝並測試 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]。

### <a name="sql-server-database-engine-ctp-12"></a>SQL Server Database Engine (CTP 1.2)
- **問題和對客戶的影響︰**在某些情況下，MSSQLSERVER 服務將會停滯在「開始」狀態。
- **因應措施：**若要解決此問題：
  -  建立 `mssqlserver` 服務和 `keyiso` 服務之間的相依性。 其中一個方法是在已提升權限的命令提示字元中執行下列命令：`sc config mssqlserver depend= keyiso`
  - 重新啟動電腦。

### <a name="documentation-ctp-12"></a>文件 (CTP 1.2)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以「適用於︰」標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。
 
### <a name="sql-server-integration-services-ssis-ctp-12"></a>SQL Server Integration Services (SSIS) (CTP 1.2)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>安裝 SSIS 相應放大時刪除 SSIS 目錄可能會失敗
**問題和對客戶的影響︰**將 SSIS 相應放大功能安裝在電腦上，刪除 SSISDB 目錄資料庫可能會因下列錯誤而失敗：「無法卸除目前使用者已登入的登入 *'login'*」。
   
**因應措施**：
-   在相應放大主機電腦上，執行命令 "services.msc" 以開啟 [服務] 視窗。 停止 SQL Server Integration Services 叢集主機服務。
-   在連接到主機的相應放大背景工作電腦上，執行命令 "services.msc" 以開啟 [服務] 視窗。 停止 SQL Server Integration Services 叢集背景工作服務。

您現在可以刪除 SSISDB 目錄資料庫。

### <a name="sql-server-master-data-services-ctp-12"></a>SQL Server Master Data Services (CTP 1.2)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>交易在實體交易記錄檔類型設為屬性時可能無法使用
**問題和對客戶的影響︰**當實體交易記錄檔類型在 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 中設為 [屬性] 時 (預設值是 [成員])，下列案例會失敗︰

* 網站不會顯示實體變更的交易。
* 無法開啟 [交易] 網頁反轉交易。
* 網站中無法更新有交易註解的實體。

**因應措施：** 沒有因應措施。

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>當 [Copy only committed version (僅複製認可的版本)] 設為 false 時，無法使用複製版本。
-  **問題和對客戶的影響︰**當 [Copy only committed version (僅複製認可的版本)] 設定設為 [否] 時 (預設值為 [是])，複製版本作業可能會失敗。 沒有任何錯誤訊息。
-  **因應措施：** 沒有因應措施。

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-11-december--2016"></a>SQL Server vNext CTP 1.1 (2016 年 12 月)
### <a name="supported-installation-scenarios-ctp-11"></a>支援的安裝案例 (CTP 1.1)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 僅為測試版本。  不支援生產環境部署。 建議您在虛擬機器上安裝並測試 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]。

具體而言，雖然下列案例可能適合您，但它們未經完整測試，且 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] **不**支援：
- 解除安裝 CTP 1.1。
- 與任何其他版本的 SQL Server 並行安裝。
- 從任何舊版的 SQL Server 升級。
- [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 安裝不提供任何 SQL Server 功能套件元件。

### <a name="documentation-ctp-11"></a>文件 (CTP 1.1)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以「適用於︰」標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。

### <a name="sql-server-master-data-services-ctp-11"></a>SQL Server Master Data Services (CTP 1.1)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>交易在實體交易記錄檔類型設為屬性時可能無法使用
**問題和對客戶的影響︰**當實體交易記錄檔類型在 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 中設為 [屬性] 時 (預設值是 [成員])，下列案例會失敗︰

* 網站不會顯示實體變更的交易。
* 無法開啟 [交易] 網頁反轉交易。
* 網站中無法更新有交易註解的實體。

**因應措施：** 沒有因應措施。

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>當 [Copy only committed version (僅複製認可的版本)] 設為 false 時，無法使用複製版本。
-  **問題和對客戶的影響︰**當 [Copy only committed version (僅複製認可的版本)] 設定設為 [否] 時 (預設值為 [是])，複製版本作業可能會失敗。 沒有任何錯誤訊息。
-  **因應措施：** 沒有因應措施。

### <a name="sql-server-integration-services-ssis-ctp-11"></a>SQL Server Integration Services (SSIS) (CTP 1.1)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>安裝 SSIS 相應放大時刪除 SSIS 目錄可能會失敗
**問題和對客戶的影響︰**將 SSIS 相應放大功能安裝在電腦上，刪除 SSISDB 目錄資料庫可能會因下列錯誤而失敗：「無法卸除目前使用者已登入的登入 *'login'*」。
   
**因應措施**：
-   在相應放大主機電腦上，執行命令 "services.msc" 以開啟 [服務] 視窗。 停止 SQL Server Integration Services 叢集主機服務。
-   在連接到主機的相應放大背景工作電腦上，執行命令 "services.msc" 以開啟 [服務] 視窗。 停止 SQL Server Integration Services 叢集背景工作服務。

您現在可以刪除 SSISDB 目錄資料庫。

#### <a name="odbc-components-are-not-supported-in-this-ctp-release"></a>這個 CTP 版本不支援 ODBC 元件
**問題和對客戶的影響**︰這個 CTP 版本不支援 ODBC 連接管理員、來源和目的地。

**因應措施：** 沒有因應措施。

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-10-november-2016"></a>SQL Server vNext CTP 1.0 (2016 年 11 月)
### <a name="supported-installation-scenarios-ctp10"></a>支援的安裝案例 (CTP&1;.0)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 僅為測試版本。  不支援生產環境部署。 建議您在虛擬機器上安裝並測試 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]。

具體而言，雖然下列案例可能適合您，但它們未經完整測試，且 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] **不**支援：
- 解除安裝 CTP 1.0。
- 與任何其他版本的 SQL Server 並行安裝。
- 從任何舊版的 SQL Server 升級。
- [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 安裝不提供任何 SQL Server 功能套件元件。

### <a name="documentation-ctp-10"></a>文件 (CTP 1.0)
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 文件集。  文中專門針對 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 的內容會以**適用於︰**標示。 
- **問題和對客戶的影響︰**[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 沒有離線內容。

### <a name="sql-server-database-engine-ctp-10"></a>SQL Server Database Engine (CTP 1.0)
-  **問題和對客戶的影響︰**CTP1 的 `STRING_AGG` 函數傳回的結果是 LOB 類型 (例如 `NVARCHAR(MAX)`)。 在未來的 CTP 版本中，此行為可能會變更，而若輸入值不是 LOB 類型，`STRING_AGG` 可能會傳回 `NVARCHAR(4000)`。 如果串連的結果無法放入 `NVARCHAR(4000)`，則可能會擲回溢位錯誤。

-  **問題和對客戶的影響︰**避免使用非保留關鍵字，例如將 `WITHIN` 用為 `STRING_AGG` 運算式的別名。 (例如，`SELECT Company.Name, STRING_AGG(Product.Name, ',') AS WITHIN FROM TableA;`。)在未來的 CTP 版本中，接在 `STRING_AGG` 呼叫後面的 `WITHIN` Token 可能會用為 `STRING_AGG` 函數的一部分。

-  **因應措施︰** 請避免使用 `WITHIN` 別名，或將 `AS WITHIN` 新增為別名規格，以避免與未來可能加入 `STRING_AGG` 函數的變更發生衝突。


### <a name="sql-server-integration-services-ctp-10"></a>SQL Server Integration Services (CTP 1.0)
#### <a name="stop-operation-in-ssis-catalog-may-fail"></a>SSIS 目錄的停止作業可能會失敗
**問題和對客戶的影響︰**使用 [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)] 或 catalog.stop_operation 預存程序停止 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 中的作業，可能會因下列錯誤而失敗：「執行使用者自訂常式或彙總 'stop_operation_internal' 時，發生 .NET Framework 錯誤。」

-  **因應措施︰** 開啟 Windows 工作管理員。 在 [處理序] 索引標籤上，找到名為 **ISServerExec** 的處理序，然後按一下 [結束工作] 結束此處理序。

#### <a name="create-dump-of-ssis-pacakge-execution-may-fail"></a>建立 SSIS 封裝執行傾印可能會失敗
**問題和對客戶的影響︰**使用 catalog.create_execution_dump 預存程序建立封裝執行傾印，可能會因下列錯誤而失敗：「執行使用者自訂常式或彙總 'create_execution_dump_internal' 時，發生 .NET Framework 錯誤。」

-  **因應措施︰** 開啟 Windows 工作管理員。 在 [處理序] 索引標籤上，找到名為 **ISServerExec** 的處理序，以滑鼠右鍵按一下此處理序，再按一下 [建立傾印檔案]。

#### <a name="get-perf-counter-of-ssis-package-execution-may-fail"></a>取得 SSIS 封裝執行效能計數器可能會失敗
**問題和對客戶的影響︰**使用 catalog.dm_execution_performance_counters 資料表值函數查詢 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 效能計數器，可能會因下列錯誤而失敗：「執行使用者自訂常式或彙總 'get_execution_perf_counters' 時，發生 .NET Framework 錯誤。」

-  **因應措施**︰使用 Windows 效能監視器直接監視效能計數器值。 沒有因應措施能夠處理針對特定封裝執行的效能計數器問題。

#### <a name="deleting-catalog-may-fail-when-ssis-scale-out-master-is-installed"></a>安裝 SSIS 相應放大主機時刪除目錄可能會失敗
**問題和對客戶的影響︰**將 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 相應放大功能安裝在電腦上，刪除 **SSISDB** 目錄可能會因下列錯誤而失敗： 「無法卸除目前使用者已登入的登入 ‘…’。」 

**因應措施**： 
* 在相應放大主機上執行命令 "services.msc"，開啟 [服務] 視窗並停止 **SQL Server Integration Services 叢集主機**服務。 

* 在連接到主機的相應放大背景工作電腦上，執行命令 "services.msc" 以開啟 [服務] 視窗。 停止 **SQL Server Integration Services 叢集背景工作**服務。 

您現在應該可以刪除 **SSISDB** 目錄。

#### <a name="odbc-connector-in-ssis-is-not-supported"></a>不支援 SSIS 的 ODBC 連接器
-  **問題和對客戶的影響︰**不支援 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 的 ODCB 連接器。
-  **因應措施：** 沒有因應措施。

### <a name="sql-server-reporting-services-ctp-10"></a>SQL Server Reporting Services (CTP 1.0)

SQL Server Reporting Services 並未釋出任何 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 新功能。

### <a name="sql-server-master-data-services-ctp-10"></a>SQL Server Master Data Services (CTP 1.0)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>交易在實體交易記錄檔類型設為屬性時可能無法使用
**問題和對客戶的影響︰**當實體交易記錄檔類型在 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 中設為 [屬性] 時 (預設值是 [成員])，下列案例會失敗︰

* 網站不會顯示實體變更的交易。
* 無法開啟 [交易] 網頁反轉交易。
* 網站中無法更新有交易註解的實體。

**因應措施：** 沒有因應措施。

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>當 [Copy only committed version (僅複製認可的版本)] 設為 false 時，無法使用複製版本。
**問題和對客戶的影響︰**當 [Copy only committed version (僅複製認可的版本)] 設定設為 [否] 時 (預設值為 [是])，複製版本作業可能會失敗。 沒有任何錯誤訊息。

**因應措施：** 沒有因應措施。
 
### <a name="sql-server-management-studio-ssms-ctp-10"></a>SQL Server Management Studio (SSMS) (CTP 1.0)
SQL Server Management Studio 需另行下戴。  如需最新資訊，請參閱 [SQL Server Management Studio - 版本資訊](https://msdn.microsoft.com/library/mt238486.aspx)。

##  <a name="infotipimageshiproominfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) 與 SQL Server 工程團隊交流 
- [堆疊溢位 (標記 sql-server) - 詢問技術性問題](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 論壇 - 詢問技術性問題](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 報告錯誤及要求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有關 R 的一般討論](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
