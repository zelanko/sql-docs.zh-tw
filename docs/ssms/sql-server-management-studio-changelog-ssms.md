---
title: "SQL Server Management Studio - 變更記錄 (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 72
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2144751277bb10897e0ed39ee24dbad8a32b4ce
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)

## <a name="ssms-1653-release"></a>SSMS 16.5.3 版
正式運作 | 組建編號：13.0.16106.4

這個版本已修正下列問題：

* 修正 SSMS 16.5.2 中出現的問題，這造成 'Table' 節點會在資料表有多個疏鬆資料行時展開。

* 使用者可以將包含 OData 連線管理員且連線到 Microsoft Dynamics AX/CRM Online 資源的 SSIS 套件部署到 SSIS 目錄。 如需詳細資訊，請參閱 [OData 連線管理員](https://msdn.microsoft.com/library/dn584133.aspx)。

* 在現有資料表上設定 Always Encrypted 失敗，不相關的物件發生錯誤。 [Connect 識別碼 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* 無法為具有多個結構描述的現有資料庫設定 Always Encrypted。 [Connect 識別碼 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* Always Encrypted、加密資料行精靈失敗，原因是資料庫包含參考系統檢視的檢視。 [Connect 識別碼 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* 使用 Always Encrypted 進行加密時，未正確處理加密後來自重新整理模組的錯誤。

* 「開啟最近使用的項目」功能表未顯示最近儲存的檔案。 [Connect 識別碼 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* SSMS 在以右鍵按一下資料表索引時 (透過遠端 (網際網路) 連線) 很緩慢。 [Connect 識別碼 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* 修正 SQL Designer 捲軸的問題。 [Connect 識別碼 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* 資料表的操作功能表會短暫停止回應 
 
* SSMS 有時會擲回活動監視器的例外狀況及損毀。 [Connect 識別碼 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016 會損毀，並出現錯誤「處理序因位於 IP 71AF8579 (71AE0000) 的 .NET 執行階段發生內部錯誤而終止，錯誤碼為 80131506」


## <a name="ssms-1651-release"></a>SSMS 16.5.1 版本
正式運作 | 組建編號：13.0.16100.1

* 已修正 Invoke-Sqlcmd 在 CHECK 條件約束發生時錯誤插入多個資料列的問題。 [Microsoft Connect 項目：811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* 已修正建立可用性群組時，非英文語言版本運作不完全的問題。

* 已修正按一下查詢計劃 XML 未開啟適當 SSMS UI 的問題。


## <a name="ssms-165-release"></a>SSMS 16.5 版
公開上市 |組建編號︰ 13.0.16000.28

* 修正了當按一下名稱包含 ";:" 資料庫資料表時會發生當機的問題。
* 修正了在 AS表格式資料庫之 [屬性] 視窗的 [模型] 頁面中執行變更時，會寫出原始定義的問題。 
[Microsoft Connect 項目：3080744](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* 修正了暫存檔案會新增到 [最近使用的檔案] 清單。  
[Microsoft Connect 項目：2558789](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* 修正了物件總管樹狀目錄中，使用者資料表節點之 [管理壓縮] 功能表項目遭到停用的問題。  
[Microsoft Connect 項目：3104616](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* 修正了使用者無法設定物件總管、註冊後的伺服器總管、範本總管與物件總管詳細資料的字型大小問題。 這些總管會使用環境的字型。  
[Microsoft Connect 項目：691432](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* 修正了 SSMS 在連線中斷後，一律時會重新連線到預設資料庫的問題。  
[Microsoft Connect 項目：3102337](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* 修正了原則管理與查詢編器視窗中許多 DPI 太高的問題，包括執行計畫圖示。

* 修正了「擴充的事件」沒有選項可以設定字型與色彩的問題。

* 修正了 SSMS 會在關閉應用程式時，或在嘗試顯示錯誤對話方塊時會損毀時的問題。


## <a name="ssms-1641-september-2016-release"></a>SSMS 16.4.1 (2016 年 9 月) 版
正式運作 | 組建編號：13.0.15900.1

*  修正了嘗試變更/修改預存程序失敗的問題︰  
[Microsoft Connect 項目 #3103831](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* 新增加 'Read-SqlTableData'、'Read-SqlViewData' 及 'Write-SqlTableData' Cmdlet，讓您可以使用 PowerShell 檢視及寫入資料。  
[Trello Read-SqlTableData 卡](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Microsoft Connect 項目 #2685363](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* 新增加 'Add-SqlLogin' Cmdlet 可讓您透過 PowerShell 執行一些新的登入管理工作。  
[Microsoft Connect 項目 #2588952](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  連線到境內不同雲端的使用者現在可享有更好的支援與使用經驗。
    
    
*  修正了擲回記憶體不足例外狀況的問題。  
[Microsoft Connect 項目 #3062914](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Microsoft Connect 項目 #3074856](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  修正了無法使用結構描述作為篩選選項的問題。  
[Microsoft Connect 項目 #3058105](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Microsoft Connect 項目 #3101136](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  修正了無法存取延伸資料庫之 [監視器] 視窗的問題。
    
*  修正了 F1 說明一律會開啟線上內容的問題。 使用者現在可以透過 [說明] 功能表中的 [設定說明偏好]，選擇要使用線上說明或離線說明。   
[Microsoft Connect 項目 #2826366](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  修正了編寫 1200 相容性層級之 Analysis Services 表格式模型的指令碼，仍無法去除編寫指令碼的密碼，而且即使伺服器版本已經是「用戶端模型物件現在會在編寫指令碼之前先同步」亦是如此的問題。
    
*  修正了 'SELECT TOP N ROWS' 選項會產生 TOP 運算子即將被取代之語法的問題。  
[Microsoft Connect 項目 #3065435](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  修正 SSMS 中多項版面配置問題，包括 [登入屬性] 頁面及各項進階查詢執行選項的問題。   
[Microsoft Connect 項目 #3058199](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 項目 #3079122](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 項目 #3071384](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  修正了使用者一開啟新的查詢視窗，就會自動建立解決方案的問題。   
[Microsoft Connect 項目 #2924667](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Microsoft Connect 項目 #2917742](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Microsoft Connect 項目 #2612635](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  修正了當時態表位於系統資料庫時，在物件總管中無法擴充的問題。  
[Microsoft Connect 項目 #2551649](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  已修正 SSMS 在執行批次後對 SELECT @@trancount 執行查詢的問題。    
[Microsoft Connect 項目 #3042364](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  修正了 Analysis Services 在從伺服器的 [屬性] 頁面建立指令碼時，會產生隱藏的連線對話方塊的問題。
    
*  修正了 Ctrl + Q 不會選取 [快速啟動] 工具列的問題。
    
*  修正了使用 [伺服器屬性] 對話方塊，為大於 2 TB 之資料庫變更資料庫的 MaxSize 時，資料庫會中斷的問題。  
[Microsoft Connect 項目 #1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  修正了 [還原資料庫精靈] 不接受包含前置空格之檔案名稱的問題︰   
[Microsoft Connect 項目 #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="ssms-163-august-2016-release"></a>SSMS 16.3 (2016 年 8 月) 版本
正式推出 | 版本號碼：13.0.15700.28

* SSMS 的每月版本現在將以數值標註。

* [新驗證選項：「Active Directory 通用驗證」](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)。 這個一個由 Azure Active Directory 驅動的權杖型驗證機制，支援多因素、密碼及整合式驗證機制。

* 符合 SQL Server Profiler 範本的新擴充事件範本 [(Microsoft Connect 項目 #2543925)](https://connect.microsoft.com/SQLServer/feedback/details/2543925/sql-server-extended-events-profiler-tool)。 深入了解包含的 [SQL Server Profiler 範本](https://msdn.microsoft.com/library/ms190176.aspx)。

* 針對 Azure SQL 資料庫推出新的 [建立資料庫和資料庫屬性] 對話方塊。

* 新的 'Get-SqlLogin' 和 'Remove-SqlLogin' Cmdlet 以協助使用 PowerShell 執行 SQL Server 登入管理。  
*連結的客戶 Bug 要求：*   
[Microsoft Connect 項目 #2588952。](https://connect.microsoft.com/SQLServer/feedback/details/2588952/)

* 新的 PowerShell Cmdlet 'New-SqlColumnMasterKeySettings'，加入針對任意提供者和金鑰路徑建立資料行主要金鑰的支援。

* 新的 [建立資料庫] 對話方塊以簡化在 SSMS 中建立 Azure SQL 資料庫的程序。

* 支援在 SSMS 物件總管的 [資料庫] 節點中進行篩選援。 在物件總管中，瀏覽至 [資料庫] 節點，並按一下位於物件總管工具列中的篩選圖示，以篩選資料庫清單。

* 在備份與還原精靈中支援 Azure Resource Manager (ARM) 類型的儲存體帳戶。

* [針對高解析度顯示器的初始 Beta 支援](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/)。  
*連結的客戶 Bug 要求：*   
[Microsoft Connect 項目 #1129301](https://connect.microsoft.com/SQLServer/feedback/details/1129301/management-studio-is-unusable-on-a-4k-display)、 [Microsoft Connect 項目 #1858763](https://connect.microsoft.com/SQLServer/feedback/details/1858763/)、 [Microsoft Connect 項目 #1852671](https://connect.microsoft.com/SQLServer/feedback/details/1852671/)、 [Microsoft Connect 項目 #1487643](https://connect.microsoft.com/SQLServer/feedback/details/1487643/)、  [Microsoft Connect 項目 #1355641](https://connect.microsoft.com/SQLServer/feedback/details/1355641/)、 [Microsoft Connect 項目 #2161595](https://connect.microsoft.com/SQLServer/feedback/details/2161595/)、 [Microsoft Connect 項目 #1854041](https://connect.microsoft.com/SQLServer/feedback/details/1854041/)、 [Microsoft Connect 項目 #1055617](https://connect.microsoft.com/SQLServer/feedback/details/1055617/)、 [Microsoft Connect 項目 #2448774](https://connect.microsoft.com/SQLServer/feedback/details/2448774/)、 [Microsoft Connect 項目 #1521405](https://connect.microsoft.com/SQLServer/feedback/details/1521405/)、 [Microsoft Connect 項目 #2117853](https://connect.microsoft.com/SQLServer/feedback/details/2117853/)、 [Microsoft Connect 項目 #2014256](https://connect.microsoft.com/SQLServer/feedback/details/2014256/)、 [Microsoft Connect 項目 #2162218](https://connect.microsoft.com/SQLServer/feedback/details/2162218/)、 [Microsoft Connect 項目 #2344551](https://connect.microsoft.com/SQLServer/feedback/details/2344551/)、 [Microsoft Connect 項目 #1664436](https://connect.microsoft.com/SQLServer/feedback/details/1664436/)、 [Microsoft Connect 項目 #2554043](https://connect.microsoft.com/SQLServer/feedback/details/2554043/)、 [Microsoft Connect 項目 #2983216](https://connect.microsoft.com/SQLServer/feedback/details/2983216/)、 [Microsoft Connect 項目 #2021706](https://connect.microsoft.com/SQLServer/feedback/details/2021706/)

* 改進 Database Engine Tuning Advisor (DTA)，以支援從 SQL Server 查詢存放區自動讀取工作負載。

* 改進 Database Engine Tuning Advisor (DTA)，以針對叢集資料行存放區索引、非叢集資料行存放區索引，以及資料列存放區索引顯示索引建議。

* 支援使用 SQL Server Analysis Services PowerShell Cmdlet 傳送資料庫主控台命令 (DBCC)。

* 針對在 SSMS 中檢視加密的 AlwaysEncrypted 大型物件 (LOB) 資料行之純文字的錯誤修正。  
*連結的客戶 Bug 要求：*   
[Microsoft Connect 項目 #2413024](https://connect.microsoft.com/SQLServer/feedback/details/2413024/cannot-view-cleartext-of-alwaysencrypted-lob-columns-in-ssms)

* 修正 [永遠加密] 對話方塊中的錯誤，以修正沒有啟用 Windows 視覺樣式 (例如啟用高對比顯示) 時所發生的當機問題。

* 針對導致無法連線到 SQL Server 執行個體的「找不到方法」錯誤的錯誤修正。

* 針對搭配 Datetime Offset 建立資料分割函數時會造成 SSMS 當機的錯誤修正。

* 針對新增/移除啟動 Distributed Replay 管理工具 (DReplay.exe) 的 Microsoft .Net 3.5 需求的錯誤修正。

* 修正 Analysis Services 部署精靈中的錯誤，以支援完整的伺服器名稱。

* 修正 SSMS 中的錯誤，以在具有 2016 相容性模型的 Analysis Services 表格式模型中顯示資料分割。  
*連結的客戶 Bug 要求：*   
[Microsoft Connect 項目 #2845053](https://connect.microsoft.com/SQLServer/feedback/details/2845053/ssms-cannot-display-partitions-in-tabular-models-in-2016-compatibility-level) 

* 針對 Analysis Services 表格式模型及 SQL Server 共用管理物件 (SMO) 的效能改進和錯誤修正。 


---
## <a name="ssms-july-2016-hotfix-update-release"></a>SSMS 2016 年 7 月 Hotfix 更新版本 
正式推出 | 版本號碼：13.0.15600.2

* 修正 SSMS 中的錯誤，以啟用遺失的右鍵功能表項目。  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect 項目 #2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect 項目 #2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016-release"></a>SSMS 2016 年 7 月版本 
正式推出 | 版本號碼：13.0.15500.91

* *編輯，7 月 5 日：*改進 SQL Server 2016 (1200 相容性層級) 表格式資料庫在 Analysis Services 處理對話方塊及 Analysis Services 部署精靈中的支援。

* *編輯，7 月 5 日：*在 SSMS [查詢執行選項] 對話方塊中新增設定 'XACT_ABORT' 的選項。此選項在這一版 SSMS 中預設為啟用，它會指示 SQL Server 復原整個交易，並在發生執行階段錯誤時中止批次。

* **在 SSMS 中支援 Azure SQL 資料倉儲。**

* SQL Server PowerShell 模組的重大更新。這包括新的 [SQL PowerShell 模組以及適用於永遠加密、SQL Agent 及 SQL 錯誤記錄檔的新 CMDLET](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update)。

* 支援在永遠加密精靈中產生 PowerShell 指令碼。

* **大幅改善 Azure SQL 資料庫的連線時間。**

* **新的 [備份至 URL] 對話方塊支援為 SQL Server 2016 資料庫備份建立 Azure 儲存體認證。這讓在 Azure 儲存體帳戶中儲存資料庫備份的體驗更為簡化。**
 
* **新增 [還原] 對話方塊以簡化從 Microsoft Azure 儲存體服務還原 SQL Server 2016 資料庫備份的作業。**
 
* **修正 SSMS 查詢設計工具中的 Bug，讓沒有資料表 SELECT 權限的使用者也能將其新增至設計工具。**

* **Bug 修正，以新增 'TRY_CAST()' 與 'TRY_CONVERT()' 函數的 IntelliSense 支援。**  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast)。

* **修正 PowerShell 模組中的 Bug，以啟用 ‘SQLAS’ Analysis Services 延伸模組的載入。**  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension)。

* **修正 SSMS 編輯器視窗中的 Bug，以允許用拖放方式開啟 SQL 檔案。**  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios)。

* **修正 Profiler 中的 Bug，以修正結束時 Profiler 當機的情況。**  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2616550](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped)。  
[Microsoft Connect 項目 #2319968](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968)。

* **修正 SSMS 中的 Bug，以防止在嘗試編輯 SSMS 資料表設計工具中的加入連結時發生當機。**  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2721052](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms)。

* **修正 SSMS 中的 Bug，允許 db_owner 角色成員產生資料庫指令碼。**  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june)。

* **修正 SSMS 編輯器中的 Bug，以移除在伺服器離線時關閉查詢索引標籤的延遲問題。**  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline)。

* **Bug 修正，以允許在 SQL Server Express 資料庫中使用 [備份] 選項。**  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2801910](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks)。  
[Microsoft Connect 項目 #2874434](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance)。

* **修正 Analysis Services 的 Bug，為多維度 Analysis Services 模型正確顯示資料摘要提供者。**

----
## <a name="ssms-june-2016-generally-available-release"></a>SSMS 2016 年 7 月正式推出版本
正式推出 | 版本號碼：13.0.15000.23

* **SSMS 從 2016 年 6 月版本後將為正式運作。**

* **SSMS 中的新 [快速尋找] 對話方塊將能與目前的文件更完善地整合，並允許透過規則運算式進行搜尋。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* **改進 SSMS 安裝程式，以允許您追蹤安裝進度，並透過指令碼處理自動安裝的結束代碼。**

* **修正 SSMS 即時線上 F1 說明中的 Bug，以正確顯示說明文件和文章。**

* **修正查詢資料存放區 [迴歸查詢] 檢視中，因捲動而造成 SSMS 當機的 Bug。** 

* **修正 Excel Analysis Services OLEDB 連接器中的 Bug，以允許從 Excel 2016 連線到 SQL Server Analysis Services。**

* **修正 SSMS [連線] 對話方塊中的 Bug，以在使用多重監視器的系統時，於主要 SSMS 視窗所在的監視器上顯示 [連線] 對話方塊。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* **修正 Always Encrypted 體驗中的 Bug。已修正 [永遠加密] 功能表選項沒有針對 Stretch Database 正確啟用的錯誤。同時已修正 Always Encrypted 精靈沒有正確使用 SafeNet (Luna SA) HSM 提供者的 Bug。**

---
## <a name="ssms-april-2016-preview"></a>SSMS 2016 年 4 月預覽 
版本號碼：13.0.14000.36
  
* **對 SSMS 安裝程式的改進，以新增人工可讀取的錯誤訊息。**  
  
* 針對 Stretch Database 精靈的改進，以新增述詞的支援。  
  
* 針對 AlwaysEncrypted PowerShell Commandlet 的改進，以加入金鑰加密 API。  
  
* **Bug 修正，以在 IntelliSense 已於 [工具]、[選項] 對話方塊中關閉的情況下，於 SSMS 工具列中關閉 IntelliSense。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2555163/sql-2016-rc2-turning-off-intellisense-from-options-does-not-turn-it-off-on-toolbar/>  
    
* 針對執行程序表比較使用者介面的改進和錯誤修正，以減少長查詢計劃所使用的間距。  
  
* 修正 SSMS 中的錯誤，以修正造成 SSMS 於結束時當機的問題。   
  
* 修正永遠加密精靈中的錯誤，以在加密期間保留使用者權限，並在精靈完成後允許資料庫中斷連結作業。  
  
* **修正 Always Encrypted [新增資料行主要金鑰] 對話方塊中的 Bug，以在嘗試使用不支援的密碼編譯演算法 (CNG) 提供者產生金鑰時提供意見反應。**  
  
---  
## <a name="ssms-march-2016-preview-refresh"></a>SSMS 2016 年 3 月預覽重新整理
版本號碼：13.0.13000.55
  
* **SSMS 現已使用 Visual Studio 2015 Isolated Shell。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2390544/update-ssms-to-use-visual-studio-2015-dependencies/>  
  
* **新快速啟動工具列，可協助您快速找到功能表物件及選項。(VS 2015 Isolated Shell)**  
  
* **改進 SSMS 佈景主題選項，以新增 SSMS 淺色佈景主題的支援。(VS 2015 Isolated Shell)**  
  
* **修正 SSMS 工具功能表選項的 Bug，以在點選 [重設為預設值] 按鈕時正確重設查詢捷徑。**  
  
* **修正 SSMS 新專案範本的 Bug，以顯示可輕鬆閱讀的範本名稱。**  
  
* **已解決在 SSMS 中查看 SQL Agent 作業記錄的錯誤。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2458860/error-viewing-job-history-microsoft-datawarehouse-sqm/>  
    
* **Bug 修正，以允許離線安裝 SSMS。這可讓您在沒有網際網路連線的情況下進行安裝。(VS 2015 Isolated Shell)**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2497178/cannot-install-ssms-when-server-has-no-internet-access/>  
    
* **Bug 修正，以在匯入 SQL Server PowerShell (SQLPS) 模組時保留使用者的目前目錄。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2434605/loading-sqlps-module-changes-current-directory-to-ps-sqlserver/>  
    
* **修正 SQL Server PowerShell (SQLPS) 模組中的 Bug，以使用已核准的 PowerShell 動詞。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2432891/sqlps-module-uses-unapproved-powershell-verbs/>  
    
* **修正 SQL Server PowerShell (SQLPS) 模組中的 Bug，以加快模組的載入速度。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2429153/sqlps-module-is-slow-to-load/>  
    
* **修正 SQL Agent 作業步驟中的 Bug，以允許修改作業步驟。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2453996/issues-with-agent-in-ssms-2016-rc0-13-0-12000-65/>  
    
* **修正 SSMS 物件總管 中的 Bug，以依字母順序列出資料表。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2424718/sql-server-2016-ssms-table-list-confusing/>  
    
* **修正 [可用的資料庫] 下拉式清單中的 Bug，以在 SQL Server 連線變更時顯示正確的資料庫名稱清單。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2513420/available-databases-drop-down-box-does-not-update-when-connection-changes-in-ssms/>  
    
* **修正 SSMS 鍵盤快速鍵中的 Bug，以在點選 'CTRL+U' 按鍵輸入時，將焦點移到 [可用的資料庫] 下拉式清單**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2534820/ssms-ctrl-u-doesnt-work/>  
  
---  
## <a name="ssms-march-2016-preview"></a>SSMS 2016 年 3 月預覽 
版本號碼：13.0.12500.29 
  
* **改進 SSMS Web 安裝程式，以允許使用鍵盤按鍵進行瀏覽。**  
  
* **改進 AlwaysEncrypted 精靈，以對加密支援別名資料類型。**  
  
* **修正 AlwaysOn [新增可用性群組精靈] 的 Bug，以顯示正確的自動容錯移轉目標最大值。**  
*連結的客戶 Bug 要求：* <https://connect.microsoft.com/SQLServer/feedback/details/2333670/ssms-is-showing-the-wrong-number-of-maximum-automatic-failover-targets/>  
    
* **修正 SSMS Web 安裝程式中的 Bug，以修正影響安裝的錯誤。**  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2181548/sql-server-2016-ctp-3-2-management-studio-setup/>  
    
* **修正 SSMS 預覽版本中的 Bug，以允許在 SQL Server 2012 及較早版本上儲存維護計畫。**  
      
* **修正備份精靈中的 Bug，以允許對等量備份使用自訂多重備份名稱，以及在選取儲存體認證後輸入新名稱時，顯示正確的備份檔案名稱。**  
  
---  
## <a name="ssms-february-2016-preview"></a>SSMS 2016 年 2 月預覽 
版本號碼：13.0.12000.65
  
* **改進活動監視器，以在 SSMS 啟用高對比設定時顯示文字選項。**  
  
* **改進 Always Encrypted 精靈對話方塊，以在資料行的定序會於加密程序期間變更時顯示警告。**  
  
* **改進原則管理，以新增在資料行加密金鑰、資料行加密金鑰值，以及資料行主要金鑰上建立條件的支援。**  
  
* **Bug 修正，以改進 Always Encrypted 主要金鑰清除對話方塊及 Always Encrypted 錯誤訊息的可用性。**  
  
* **Bug 修正，以在只存在單一金鑰的情況下停用 Always Encrypted 資料行主要金鑰輪替。**  
  
* **修正以 SSMS 1 月版本或搭配 SQL Server RC0 媒體的 SSMS 版本啟動 [Always Encrypted] 對話方塊時，造成「型別初始設定式」錯誤的 Bug。**  
  
---  
## <a name="ssms-january-2016-preview"></a>SSMS 2016 年 1 月預覽 
版本號碼：13.0.11000.78 
  
* **Bug 修正，在 SSMS 中允許刪除擴充的事件 (XEvent) 工作階段。**  
  
* **Bug 修正，開啟 SQL Server 2014 可用性群組的屬性對話方塊。**  
 *連結的客戶 Bug 要求：*  
 <https://connect.microsoft.com/SQLServer/feedback/details/1609719/>  
     
* **Bug 修正，啟用將 Azure 複本新增至可用性群組的功能。**  
 *連結的客戶 Bug 要求：*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2029135/>  
     
* **Bug 修正，開啟 SQL Server 2014 資料庫的屬性對話方塊。**  
 *連結的客戶 Bug 要求：*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2080209/>  
     
* **Bug 修正，連接到 Azure SQL 資料庫時，移除為每個資料表顯示的重複資料行。**  
 *連結的客戶 Bug 要求：*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2103116/>  
---  
## <a name="ssms-december-2015-preview"></a>SSMS 2015 年 12 月預覽 
版本號碼：13.0.900.73
  
* **改進執行程序表比較功能，以便在目前的查詢執行計畫與已儲存於檔案中的查詢執行計畫之間進行比較。**  
  
* **改進 IntelliSense 支援，允許在 SSMS 中使用內嵌資料行存放區索引。**  
  
* **修正 [擴充事件工作階段精靈] 的 Bug，允許在連接到 Azure V12 伺服器時選取範本。**  
  
* **在 [安全性] 資料夾下的 [建立稽核] 和 [新增登入] 新增定位停駐點，讓鍵盤瀏覽更加輕鬆。**  
  
* **Bug 修正，以在 SSMS 設為以方格形式呈現結果時，提供 [查詢執行後切換到結果索引標籤] 功能。**   
 *連結的客戶 Bug 要求：*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1390296/switch-to-results-tab-after-query-execution-grid-mode-in-ssms-2016>  
  
* **Bug 修正，以在 SSMS 設為以方格形式呈現結果時，顯示未截斷的資料行標頭。**  
 *連結的客戶 Bug 要求：*  
  <https://connect.microsoft.com/SQLServer/feedback/details/2004111/bugbash-column-headers-in-grid-mode-truncated-with-courier-new-8>  
      
* **Bug 修正，使得 SSMS Web 安裝程式能夠正常安裝。**  
 *連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2003865/ssms-october-preview-incoherent-error-message>  
<https://connect.microsoft.com/SQLServer/feedback/details/2079557/unable-to-instal-sql-server-update-13-0-800-111-over-13-0-700-242-error-code-2711>  
  
---  
## <a name="ssms-november-2015-preview"></a>SSMS 2015 年 11 月預覽
版本號碼：13.0.800.111
  
* **適用於 SSMS 中高 DPI 顯示器點的陣圖縮放支援。**  
  
* **AlwaysEncrypted 對話方塊及精靈的使用者介面改善功能，用以簡化建立資料庫加密金鑰的程序。**  
  
* **活動監視器中「處理序」清單中新的右鍵操作功能表選項，用以檢視即時查詢統計資料。**  
  
* **Bug 修正，用以適當地將用戶端電腦上的 SSMS 預覽版本解除安裝。**  
  *連結的客戶 Bug 要求：*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1868474/ssms-2016-preview-can-be-installed-but-not-uninstalled>  
  
* 錯誤修正，以允許在檔案遺漏時仍能編輯 SQL Job Agent 的作業步驟。  
  *連結的客戶 Bug 要求：*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
    <https://connect.microsoft.com/SQLServer/feedback/details/1502100/ssms-preview-error>  
      
* **在 Azure 虛擬機器中執行的資料庫中，「擴充事件工作階段」的「檢視目標資料」功能表選項中的 Bug 修正。**  
  *連結的客戶 Bug 要求*：  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
***  

## <a name="ssms-october-2015-preview"></a>SSMS 2015 年 10 月預覽 
版本號碼：13.0.700.242  
* **新增現代化輕量型 Web 安裝程式，簡化了 SSMS 的下載與安裝程序。**  
  
* **新增 Always Encrypted 資料行加密精靈，允許在用戶端為選取的資料行加密及解密。**  
  
* **新增資料行主要金鑰 (CMK) 輪換對話方塊，可用於 Always Encrypted 資料庫，簡化了輪換加密金鑰來確保資料安全的程序。**  
  
* **新增延伸資料庫監視器，可讓您監視資料移轉到 Azure 雲端的狀態，並為其疑難排解。**  
  
* **彈性資料庫精靈可讓您選擇不在預設 Microsoft Azure 訂用帳戶中的 Microsoft Azure 伺服器。**  
  *連結的客戶 Bug 要求：*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1687063/cannot-choose-from-multiple-microsoft-azure-subscriptions>  
* **Bug 修正，以在 SSMS 中正確地顯示即時執行計畫。**  
  *連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/1774446/viewing-live-execution-plan-from-activity-monitor-crashes-ssms>    
* **修正 Bug 以移除資料庫快照集之 SSMS 指令碼中的無效選項**  
  *連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/1515168/ssms-scripting-of-database-snapshots-includes-invalid-options>  
* **修正查詢資料存放區 UI 中的 Bug，以便能在 [最耗用資源的查詢] 窗格中顯示詳細資料。**  
  *連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/1737185/sql-server-2016-overall-resource-consumption-query-store-pane-issue>  
***  

## <a name="ssms-september-2015-preview"></a>SSMS 2015 年 9 月預覽 
版本號碼：13.0.600.65  
* **新增防火牆規則對話方塊，以簡化連接到 Azure SQL 資料庫的程序。**      
    
* **更新 [新索引] 對話方塊，讓即使在已有叢集資料行存放區索引的情況下，也能建立非叢集資料列存放區索引。SQL 2016 及更新版本才提供此功能。**      
  *連結的客戶 Bug 要求：*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1552617/creation-of-nc-index-when-clustered-columnstore-index>  
      
* **修正 Bug 以便能在 Windows 7 上執行之 SSMS 預覽版中，檢視及編輯 SQL Agent 作業步驟。**      
  *連結的客戶 Bug 要求：*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1548140/cannot-view-or-edit-any-sql-agent-job-step>、    
  <https://connect.microsoft.com/SQLServer/feedback/details/1626895/unable-to-load-dll-dts>、    
  <https://connect.microsoft.com/SQLServer/feedback/details/1576662/error-creating-new-job-step>     
      
* **修正 Bug 以在 SQL Server 2014 及更新版本的 SSMS 中顯示觸發程序節點。**      
  *連結的客戶 Bug 要求：*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1617533/trigger-node-missing>   
      
* **修正資料庫與伺服器標準報表用者介面中的 Bug，以排除標頭中的版本資訊。**      
  *連結的客戶 Bug 要求：*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1387471/report-headings-wrongly-named>  
      
* **修正 Bug，以避免即時查詢統計資料節點在未完成時顯示為已完成。**      
  *連結的客戶 Bug 要求：*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1589096/live-query-statistics-node-shows-as-completed>  
  
***      
## <a name="ssms-august-2015-preview"></a>SSMS 2015 年 8 月預覽 
版本號碼：13.0.500.53
  
* **更新物件總管，以降低載入大量資料庫時的延遲。**  
  
* **改進 Windows 10 電腦上的安裝 SSMS。**  
  
* **更新及修正 SQL Server 組態管理員及 SSMS 使用者報表介面中的 Bug**    
***  
  
## <a name="ssms-july-2015-preview"></a>SSMS 2015 年 7 月預覽
版本號碼：13.0.400.91
  
* **Azure SQL Database (V12) 的資料庫圖表。**  
  
* **改進新暫時資料表語法的 IntelliSense 支援。**  
  
* **更新的 DacFx 程式庫，以支援最新的 Azure SQL 資料庫功能，包括資料列層級安全性及 Azure Active Directory 驗證。**  
  
* **修正 Bug (更新 [檢查更新] UI、修正 [相容性層級] 清單中的 UI 等等)。**  
***  
  
## <a name="ssms-june-2015-preview"></a>SSMS 2015 年 6 月預覽 
版本號碼：13.0.300.44
  
* **新增 SSMS 輕量級 Web 安裝程式。**  
  
* **自動檢查更新。**  
  
* **SSMS 現在也可為 Azure SQL Database (V12) 提供全文檢索搜尋支援。**  
  
* **解決了最多客戶提出的要求：**  
  * 允許在物件總管中對資料表與檢視表執行 [編輯前 200 個資料列]。  
  * Azure SQL Database (V12) 現已可使用資料表設計工具。  
  * Azure SQL database (V12) 現在也有資料庫與資料表屬性對話方塊。  
    
 * **新增選項以略過儲存 T-SQL 檔案的提示。**  
   
 * **為新的 Azure SQL Database 服務層 (基本、標準、進階) 提供匯入/匯出精靈支援。**  
   
 * **許多 Bug 修正 (指令碼案例、允許 SQL 資料庫啟用變更追蹤等等)。**   
     
  
  
  
  
  
  
    

