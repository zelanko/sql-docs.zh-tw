---
title: "下載 SQL Server Management Studio (SSMS) | Microsoft Docs"
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
caps.latest.revision: "145"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 550f91939f2ab6b8e16455a6a5dea2a4ac519c5d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="download-sql-server-management-studio-ssms"></a>下載 SQL Server Management Studio (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] SSMS 是整合式環境，用於管理任何 SQL 基礎結構，從 SQL Sever 到 SQL Database 皆適用。 SSMS 提供工具來設定、監視和管理 SQL 執行個體。 使用 SSMS，即可部署、監視和升級應用程式所使用的資料層元件，以及建置查詢和指令碼。

使用 SQL Server Management Studio (SSMS)，即可查詢、設計與管理資料庫和資料倉儲，而不論它們位在何處：本機電腦上，或雲端中。

**SSMS 是免費的！**

SSMS 17.x 是最新一代的 *SQL Server Management Studio*，並提供 SQL Server 2017 的支援。

**[![下載](../ssdt/media/download.png) 下載 SQL Server Management Studio 17.3](https://go.microsoft.com/fwlink/?linkid=858904)**

**[![下載](../ssdt/media/download.png) 下載 SQL Server Management Studio 17.3 升級套件 (從 17.x 升級至 17.3)](https://go.microsoft.com/fwlink/?linkid=858906)**

SSMS 17.x 安裝不會升級或取代 SSMS 16.x 版或更早版本。 SSMS 17.x 會與舊版本並存安裝，讓兩個版本同時可供使用。
如果電腦包含 SSMS 並存安裝，請確認已針對您的特定需求啟動正確的版本。 最新版本會標上 Microsoft SQL Server Management Studio 17，並且具有新的圖示： 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> SQL Server PowerShell 模組現在透過 PowerShell 資源庫個別安裝。  如需詳細資訊，請參閱[下載指示](download-sql-server-ps-module.md)。

## <a name="sql-server-management-studio"></a>Transact-SQL

**版本資訊**

版本號碼：17.3

此版本的組建編號：14.0.17199.0

## <a name="new-in-this-release"></a>此版本中的新功能

SSMS 17.3 是 SQL Server Management Studio 的最新版本。 17.x 世代的 SSMS 幾乎支援 SQL Server 2008 到 SQL Server 2017 的所有功能領域。 17.x 版也支援 SQL Analysis Service PaaS。

17.3 版包括：

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

SQL Server Management Studio 17.3：<br>
[中文 (中華人民共和國)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [中文 (台灣)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)

SQL Server Management Studio 17.3 升級套件 (從 17.x 升級至 17.3)：<br>
[中文 (中華人民共和國)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x804) | [中文 (台灣)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40a)

## <a name="release-notes"></a>版本資訊

以下是這個 17.3 版本的問題和限制：

**一般 SSMS**

- 使用具 MFA 之 UA 的 Azure AD 驗證不支援下列 SSMS 功能：
   - Azure AD 驗證不支援 Database Engine Tuning Advisor；有一個已知問題，其向使用者呈現的錯誤訊息不太容易了解：「無法載入檔案或組件 'Microsoft.IdentityModel.Clients.ActiveDirectory'…」 而不是預期的「Database Engine Tuning Advisor 不支援 Microsoft Azure SQL Database (DTAClient)」。
- 嘗試分析 DTA 中的查詢會導致錯誤：「物件必須實作 IConvertible (mscorlib)」。
- 物件總管中報表的 [查詢存放區] 清單遺漏「迴歸查詢」。
   - 因應措施：以滑鼠右鍵按一下 [查詢存放區] 節點，然後選取 [檢視迴歸查詢]。

**Integration Services (IS)**

- [catalog].[event_messagea] 中的 [execution_path] 不是 Scale Out 中正確的套件執行路徑。[execution_path] 會以 “\Package” 開頭，而不是套件可執行檔的物件名稱。 在 SSMS 中檢視套件執行的概觀報表時，[執行概觀] 中 [執行路徑] 的連結無法運作。 因應措施是按一下概觀報表中的 [檢視訊息] 以檢查所有事件訊息。



## <a name="previous-releases"></a>舊版

[先前 SQL Server Management Studio 版本](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>意見反應

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 用戶端工具論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 記錄問題或建議](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>另請參閱

- [教學課程：SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 文件](sql-server-management-studio-ssms.md)
- [其他的更新與 Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
