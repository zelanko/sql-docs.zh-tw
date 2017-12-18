---
title: "SQL Server Management Studio - 變更記錄 (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 10/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: "72"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: dde2d7831a7bc75f9873efedcddb0bf6134669d9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 本文提供目前版本和舊版本之 SSMS 的更新、改善和 Bug 修正詳細資料。 下載[下面的舊版 SSMS](#previous-ssms-releases)。


## <a name="ssms-173download-sql-server-management-studio-ssmsmd"></a>[SSMS 17.3](download-sql-server-management-studio-ssms.md)
正式運作 | 組建編號：14.0.17199.0

### <a name="enhancements"></a>功能增強

- 已新增 [匯入一般檔案精靈]，其使用智慧型架構來簡化 CSV 檔案的匯入體驗，需要最少使用者介入或專業領域知識。 如需詳細資料，請參閱[匯入一般檔案至 SQL 精靈](../relational-databases/import-export/import-flat-file-wizard.md)。
- 已將 [XEvent Profiler] 節點新增至物件總管。 如需詳細資料，請參閱[使用 SSMS XEvent Profiler](../relational-databases/extended-events/use-the-ssms-xe-profiler.md)。
- 已更新效能儀表板等候歷程記錄報表中的等候篩選和分類。
- 已新增 "Predict" 函式的語法檢查。
- 已新增外部程式庫管理查詢的語法檢查。
- 已新增外部程式庫管理的 SMO 支援。
- 已將 [啟動 PowerShell] 支援新增至 [已註冊的伺服器] 視窗 (需要新的 SQL PowerShell 模組)。
- AlwaysOn：已新增對可用性群組的[唯讀路由支援](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)。
- 已將傳送追蹤詳細資料的選項新增至 [具 MFA 支援的 Active Directory - 通用] 登入的 [輸出] 視窗 (預設為關閉；需要在 [工具] > [選項] > [Azure 服務] > [Azure 雲端] > [ADAL 輸出視窗的追蹤層級] 下的 [使用者設定] 中開啟)。 
- 查詢存放區： 
  - 只要 QDS 已記錄任何資料，即使 QDS 處於 [關閉] 狀態，仍可存取 [查詢存放區] UI。
  - [查詢存放區] UI 現在會在所有現有的報表中公開等候分類。 這可讓客戶解除鎖定熱門等候查詢及更多案例。
- 已選擇性包括指令碼參數標頭 (預設為關閉；可在 [工具] > [選項] > SQL Server 物件總管 > [指令碼] > [包括指令碼參數標頭] 下的 [使用者設定] 中啟用)- [Connect 項目 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199)。
- 已移除 "RC" 商標。

### <a name="bug-fixes"></a>錯誤修正

**一般 SSMS**

