---
title: "下載 SQL Server Management Studio (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安裝 ssms, 下載 ssms, 最新的 ssms"
- Transact-SQL
- ssms.exe
- sql man studio
- sql management studio
- sql management studio install
- download sql management studio
- ms sql management studio
- install sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 3f12671ace99d5fefc199c7b1c2db31e5b3cfade
ms.openlocfilehash: a689293fadb1a442f94d88cc06a9e7a4ef06650f
ms.contentlocale: zh-tw
ms.lasthandoff: 08/08/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>下載 SQL Server Management Studio (SSMS)

SSMS 是整合式環境，用於管理任何 SQL 基礎結構，從 SQL Sever 到 SQL Database 皆適用。 SSMS 提供工具來設定、監視和管理 SQL 執行個體。 使用 SSMS，即可部署、監視和升級應用程式所使用的資料層元件，以及建置查詢和指令碼。

使用 SQL Server Management Studio (SSMS)，即可查詢、設計與管理資料庫和資料倉儲，而不論它們位在何處：本機電腦上，或雲端中。

**SSMS 是免費的！**

SSMS 17.x 是最新一代的 *SQL Server Management Studio*，並提供 SQL Server 2017 的支援。

**[![下載](../ssdt/media/download.png) 下載 SQL Server Management Studio 17.2](https://go.microsoft.com/fwlink/?linkid=854085)**

**[![下載](../ssdt/media/download.png) 下載 SQL Server Management Studio 17.2 升級套件 (從 17.x 升級至 17.2)](https://go.microsoft.com/fwlink/?linkid=854087)**

SSMS 17.x 安裝不會升級或取代 SSMS 16.x 版或更早版本。 SSMS 17.x 會與舊版本並存安裝，讓兩個版本同時可供使用。
如果電腦包含 SSMS 並存安裝，請確認已針對您的特定需求啟動正確的版本。 最新版本會標上 Microsoft SQL Server Management Studio 17，並且具有新的圖示： 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> SQL Server PowerShell 模組現在透過 PowerShell 資源庫個別安裝。  如需詳細資訊，請參閱[下載指示](download-sql-server-ps-module.md)。

## <a name="sql-server-management-studio"></a>Transact-SQL

**版本資訊**

版本號碼：17.2 此版本的組建編號：14.0.17177.0

## <a name="new-in-this-release"></a>此版本中的新功能

SSMS 17.2 是 SQL Server Management Studio 的最新版本。 17.x 世代的 SSMS 幾乎支援 SQL Server 2008 到 SQL Server 2017 的所有功能領域。 17.x 版也支援 SQL Analysis Service PaaS。

17.2 版包括：

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
- 新的 CLI 介面支援 SQL Database 和 SQL 資料倉儲的 Azure AD 管理員設定。

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
- 安全性：連接對話方塊將會預設為不信任伺服器憑證，並要求加密 Azure SQL Database 連接
- Linux 上 SQL Server 支援的一般改善：
 - 已回復 Database Mail 節點
 - 解決一些與路徑相關的問題
 - 活動監視器穩定性改善
 - [連接屬性] 對話方塊會顯示正確平台
- 效能儀表板伺服器報表現在可作為預設報表：
  - 可以連接至 SQL Server 2008 和較新版本。
  - 遺漏索引子報表使用計分來協助識別最有用的索引。
  - 歷程記錄等候統計資料子報表現在會彙總為類別的等候。 預設已篩選出閒置和睡眠等候。
  - 新的閂鎖歷史記錄子報表。
- 執行程序表節點搜尋允許在計畫屬性中搜尋。 輕鬆地尋找任何運算子屬性，例如資料表名稱。 在檢視計畫時使用此選項：
  - 以滑鼠右鍵按一下計畫，並按一下內容功能表中的 [尋找節點] 選項
  - 使用 CTRL+F

如需完整變更清單，請參閱 [SQL Server Management Studio - 變更記錄 (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)。

如需使用者資料收集的資訊，請參閱 [SQL Server 隱私權聲明](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx)。

## <a name="supported-sql-offerings"></a>支援的 SQL 供應項目

* 此版本的 SSMS 適用於所有[支援的 SQL Server 2008 - SQL Server 2017 版本](https://support.microsoft.com/lifecycle?C2=1044)，並提供最高層級的支援以使用 Azure SQL Database 中最新的雲端功能，以及 Azure SQL 資料倉儲。
* SQL Server 2000 或 SQL Server 2005 並未受到明確限制，但有些功能可能無法正常運作。
* 此外，SSMS 17.x 可以與 SSMS 16.x 或 SQL Server 2014 SSMS 及更早的版本並存安裝。

## <a name="supported-operating-systems"></a>支援的作業系統
  
搭配最新推出的服務套件使用時，這一版 SSMS 支援下列 64 位元平台：
- Windows 10 (64 位元)
- Windows 8.1 (64 位元)
- Windows 8 (64 位元)
- Windows 7 (SP1) (64 位元)
- Windows Server 2016 *
- Windows Server 2012 R2 (64 位元)
- Windows Server 2012 (64 位元)
- Windows Server 2008 R2 (64 位元)

\* SSMS 17.X 以 Windows Server 2016 之前發行的 Visual Studio 2015 獨立模式 Shell 為基礎。 Microsoft 重視應用程式相容性，並確保已出貨的應用程式會持續在最新的 Windows 版本上執行。 為了將在 Windows Server 2016 上執行 SSMS的問題降至最低，請確定 SSMS 已套用所有最新的更新。 如果在 Windows Server 2016 上發生任何 SSMS 問題，請連絡支援服務。 支援小組會判斷問題是否與 SSMS、Visual Studio 或 Windows 相容性有關。 然後，支援小組會將問題傳送至適當的小組以進行進一步的調查。

## <a name="ssms-installation-tips-and-issues"></a>SSMS 安裝祕訣與問題

### <a name="minimize-installation-reboots"></a>最小化安裝重新開機

* 請採取下列動作，以降低 SSMS 安裝程式需要在安裝結束時重新開機的機會：
  * 請確定您執行的是最新版的 Visual C++ 2013 可轉散發套件。 需要 12.00.40649.5 版本 (或更新版本)。 只需要 x64 版本。
  * 請確認電腦上的 .NET Framework 版本是 4.6.1 (或更新版本)。
  * 關閉電腦上開啟的所有其他 Visual Studio 執行個體。
  * 請確定電腦上安裝了所有最新的作業系統更新。
  * 所述的動作通常只需要執行一次。 只有極少數的情況，需要在另外升級至相同主要版本的 SSMS 時重新開機。 針對次要升級，電腦上會安裝好所有的 SSMS 先決條件。

* 若要查看已知問題和解決方法的清單，請參閱 [SQL Server Management Studio - 版本資訊](../ssms/sql-server-management-studio-release-notes.md)。

## <a name="available-languages"></a>可用語言

> [!NOTE]
> 非英文的 SSMS 語言版本如果安裝在 Windows 8、Windows 7、Windows Server 2012 及 Windows Server 2008 R2，就需要 [KB 2862966 安全性更新程式封裝](https://support.microsoft.com/en-us/kb/2862966) 。

此版 SSMS 提供下列語言版本：

SQL Server Management Studio 17.2：<br>
[中文 (中華人民共和國)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [中文 (台灣)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

SQL Server Management Studio 17.2 升級套件 (從 17.x 升級至 17.2)：<br>
[中文 (中華人民共和國)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x804) | [中文 (台灣)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40a)

## <a name="release-notes"></a>版本資訊

以下是這個 17.2 版本的問題和限制：

- 在開啟大約一小時 (含) 以上之後嘗試執行查詢時，使用「具 MFA 支援的 Active Directory - 通用」驗證的查詢視窗可能會發生與下列類似的錯誤：

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of *ConnectRetryCount* to increase the number of recovery attempts.`

   重新執行查詢應該可更正錯誤並成功。

- 使用具 MFA 的通用驗證的 Azure AD 不支援下列 SSMS 功能：
  - [新增資料表/檢視] 設計工具會顯示舊式登入提示，並不適用於 Azure AD 驗證。
  - [編輯前 200 個資料列] 功能不支援 Azure AD 驗證。
  - [已註冊的伺服器] 元件不支援 Azure AD 驗證。
  - 不支援 **Database Engine Tuning Advisor** 進行 Azure AD 驗證。 有一個已知問題，其向使用者呈現的錯誤訊息較無幫助：*無法載入檔案或組件 'Microsoft.IdentityModel.Clients.ActiveDirectory,…* 而不是預期的 *Database Engine Tuning Advisor 不支援 Microsoft Azure SQL Database。(DTAClient)*.

**AS**

- SSAS 中的物件總管不會在 AS Azure 連接內容中顯示「Windows 驗證」使用者名稱。
如需詳細資訊，請參閱 [SSMS 變更記錄](sql-server-management-studio-changelog-ssms.md)。

## <a name="previous-releases"></a>舊版

[先前 SQL Server Management Studio 版本](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>意見反應

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 用戶端工具論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 記錄問題或建議](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>另請參閱

- [教學課程：SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 文件](sql-server-management-studio-ssms.md)
- [其他的更新與 Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