- XEvent： 
   - 已修正 SSMS 只會開啟 .xel 檔案中部分事件的問題。
   - 已改善預設資料庫不是 'master' 時的「監看即時資料」體驗 - [Connect 項目 1222582](https://connect.microsoft.com/SQLServer/feedback/details/1222582)。
- AlwaysOn：已修正「還原記錄備份」可能因錯誤「這個備份組的記錄於 LSN x 結束，要套用到資料庫還太早」而失敗的問題。
- 作業活動監視器：已修正不一致的圖示 - [Connect 項目 3133100](https://connect.microsoft.com/SQLServer/feedback/details/3133100)。
- 查詢存放區︰已修正使用者無法針對查詢存放區報表選擇「自訂」日期範圍的問題。 已連結至下列 Connect 項目。
   - [Connect 項目 3139842](https://connect.microsoft.com/SQLServer/feedback/details/3139842)
   - [Connect 項目 3139399](http://connect.microsoft.com/SQLServer/feedback/details/3139399)
- 已修正連接對話方塊未「清除」最近使用之資料庫的問題；當儲存的資訊包含具名資料庫且使用者選取 <default> 時，就會發生此問題。
- 物件指令碼：
    - 已修正「產生資料庫指令碼」無法運作並擲回錯誤的問題；當使用者在伺服器上有已暫停的 DW 資料庫，但選取了另一個非 DW 資料庫並嘗試對其進行指令碼處理時，就會發生此問題。
    - 已修正指令碼預存程序的標頭不符合指令碼設定，而導致可能造成誤導之指令碼的問題 - [Connect 項目 3139784](http://connect.microsoft.com/SQLServer/feedback/details/3139784)。
    - 已重新啟用目標為 SQL Azure 物件時的「指令碼按鈕」。
    - 已修正 SSMS 不允許在某些物件 (UDF、檢視、SP、觸發程序) 上撰寫「改變」或「執行」指令碼的問題；當連接到 Azure SQL Database 時，就會發生此問題 - [Connect 項目 3136386](https://connect.microsoft.com/SQLServer/feedback/details/3136386)。
- 查詢編輯器：
  - 已改善目標為 Azure SQL Database 時的 IntelliSense。
  - 已修正查詢因驗證權杖 (通用驗證) 過期而失敗的問題。
  - 已改善針對 Azure SQL Database 使用時的 IntelliSense (特別是連接到 Azure SQL Database 時，將會使用最新的 T-SQL 文法 (140))。
  - 已修正開啟連接到伺服器上非 DataWarehouse 資料庫的查詢視窗，會導致該伺服器對 DataWarehouse 資料庫的所有後續查詢視窗擲回未支援類型/選項之各種相關錯誤的問題。
- 一律開啟：
   - 已將植入模式資料行新增至 AlwaysOn 儀表板和 AG 屬性頁面。
   - 已修正主要在 Windows 上時無法建立 Linux AG 的問題 - [Connect 項目 3139856](https://connect.microsoft.com/SQLServer/feedback/details/3139856)。
- 已修正執行查詢時 SSMS 中的數種「記憶體不足」問題 - [Connect 項目 2845190](https://connect.microsoft.com/SQLServer/feedback/details/2845190)、[Connect 項目 3123864](https://connect.microsoft.com/SQLServer/feedback/details/3123864)。
- Profiler： 
   - 已修正目標為 SQL 2005 時 Profiler 無法運作的問題。
   - 已修正 Profiler 不允許 [信任伺服器憑證] 連接選項的問題。
- 活動監視器：已修正活動監視器在指向 Linux 上執行的 SQL Server 時無法運作的問題。
- 已修正 SMO 傳送類別無法傳送外部資料來源或外部檔案格式物件的問題，這些類型的物件現在應該可以正確地包含在傳送中。
- 已註冊的伺服器：
   - 已啟用 UA 伺服器的多伺服器查詢 (它將會嘗試對群組中的每部 UA 伺服器使用相同的權杖)。
- AD 通用驗證：
   - 已修正不支援 Azure AD 驗證的問題。
   - 已修正資料表/檢視表設計工具無法運作的問題。
   - 已修正 [選取前 1000 個資料列] 和 [編輯前 200 個資料列] 無法運作的問題。
- 資料庫還原：已修正還原作業在將檔案移至其他位置時省略路徑中最後一個資料夾的問題。
- 壓縮精靈：
   - 已修正為索引管理 [壓縮精靈] 的問題；已修正 [壓縮資料精靈] 在 SQL 2016 和舊版中遭中斷的問題。
        https://connect.microsoft.com/SQLServer/feedback/details/3139342
   - 已將 [壓縮精靈] 新增至 Azure 資料表和索引。
- 執行程序表： 
   - 已修正無法辨識 PDW 運算子的問題。
- 伺服器屬性：
   - 已修正無法修改伺服器處理器親和性的問題。


**Analysis Services (AS)**

- 已修正 [部署精靈] 的一些問題來支援表格式 1400 相容性層級模型和 Power Query 資料來源。
- 從命令列執行時，[部署精靈] 現在可以部署至 AS Azure。
- 在 AS Azure 中使用 Windows 驗證時，使用者現在會在物件總管中看到正確的使用者帳戶名稱。


### <a name="known-issues-in-this-173-release"></a>此 17.3 版本的已知問題：

**一般 SSMS**

- 使用具 MFA 之 UA 的 Azure AD 驗證不支援下列 SSMS 功能：
   - Azure AD 驗證不支援 Database Engine Tuning Advisor；有一個已知問題，其向使用者呈現的錯誤訊息不太容易了解：「無法載入檔案或組件 'Microsoft.IdentityModel.Clients.ActiveDirectory'…」 而不是預期的「Database Engine Tuning Advisor 不支援 Microsoft Azure SQL Database (DTAClient)」。
- 嘗試分析 DTA 中的查詢會導致錯誤：「物件必須實作 IConvertible (mscorlib)」。
- 物件總管中報表的 [查詢存放區] 清單遺漏「迴歸查詢」。
   - 因應措施：以滑鼠右鍵按一下 [查詢存放區] 節點，然後選取 [檢視迴歸查詢]。

**Integration Services (IS)**

- [catalog].[event_messagea] 中的 [execution_path] 不是 Scale Out 中正確的套件執行路徑。[execution_path] 會以 “\Package” 開頭，而不是套件可執行檔的物件名稱。 在 SSMS 中檢視套件執行的概觀報表時，[執行概觀] 中 [執行路徑] 的連結無法運作。 因應措施是按一下概觀報表中的 [檢視訊息] 以檢查所有事件訊息。


## <a name="previous-ssms-releases"></a>舊版 SSMS

按一下下列各節中的標題連結，以下載舊版 SSMS。

## <a name="downloadssdtmediadownloadpng-ssms-172httpsgomicrosoftcomfwlinklinkid854085"></a>![下載](../ssdt/media/download.png) [SSMS 17.2](https://go.microsoft.com/fwlink/?linkid=854085)
正式運作 | 組建編號：14.0.17177.0

### <a name="enhancements"></a>功能增強

- Multi-Factor Authentication (MFA)
  - 適用於具 Multi-Factor Authentication 的通用驗證 (具 MFA 的 UA) 的多使用者 Azure AD 驗證
  - 已針對具 MFA 的通用驗證新增使用者認證輸入欄位，以支援多使用者驗證。
- 連接對話方塊現在支援下列 5 種驗證方法：
  - Windows 驗證
  - SQL Server 驗證
  - Active Directory - 含 MFA 的通用支援
  - Active Directory - 密碼
  - Active Directory - 整合式

- DacFx 的資料庫匯入/匯出精靈現在可以使用具 MFA 的通用驗證。
- 如需 API 支援，請參閱 [IUniversalAuthProvider 介面](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)。
- 具 MFA 的 Azure AD 通用驗證所使用的 ADAL Managed 程式庫已升級至 3.13.9 版。
- 此外，提供的新 CLI 介面可支援 SQL Database 和 SQL 資料倉儲的 Azure AD 管理員設定。

 如需 Active Directory 驗證方法的詳細資訊，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) 和[設定適用於 SQL Server Management Studio 的 Azure SQL Database Multi-Factor Authentication](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)。

- 輸出視窗包含在展開 [物件總管] 節點期間所執行查詢的項目
- Azure SQL Database 的已啟用檢視表設計工具
- SSMS 中從物件總管編寫物件指令碼的預設指令碼選項已變更：
  - 以前，新安裝上的預設值是讓產生的指令碼以最新版的 SQL Server (目前為 SQL Server 2017) 為目標。
  - 在 SSMS 17.2 中，已新增一個新選項：[使指令碼設定與來源相符]。 設定為 True 時，產生的指令碼是以與從中編寫物件指令碼之伺服器相同的版本、引擎類型和引擎版本為目標。
  - [使指令碼設定與來源相符] 值預設為 *True*，讓新的 SSMS 安裝自動預設為一律將物件指令碼編寫成與原始伺服器相同的目標。
  - [使指令碼設定與來源相符] 值設定為 *False* 時，會啟用一般指令碼目標選項，並且運作方式與以前一樣。
    - 此外，所有指令碼選項都已移至其專屬區段：[版本選項]。 它們不再位於 [一般指令碼選項] 下方。

- [從 URL 還原] 中已新增國內雲端支援
- QueryStoreUI 報表現在支援來自 sys.query_store_runtime_stats 的其他計量 (RowCount、DOP、CLR 時間等)。
- Azure SQL Database 現在支援 IntelliSense
    - https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
- 安全性：連接對話方塊將會預設為不信任伺服器憑證，並要求加密 Azure SQL DB 連接
- Linux 上 SQL Server 支援的一般改善：
 - 已回復 Database Mail 節點
 - 解決其他路徑相關問題
 - 活動監視器更為穩定
 - [連接屬性] 對話方塊會顯示正確平台
- 效能儀表板伺服器報表現在可作為預設報表：
  - 可以連接至 SQL Server 2008 和較新版本。
  - 遺漏索引子報表使用計分來協助識別最有用的索引。
  - 歷程記錄等候統計資料子報表現在會彙總為類別的等候。 預設已篩選出閒置和睡眠等候。
  - 新的閂鎖歷史記錄子報表。
- 執行程序表節點搜尋允許在計畫屬性中搜尋。 輕鬆地尋找任何運算子屬性，例如資料表名稱。 在檢視計畫時使用此選項：
  - 以滑鼠右鍵按一下計畫，並按一下內容功能表中的 [尋找節點] 選項
  - 使用 CTRL+F


**Analysis Services (AS)**

- 在 SSMS 的 AS Azure 模型中，沒有電子郵件地址之使用者的新 AAD 角色成員選擇

**Integration Services (IS)**

- 已將新的資料行 ([已執行的計數]) 新增至 SSIS 的執行報表

### <a name="known-issues-in-this-release"></a>此版本的已知問題：

- 在開啟一小時之後嘗試執行查詢時，使用「具 MFA 支援的 Active Directory - 通用」驗證的查詢視窗可能會發生與下列類似的錯誤：

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of ConnectRetryCount to increase the number of recovery attempts.`

   重新執行查詢應該可更正錯誤並成功。

- 使用具 MFA 之通用驗證的 Azure AD 驗證不支援下列 SSMS 功能：
  - [新增資料表/檢視] 設計工具會顯示舊式登入提示，並不適用於 Azure AD 驗證。
  - [編輯前 200 個資料列] 功能不支援 Azure AD 驗證。
  - [已註冊的伺服器] 元件不支援 Azure AD 驗證。
  - 不支援 **Database Engine Tuning Advisor** 進行 Azure AD 驗證。 有一個已知問題，其向使用者呈現的錯誤訊息較無幫助：*無法載入檔案或組件 'Microsoft.IdentityModel.Clients.ActiveDirectory,…* 而不是預期的 *Database Engine Tuning Advisor 不支援 Microsoft Azure SQL Database。(DTAClient)*.

**Analysis Services (AS)**

- SSAS 中的物件總管不會在 AS Azure 連接內容中顯示「Windows 驗證」使用者名稱。

### <a name="bug-fixes"></a>錯誤修正

- 修正在嘗試列印查詢結果 (文字格式) 時的問題。  https://connect.microsoft.com/SQLServer/feedback/details/3055225/
- 修正 SSMS 在 SQL Azure Database 上編寫這類物件刪除指令碼時不正確地卸除資料表和其他物件的問題。
- 修正 SSMS 偶而因下列這類錯誤而拒絕啟動的問題：「找不到一或多個元件。 請重新安裝該應用程式」。
- 已修正 SSMS UI 中 SPID 無法取得過時及不同步的問題。https://connect.microsoft.com/SQLServer/feedback/details/1898875
- 修正將 /passive 引數視為 /quiet 的 SSMS (無訊息) 安裝程式問題。
- 修正 SSMS 偶而在啟動時擲回「物件參考未設定成物件的執行個體」錯誤的問題。 http://connect.microsoft.com/SQLServer/feedback/details/3134698
- 修正 [資料壓縮精靈] 上導致 SSMS 在 [圖形資料表] 上按 [計算] 時當機的問題
- 解決以滑鼠右鍵按一下資料表的索引 (透過慢速的網際網路連接) 時的效能問題。 https://connect.microsoft.com/SQLServer/feedback/details/3120783
- 修正 SSMS 無法在具有區分大小寫定序之伺服器上列舉備份檔案的問題。 http://connect.microsoft.com/SQLServer/feedback/details/3134787 和 https://connect.microsoft.com/SQLServer/feedback/details/3137000
- 執行程序表和執行程序表比較綜合修正
- 修正除非已在執行 SSMS 的電腦上安裝 SQL Server，否則 [連接] 對話方塊不允許使用者指定 [網路通訊協定] 用於連接的問題。 https://connect.microsoft.com/SQLServer/feedback/details/3134997
- 改善在「隨機」位置上顯示某個 SSMS 對話方塊的多監視器組態支援。 已在 [SQL Server 物件總管 | 命令] 使用者設定下新增選項 [工作對話方塊]，允許記住工作對話方塊或屬性工作表在關閉時的位置。 https://connect.microsoft.com/SQLServer/feedback/details/889169、https://connect.microsoft.com/SQLServer/feedback/details/1158271、https://connect.microsoft.com/SQLServer/feedback/details/3135260 
- 修正 SSMS 無法變更加密 Azure SQL DB 之 DB 內容的問題
- 改善 [執行之後捨棄結果] 選項。 https://connect.microsoft.com/SQLServer/feedback/details/1196581
- 改善/修正使用者無法存取他們不是系統管理員之 Azure 訂用帳戶的問題。
- 改善 [資料庫還原精靈] 以在 OE 中持續選取目標資料庫，不論是否選取來源資料庫。 https://connect.microsoft.com/SQLServer/feedback/details/3118581
- 修正物件總管未排序錯誤新增之「原生編譯的預存程序」的問題。 http://connect.microsoft.com/SQLServer/feedback/details/3133365
- 修正 [選取前 n 個資料列] 未包含 "TOP" 子句的問題。 適用於 Azure SQLDW。 https://connect.microsoft.com/SQLServer/feedback/details/3133551 和 https://connect.microsoft.com/SQLServer/feedback/details/3135874
- QueryStoreUI：修正非自訂時間間隔未正確地作用於所有報表的問題。
- Always Encrypted：
    - 改善 [新增資料行主要金鑰] 對話方塊中 AKV 權限狀態的傳訊
    - 將工具提示新增至 CEK 下拉式清單，以簡化可區別具有長名稱的 CEK
    - 修正未針對 [Always Encrypted] 將某些 CNG 金鑰存放區提供者顯示在 [新增資料行主要金鑰] 對話方塊中的問題
- 修正 SSMS 連接的不一致「應用程式名稱」。 http://connect.microsoft.com/SQLServer/feedback/details/3135115
- 修正 SSMS 未產生 SQL Azure 之正確指令碼的問題 (使用 DATA_COMPRESSIONS 選項的資料表和索引)。 https://connect.microsoft.com/SQLServer/feedback/details/3133148
- 修正問題：使用者無法使用 CTRL+Q 快速鍵進行快速啟動 (注意：在 [查詢編輯器] 中切換 [IntelliSense 已啟用] 選項的新按鍵繫結關係現在是 CTRL+B、CTRL+I)。 https://connect.microsoft.com/SQLServer/feedback/details/3131968
- 修正 [還原資料庫] 中 SSMS 在嘗試從具有已定義自訂網域之帳戶的訂閱中選取儲存體帳戶時擲回例外狀況的問題
- 修正 [資料庫圖表] 中 SSMS 擲回「索引在陣列的界限之外」錯誤的問題；而且，使用者無法將 [資料表檢視] 變更為任何項目，只能變更為標準。 https://connect.microsoft.com/SQLServer/feedback/details/3133792 和 http://connect.microsoft.com/SQLServer/feedback/details/3135326
- 修正 [備份/還原至 URL] 中 SSMS 未列舉傳統儲存體帳戶的問題。
- 修正嘗試將結構描述繫結安全性實體新增至 DB 角色時擲回例外狀況的問題。 https://connect.microsoft.com/SQLServer/feedback/details/3118143
- 修正 SSMS 間歇地顯示下列錯誤的問題：「資料為 Null。 無法在值為 Null 的情況下呼叫這個方法或屬性。」 展開資料表節點 http://connect.microsoft.com/SQLServer/feedback/details/3136283 時
- DTA：修正在評估具有特定界限值的資料分割函式時，DTAEngine.exe 因堆積損毀而終止的問題。


**Analysis Services (AS)**

- 修正 DB 的名稱和識別碼不同時，[AS 還原資料庫] 因錯誤而失敗的問題
- 修正導致 DAX 查詢視窗捨棄切換 [IntelliSense 已啟用] 之功能表選項的問題
- 修正避免透過 msmdpump IIS http/https 位址連接至 SSAS 的問題
- 允許使用包含分號的密碼連接至 AS Azure
- 與 SQL Server 2017 AS 伺服器或 AS Azure 搭配使用時，具有 [略過成員資格] 選項的 [正在產生 AS 還原資料庫的指令碼] 命令會包含新的對應 JSON 選項
- 修正導致刪除資料庫對話方塊在載入時引發錯誤的極罕見問題
- 修正嘗試檢視包含混用 SQL 查詢和 M 資料分割定義的 1400 相容性層級模型中的資料分割時可能發生的問題

**Integration Services (IS)**
- 修正無法顯示 SSISDB 目錄之執行資訊報表的問題
- 解決 SSMS 中大量專案/套件之效能不良的相關問題

## <a name="downloadssdtmediadownloadpng-ssms-171httpsgomicrosoftcomfwlinklinkid849819"></a>![下載](../ssdt/media/download.png) [SSMS 17.1](https://go.microsoft.com/fwlink/?linkid=849819)
正式推出 |組建編號： 14.0.17119.0

### <a name="enhancements"></a>功能增強

- 剖析工具：說明 > 關於現在會顯示發行版本號碼 (例如 17.1)
- 分析服務使用者可以從資料來源的內容功能表，針對 1200 TM 模型和更高版本重新整理其資料來源的認證
- 內建的 SSIS 報表現在顯示 CTP 2.1 中 SSIS 向外延展執行的記錄
- SSIS 向外延展管理應用程式
  - 檢視向外延展 master 的基本資訊。
  - 輕鬆地將背景工作角色加入向外延展部署。
  - 檢視所有的向外延展背景工作角色和基本相關資訊，也可以輕鬆地進行啟用或停用。

### <a name="bug-fixes"></a>錯誤修正
- 一律開啟：
  - 已修正下列問題：可用性複本的屬性一律顯示為 WSFC AG 的「自動容錯移轉」模式。
  - 已修正下列問題：更新可用性群組時，覆寫了唯讀的路由清單
- 永遠加密：已修正下列問題：產生的記錄檔遺漏了 DacFx 所產生的資訊。
- 執行程序表：已修正下列問題：UI 一律顯示自適性聯結運算子的實際聯結型別屬性。
- 安裝程式：
  - 已修正下列問題：SSMS 17.0 已在 Visual Studio 2013 上中斷 SSDT [連接項目 3133479]
  - 已修正下列問題：按一下安裝程式結尾處的 [重新啟動]，並不會重新啟動電腦
- 指令碼：藉由停用該選項，在嘗試指令碼刪除時防止 SSMS 意外刪除 Azure 資料庫物件。  正確的修復程式將位於即將發佈的 SSMS 版本中。
- 物件總管：已修正下列問題：連接至使用 "AS COPY" 建立的 Azure 資料庫時，「資料庫」節點未展開

## <a name="downloadssdtmediadownloadpng-ssms-170httpgomicrosoftcomfwlinklinkid847722"></a>![下載](../ssdt/media/download.png) [SSMS 17.0](http://go.microsoft.com/fwlink/?LinkID=847722)
正式運作 | 組建編號：14.0.17099.0

### <a name="enhancements"></a>功能增強 

- 升級封裝和 Windows Software Update Services (WSUS) 
    - 未來的 17.X 版包含較小的累積更新封裝 
  - 更新封裝也將發佈至 WSUS 目錄  
- 圖示更新
    - 圖示已更新為與 VS Shell 所提供圖示一致，且支援高 DPI 解析度
    - 新的 SSMS 和分析工具程式圖示，以區分 16.X 和 17.X 版本
- SQL PowerShell 模組
  - SQL Server PowerShell 模組已從 SSMS 中移除，現在是透過 PowerShell 資源庫 (目前需要有 PowerShell 5.0 才能支援模組版本設定) 提供
  - 針對某些 SMO 物件呈現方式 (格式化) 的其他改進 (例如，資料庫現在會顯示大小及可用空間，且資料表會顯示資料列計數和空間使用量)
  - 新增從 OE 中的 [啟動 PowerShell] 功能表叫用 PowerShell 命令提示字元時的顏色標示
  - 新增 -ClusterType 和 -RequiredCopiesToCommit 參數至 AG Cmdlet (New-SqlAvailabilityGroup、Join-SqlAvailabilityGroup 及 Set-SqlAvailabilityGroup Cmdlet)
  - 新增參數 -ActiveDirectoryAuthority 和 -AzureKeyVaultResourceId 至 Add-SqlAzureAuthenticationContext Cmdlet
  - 新增 Revoke-SqlAvailabilityGroupCreateAnyDatabase、Grant-SqlAvailabilityGroupCreateAnyDatabase 和 Set-SqlAvailabilityReplicaRoleToSecondary Cmdlet
  - 在 Set-SqlAvailabilityReplica 和 New-SqlAvailabilityReplica Cmdlet 中新增 -SeedingMode 參數
  - 在 Get-SqlDatabase 中新增 -ConnectionString 參數
- Linux 上的 SQL Server
    - 記錄傳送的一般改進和修正
  - 新增原生 Linux 路徑附加、還原和備份資料庫的支援
  - 新增原生 Linux 路徑對稽核記錄目的地資料夾的支援
- Analysis Services
  - XMLA 查詢視窗：
    - 編輯器中的括號匹配
    - DEFINE MEASURE 和 DEFINE VAR 語法支援
    - 各種 Intellisense 增強功能
  - 通用驗證
    - 允許使用者指定使用者名稱和任何密碼，而 [Azure 登入] 對話方塊會處理連線
  - SSMS PQ 整合： 
    - 結構化資料來源的指令碼可運作 
    - 在 PQ UI 中檢視及編輯結構化資料來源
- 新的「加入唯一條件約束」範本
- Showplan
    - 在已耗用時間的屬性視窗中顯示所有執行緒的最大值，而非加總
    - 公開新的記憶體授與運算子屬性
    - 啟用「即時查詢統計資料」中的 [編輯查詢] 按鈕
    - 支援交錯執行
  - [分析實際執行計畫] 的新選項
  - 執行程序表比較的一般增強功能
  - 執行程序表比較功能中引進了功能，以找出兩個查詢計劃的相符節點之間，基數估計的顯著差異，並執行可能根本原因的基本分析
- 移除「已註冊的伺服器總管」中的 [組態管理員]
- 啟用讀取來自 Azure Blob 儲存體的稽核記錄
- 為 Always Encrypted 新增參數化，如需詳細資料，請參閱[此頁面](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/) 
- 目標為 Azure SQL DB 的 AAD 通用驗證連線支援自訂租用戶識別碼 
- 為 Azure SQL Database 產生指令碼，現在可編寫全文、規則及資料庫指令碼
- 修正 SSMS 和 Profiler 啟動顯示畫面的商標
- 從 SSMS 移除公用程式控制點 UI
- SSMS 現在可以建立 "PremiumRS" 版本的 SQL Azure 資料庫
- AlwaysOn 可用性群組
  - 新增新叢集類型的支援：EXTERNAL 和 NONE
    - 新增 Linux 上的 SQL Server 支援
    - 新增自動植入作為初始資料同步處理的選項
    - 修正一些缺陷，例如端點 URL 處理、資料庫重新整理和 UI 配置
    - 移除 Azure 複本相關功能
  - 改進 IntelliSense 的數個可用性群組關鍵字
- 活動監視器
  - 在 [SSMS 輸出]視窗中新增新的 [活動監視器] 窗格
  - 變更連線錯誤/逾時訊息，將資訊記錄到輸出視窗，而不是快顯訊息
  - 移除 [概觀] 區段中的空白圖表 (第 5 個圖表)
  - 已暫停活動監視器資料收集時，在概觀標題中新增 (暫停)
  - SQL Server 的圖形延伸模組 
    - 圖形節點和邊緣資料表的新圖示
    - 圖形節點和邊緣資料表將會顯示在 [圖形資料表] 資料夾下方
    - 可建立圖形節點和邊緣資料表的範本
- 簡報模式
    - 3 個可透過快速啟動 (Ctr-Q) 使用的新工作
    - PresentOn - 開啟簡報模式
    - PresentEdit - 編輯簡報模式的簡報字型大小。  查詢編輯器的「文字編輯器字型」。  其他組件的「環境字型」。
    - RestoreDefaultFonts - 還原至預設設定。
    - *注意：目前沒有 PresentOff 命令。請使用 RestoreDefaultFonts 來關閉簡報模式*

### <a name="bug-fixes"></a>錯誤修正

- 修正透過 surfacebook 觸控板捲動執行程序表時 SSMS 當機的問題
- 修正 SSMS 在取得所還原或離線資料庫的屬性時，長時間停止回應的問題 
- 修正「說明檢視器」無法在 RC 組建中開啟的問題
- 修正 SSMS 中可能遺失「維護計畫工作工具箱」項目的問題。
- 修正 SSMS 中當資料庫名稱包含大括號時，使用者無法壓縮資料庫的問題。 [Connect 項目](https://connect.microsoft.com/SQLServer/feedback/details/3122618)
- 修正 SSMS 嘗試撰寫指令碼以刪除 Azure 資料庫時，實際上造成刪除資料庫本身的問題。 [Connect 項目](http://connect.microsoft.com/SQLServer/feedback/details/3131458/)
- 修正預設值沒有針對使用者定義資料表類型編寫指令碼的問題。 [Connect 項目](https://connect.microsoft.com/SQLServer/feedback/details/3119027)
- 針對索引上操作功能表的另一輪效能改進。 [Connect 項目](https://connect.microsoft.com/SQLServer/feedback/details/3120783)
- 修正當滑鼠游標暫留在執行計畫中的遺失索引上時，會造成過度閃爍的問題。 [Connect 項目](https://connect.microsoft.com/SQLServer/feedback/details/3118510)
- 修正 SSMS 在編寫指令碼時會使 DB 離線的問題 [Connect 項目](https://connect.microsoft.com/SQLServer/feedback/details/3118550)
- SSMS 當地語系化 (非英文) 版本的其他 UI 修正。
- 修正以 SQL 2016 SP1 Standard Edition 為目標時，[Always Encrypted 金鑰] 節點會遺失的問題。
- 永遠加密
    - 當以 SQL 2016 RTM Standard Edition 或任何 SQL 2014 (及以下) 伺服器為目標時，[Always Encrypted] 功能表會不正確地啟動
    - 修正當使用 CREATE OR ALTER 語法時，IntelliSense 會報告錯誤的問題
    - 修正當 CMK/CEK 中包含需要逸出 (以括弧括住) 的字元時，加密會失敗的問題
    - 當 SSMS 中出現「記憶體不足」例外狀況時，使用者會看到建議使用原生 (64 位元) PowerShell 的錯誤。
    - 修正當使用者使用資源群組管理員訂用帳戶，而不是使用傳統 Azure 訂用帳戶時，AE 精靈會失敗的問題
    - 修正當使用者在訂用帳戶中沒有任何權限或 Azure 金鑰保存庫時，AE 精靈會顯示不正確錯誤的錯誤。
    - 修正在 AE 精靈具有多個 AAD 的情況下，Azure 金鑰保存庫登入頁面不會顯示 Azure 訂用帳戶的問題
    - 修正在 AE 精靈中，Azure 金鑰保存庫登入頁面不會顯示使用者具有讀取權限之 Azure 訂用帳戶的問題
  - 修正目前可能不會載入資源檔，因此導致錯誤訊息不正確的問題
- 改進 SSMS 安裝頁面上超連結的對比
- 修正連線到 SQL Server Express (2016 SP1) 時不會顯示 Polybase 節點的問題
- 修正 SSMS 無法將 Azure 資料庫的 [相容性層級] 變更為 [v140] 的問題
- 改進 [物件總管] 在展開 Azure 資料庫清單時的效能 [Connect 項目 (英文)](https://connect.microsoft.com/SQLServer/feedback/details/3100675)
- 修正 [檢視 SQL Server 記錄檔] 操作功能表項目針對非關聯式伺服器類型 (AS\RS\IS) 會不正確顯示的問題 
- 修正使用 SQL 驗證檢查 Analysis Services 分割區查詢的語法時，可能會導致出現登入失敗訊息的問題
- 修正在 SSMS 中重新命名預覽 1400 相容性層級 AS 表格式模型會導致失敗的問題
- 修正在 AS 伺服器上嘗試無效作業之後，在罕見情況下可能會產生「模型上作業失敗」的問題，並在無法成功於模型上儲存之後還原本機變更
- 修正 [Analysis Services 同步處理資料庫] 快顯對話方塊中的錯字
- 在多個監視器安裝程式的畫面上，看不到備份/還原容器對話方塊。 
- 如果目標物件名稱中有 ]，SecurityPolicy 建立會失敗。
- SSMS 2016 [開啟最近使用的項目] 功能表未顯示最近儲存的檔案。 [Connect 項目](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)
- 移除 VS Shell 更新時，使用者設定的重設。
- 修正導致使用者無法在 SQL Server 2017 上變更資料庫相容性層級的問題。
- 使用 AAD 通用驗證的查詢視窗在一小時後無法重新整理查詢。
- 公用程式控制點 UI 已從 SSMS 移除。
- AD 通用驗證連線在初始權杖過期後無法查詢資料。
- 無法將 Rules from Azure SQL DB 編碼為 Azure SQL DB。
- 修正 SQL PowerShell 無法連接舊版 SQL 執行個體 (2014 及更早版本) 的問題。 [Connect 項目](https://connect.microsoft.com/SQLServer/feedback/details/1138754/sql-server-sqlps-powershell-module-fails-connection-to-sql-2012-instance)
- 修正在 SSMS 無法匯入註冊的伺服器時造成損毀的問題。
- 修正如果使用者有資料庫的特定權限，會造成 SSMS 損毀的問題。 
- SSMS - 在檢閱檢視時，資料表會從設計介面消失。 [Connect 項目](https://connect.microsoft.com/SQLServer/feedback/details/2946125/ssms-tables-disappears-from-design-surface-while-reviewing-views) 
- 資料表捲軸不允許使用者捲動資料表內容，只有向上/下箭號允許這個動作。 也有可能在嘗試使用捲軸捲動後，捲動資料表內容，而這是一項錯誤。 [Connect 項目](
http://connect.microsoft.com/SQLServer/feedback/details/3106561/sql-server-manager-2016-bug-in-design-view) 
- 註冊的伺服器在重新整理根節點後未顯示圖示。
- Azure v12 伺服器上 [建立資料庫] 的指令碼按鈕會執行指令碼，然後顯示訊息「沒有要編寫指令碼的動作」。
- SSMS [連接到伺服器] 對話方塊未清除每個新連線的 [其他屬性] 索引標籤。
- [產生工作] 指令碼未為 Azure SQL DB 產生 [建立資料庫] 指令碼。
- 檢視設計工具中的捲軸顯示為已停用。
- Always Encrypted AVK 金鑰路徑未包含版本識別碼。
- 減少查詢視窗中的引擎版本查詢數。 [Connect 項目](http://connect.microsoft.com/SQLServer/feedback/details/3113387)
- 未正確處理加密後來自重新整理模組的 Always Encrypted 錯誤。
- 將 OLTP 與 OLAP 的預設連線逾時從 15 秒變更為 30 秒，以修正略過連線的這類失敗。 
- 修正自訂報表啟動時，SSMS 中的損毀。 [Connect 項目](http://connect.microsoft.com/SQLServer/feedback/details/3118856)
- 修正 [產生指令碼...] 在 Azure SQL 資料庫失敗的問題。
- 修正 [編寫指令碼為] 及 [產生指令碼精靈]，不要在編寫預存程序等物件的指令碼時新增額外新行。 [Connect 項目](http://connect.microsoft.com/SQLServer/feedback/details/3115850)
- SQLAS PowerShell 提供者：將 LastProcessed 屬性新增到 Dimension 及 MeasureGroup 資料夾。 [Connect 項目](http://connect.microsoft.com/SQLServer/feedback/details/3111879)
- 即時查詢統計資料：修正其只顯示批次中第一個查詢的問題。 [連線項目] (http://connect.microsoft.com/SQLServer/feedback/details/3114221)  
- 執行程序表：在視窗中顯示執行緒的最大值，而非加總。
- 查詢存放區：對具有高執行變化的查詢新增報表。
- 物件總管效能問題：[Connect 項目](http://connect.microsoft.com/SQLServer/feedback/details/3114074)
    - 資料表的操作功能表會短暫停止回應
    - SSMS 在以右鍵按一下資料表索引時 (透過遠端 (網際網路) 連線) 很緩慢。 
    - 避免發行依伺服器排序的資料表查詢
- 從 SSMS 移除 Azure 部署精靈 (將資料庫部署到 Azure VM)
- 修正遺漏的索引未在 SSMS 中的執行計劃顯示的問題 [Connect 項目](http://connect.microsoft.com/SQLServer/feedback/details/3114194)
- 修正 SSMS 中常見的關機時當機問題
- 修正物件總管中，在 Polybase|向外延展群組節點上帶出操作功能表時發生錯誤的問題 [Connect 項目](http://connect.microsoft.com/SQLServer/feedback/details/3115128)
- 修正 SSMS 可能在嘗試顯示資料庫權限時損毀的問題
- 查詢存放區：在操作功能表項目中，為查詢存放區報表的結果方格進行一般功能增強
- 為現有資料表設定 Always Encrypted 失敗，不相關的物件發生錯誤。 [Connect 項目](http://connect.microsoft.com/SQLServer/feedback/details/3103181)
- 無法為具有多個結構描述的現有資料庫設定 Always Encrypted。 [連線項目] (http://connect.microsoft.com/SQLServer/feedback/details/3109591)
- Always Encrypted、加密資料行精靈失敗，原因是資料庫包含參考系統檢視的檢視。 [連接項目] (http://connect.microsoft.com/SQLServer/feedback/details/3111925)
- 使用 Always Encrypted 進行加密時，未正確處理加密後來自重新整理模組的錯誤。
- 修正 [新增伺服器註冊] 對話方塊上的 UI 截斷問題
- 修正 DMF 條件 UI 未正確更新其字串常值中有引號的運算式
- 修正執行自訂報表時可能造成 SSMS 損毀的問題
- 將 [向外延展中的執行...] 功能表項目 新增到資料夾節點
- 修正 Azure SQL DB 防火牆白名單 IP 地址功能的問題
- 修正 SSMS 中在編輯 AS 多維磁碟分割來源時，導致物件參考未設定例外狀況的問題
- 修正 SSMS 中從多維 AS 伺服器刪除客戶組件時，導致物件參考未設定例外狀況的問題
- 修正重新命名 AS 表格式 1400 資料庫失敗的問題
- 修正從 [連線屬性] 對話方塊中，為 1400 相容性層級 AS 表格式資料來源撰寫指令碼的問題
- 移除 AS 1400 相容性層級模型中的資料表至少有一個資料分割的假設
- Ctrl-R 現在可於 SSMS DAX 查詢編輯器中切換結果窗格


## <a name="downloadssdtmediadownloadpng-ssms-1653httpgomicrosoftcomfwlinklinkid840946"></a>![下載](../ssdt/media/download.png) [SSMS 16.5.3](http://go.microsoft.com/fwlink/?LinkID=840946)
正式運作 | 組建編號：13.0.16106.4

這個版本已修正下列問題：

* 修正 SSMS 16.5.2 中出現的問題，這造成 'Table' 節點會在資料表有多個疏鬆資料行時展開。

* 使用者可以將包含 OData 連線管理員且連線到 Microsoft Dynamics AX/CRM Online 資源的 SSIS 套件部署到 SSIS 目錄。 如需詳細資訊，請參閱 [OData 連線管理員](../integration-services/connection-manager/odata-connection-manager.md)。

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


## <a name="ssms-1651"></a>SSMS 16.5.1
正式運作 | 組建編號：13.0.16100.1

* 已修正 Invoke-Sqlcmd 在 CHECK 條件約束發生時錯誤插入多個資料列的問題。 [Microsoft Connect 項目：811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* 已修正建立可用性群組時，非英文語言版本運作不完全的問題。

* 已修正按一下查詢計劃 XML 未開啟適當 SSMS UI 的問題。


## <a name="downloadssdtmediadownloadpng-ssms-165httpgomicrosoftcomfwlinklinkid832812"></a>![下載](../ssdt/media/download.png) [SSMS 16.5](http://go.microsoft.com/fwlink/?LinkID=832812)
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


## <a name="downloadssdtmediadownloadpng-ssms-1641-september-2016httpgomicrosoftcomfwlinklinkid828615"></a>![下載](../ssdt/media/download.png) [SSMS 16.4.1 (2016 年 9 月)](http://go.microsoft.com/fwlink/?LinkID=828615)
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



## <a name="downloadssdtmediadownloadpng-ssms-163-august-2016httpgomicrosoftcomfwlinklinkid824938"></a>![下載](../ssdt/media/download.png) [SSMS 16.3 (2016 年 8 月)](http://go.microsoft.com/fwlink/?LinkID=824938)
正式推出 | 版本號碼：13.0.15700.28

* SSMS 的每月版本現在將以數值標註。

* [新驗證選項：「Active Directory 通用驗證」](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)。 這個一個由 Azure Active Directory 驅動的權杖型驗證機制，支援多因素、密碼及整合式驗證機制。

* 符合 SQL Server Profiler 範本的新擴充事件範本 [(Microsoft Connect 項目 #2543925)](../tools/sql-server-profiler/sql-server-profiler-templates.md)。

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
## <a name="downloadssdtmediadownloadpng-ssms-july-2016-hotfix-updatehttpgomicrosoftcomfwlinklinkid822301"></a>![下載](../ssdt/media/download.png) [SSMS 2016 年 7 月 Hotfix 更新](http://go.microsoft.com/fwlink/?LinkID=822301)
正式推出 | 版本號碼：13.0.15600.2

* 修正 SSMS 中的錯誤，以啟用遺失的右鍵功能表項目。  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect 項目 #2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect 項目 #2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016"></a>SSMS 2016 年 7 月 
正式推出 | 版本號碼：13.0.15500.91

* 編輯，7 月 5 日：改善 SQL Server 2016 (1200 相容性層級) 表格式資料庫在 [Analysis Services 處理] 對話方塊及 Analysis Services 部署精靈中的支援。

* 編輯，7 月 5 日：在 SSMS [查詢執行選項] 對話方塊中新增設定 'XACT_ABORT' 的選項。 此選項在這一版 SSMS 中會根據預設啟用，其指示 SQL Server 復原整個交易，並在執行階段錯誤發生時中止批次。

* 在 SSMS 中支援 Azure SQL 資料倉儲。

* SQL Server PowerShell 模組的重大更新。 這包括新的[SQL PowerShell 模組以及適用於永遠加密、SQL Agent 及 SQL 錯誤記錄檔的新 CMDLET](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update)。

* 支援在 [永遠加密精靈] 中產生 PowerShell 指令碼。

* 大幅改善 Azure SQL 資料庫的連線時間。

* 新的 [備份至 URL] 對話方塊支援為 SQL Server 2016 資料庫備份建立 Azure 儲存體認證。 此對話方塊讓在 Azure 儲存體帳戶中儲存資料庫備份的體驗更為簡化。
 
* 新增 [還原] 對話方塊以簡化從 Microsoft Azure 儲存體服務還原 SQL Server 2016 資料庫備份的作業。
 
* 修正 SSMS 查詢設計工具中的錯誤，讓沒有資料表 SELECT 權限的使用者也能將其加入設計工具中。

* 修正錯誤，以新增 'TRY_CAST()' 與 'TRY_CONVERT()' 函數的 IntelliSense 支援。  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast)。

* 修正 PowerShell 模組中的錯誤，以啟用 ‘SQLAS’ Analysis Services 延伸模組的載入。  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension)。

* 修正 SSMS 編輯器視窗中的錯誤，以允許用拖放方式開啟 SQL 檔案。  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios)。

* 修正 Profiler 中的問題，以修正結束時 Profiler 當機的情況  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2616550](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped)。  
[Microsoft Connect 項目 #2319968](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968)。

* 修正 SSMS 中的問題，以防止在嘗試編輯 SSMS 資料表設計工具中的加入連結時發生當機。  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2721052](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms)。

* 修正 SSMS 中的問題，允許 db_owner 角色成員產生資料庫指令碼  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june)。

* 修正 SSMS 編輯器中的問題，以移除在伺服器離線時關閉查詢索引標籤的延遲問題。  
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline)。

* 修正錯誤，以允許在 SQL Server Express 資料庫中使用 [備份] 選項。 
*連結的客戶 Bug 要求：*  
[Microsoft Connect 項目 #2801910](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks)。  
[Microsoft Connect 項目 #2874434](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance)。

* 修正 Analysis Services 的錯誤，為多維度 Analysis Services 模型正確顯示資料摘要提供者。

----
## <a name="downloadssdtmediadownloadpng-ssms-june-2016httpgomicrosoftcomfwlinklinkid799832"></a>![下載](../ssdt/media/download.png) [SSMS 2016 年 6 月](http://go.microsoft.com/fwlink/?LinkID=799832)
正式推出 | 版本號碼：13.0.15000.23

* SSMS 從 2016 年 6 月版本後將為正式推出。

* SSMS 中的新 [快速尋找] 對話方塊將能更好地與目前的文件整合，並允許透過規則運算式做出搜尋。 
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* 改進 SSMS 安裝程式，以允許您追蹤安裝進度，並透過指令碼處理自動安裝的結束代碼。

* 修正 SSMS 即時線上 F1 說明中的錯誤，以正確顯示說明文件和文章。

* 修正查詢資料存放區 [迴歸查詢] 檢視中，因捲動而造成 SSMS 當機的錯誤。

* 修正 Excel Analysis Services OLEDB 連接器中的錯誤，以允許從 Excel 2016 連線到 SQL Server Analysis Services。

* 修正 SSMS [連線] 對話方塊中的錯誤，以在使用多重監視器的系統時，於主要 SSMS 視窗所在的監視器上顯示 [連線] 對話方塊。  
*連結的客戶 Bug 要求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* 修正永遠加密體驗中的錯誤。 已修正 [永遠加密] 功能表選項沒有針對 Stretch Database 正確啟用的錯誤。 同時已修正永遠加密精靈沒有正確使用 SafeNet (Luna SA) HSM 提供者的錯誤。


## <a name="additional-downloads"></a>其他下載  
如需所有 SQL Server Management Studio 的下載清單，請搜尋 [Microsoft 下載中心](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending)。  
  
若要取得最新版的 SQL Server Management Studio，請參閱[下載 SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)。  
