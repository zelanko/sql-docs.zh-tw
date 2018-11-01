---
title: SQL Server 2019 版本資訊 | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2018
ms.prod: sql-server-2018
ms.reviewer: ''
ms.technology:
- server-general
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: e7c4447ce03c25eab91e62c03540906d29714d7f
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419095"
---
# <a name="sql-server-2019-preview-release-notes"></a>SQL Server 2019 預覽版版本資訊

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文描述 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Community Technology Preview (CTP) 版本的限制和已知問題。 如需相關資訊，請參閱：
- [SQL Server 2019 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 預覽版本可供您體驗即將推出版本的功能。 它們不支援或授權用於生產環境。 明確不支援下列情節：
>
> - 與其他版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 並存安裝
> - 解除安裝
> - 從舊版 SQL Server 升級

**請試用 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]！**
- [![從評估中心下載](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=862101) [下載 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 以安裝於 Windows](http://go.microsoft.com/fwlink/?LinkID=862101)
- 安裝於 Linux for [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md)、[SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 和 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)。
- [在 Docker 的 SQL Server 2019 上執行](../linux/quickstart-install-connect-docker.md)。

## <a name="ctp-20-september-2018"></a>CTP 2.0 (2018 年 9 月)

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 是第一個公用版本的 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]。

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 僅提供評估版。 沒有其他可用版本。 安裝媒體隨附的 license_Eval.rtf 中會描述 CTP 2.0 支援。

在下列其中一個位置可以找到有限支援：

- 論壇
  - [SQL Server 意見反應](http://aka.ms/sqlfeedback)
  - [SQL Server 使用者入門](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [SQL Server 文件](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- 或具有 [#sqlhelp](https://twitter.com/search?q=%23sqlhelp) 的推文 [@SQLServer](http://twitter.com/SQLServer)

### <a name="documentation-ctp-20"></a>文件 (CTP 2.0)

- **問題和對客戶的影響**︰SQL Server 2019 (15.x) 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 文件集。 文中專門針對 SQL Server 2019 (15.x) 的內容會以**適用於**來標示。

- **問題和對客戶的影響**：可以依版本篩選 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文件。 使用每個文件頁面左上方控制項來篩選您的需求。 

- **問題和對客戶的影響**︰沒有 SQL Server 2019 (15.x) 可用的離線內容。

### <a name="hardware-and-software-requirements"></a>硬體與軟體需求

- **問題和對客戶的影響**：仍然會檢閱硬體和軟體需求，而且不是產品版本的最終需求。

  - **硬體**
    - [Windows - 處理器、記憶體和作業系統需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - 系統需求](../linux/sql-server-linux-setup.md#system)
  - **軟體**
    - Windows Server 2016 或更新版本。 如需其他需求，請參閱[安裝 SQL Server 的需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - 針對 Linux，請參閱 [Linux - 支援的平台](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="sql-graph"></a>SQL Graph

**問題和對客戶的影響**：與 DacFx 相依的工具 (例如匯入-匯出) 將不適用於新圖形功能，亦即邊緣條件約束或合併 DML。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的指令碼可能無法運作。

**因應措施**：將會撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼，並使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 SQLCMD 針對伺服器執行它們。 匯出或匯入可建立邊緣條件約束的資料庫物件具有新合併 DML 語法，或將無法在圖形物件上建立衍生資料表/檢視表。 使用者必須使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼，在其資料庫中手動建立這類物件。 

**適用對象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0。

### <a name="utf-8-collations"></a>UTF-8 定序

**問題和對客戶的影響**：啟用 UTF-8 的定序不能與一些其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能搭配使用。 使用下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能時不支援 UTF-8：

- SQL Server 複寫
- 連結的伺服器
- 記憶體內部 OLTP
- Polybase 的外部資料表

  另請注意，在 Azure Data Studio 或 SSDT 中，目前沒有 UI 支援可選擇啟用 UTF-8 的定序。 最新 SSMS 版本支援在 UI 中選擇啟用 UTF-8 的定序。

**因應措施**：沒有 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 的因應措施。

**適用對象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0。

### <a name="lightweight-query-profiling-infrastructure"></a>輕量型查詢分析基礎結構

**問題和對客戶的影響**：執行命令 `ALTER DATABASE SCOPED CONFIGURATION SET LIGHTWEIGHT_QUERY_PROFILING = ON` 會傳回語法錯誤。 任何取決於執行此命令的情節都會失敗。

> [!NOTE]
> 目前，無法在個別資料庫層級控制輕量型查詢分析基礎結構 (LWP)，而且根據預設，針對所有資料庫，它都會保持已啟用。 如需 LWP 的詳細資訊，請參閱 [SQL Server 2019 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

**因應措施**：沒有 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 的因應措施。

**適用對象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0。

### <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted

**問題和對客戶的影響**：豐富計算會暫止數個效能最佳化 (包含無編製索引等這類有限功能)，而且目前預設會予以停用。

**因應措施**：若要啟用豐富計算，請執行 `DBCC traceon(127,-1)`。 如需詳細資料，請參閱[啟用豐富計算](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

**適用對象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0。

### <a name="sql-server-integration-services-ssis-transfer-database-task"></a>SQL Server Integration Services (SSIS) 傳送資料庫工作

**問題和對客戶的影響**：`Transfer Database Task` 設定為以 `Database Online` 模式傳送資料庫時，可能會因下列錯誤而失敗：

>工作上的 Execute 方法已傳回錯誤碼 0x80131500 (傳輸資料時發生錯誤。 如需詳細資料，請參閱內部例外狀況)。 Execute 方法必須成功，並使用 "out" 參數表示結果。

**因應措施**：在伺服器上執行 `DBCC TRACEON (7416,-1)`並重試。

### <a name="sql-server-machine-learning-services-installation-failure"></a>SQL Server 機器學習服務安裝失敗

**問題/客戶影響**：在與主要網域具有信任關係問題的機器上，SQL Server 機器學習服務安裝會失敗。 在此情況下，會在記錄檔中出現下列錯誤：
 
>  Error: 0 : System.SystemException:The trust relationship between this workstation and the primary domain failed at System.Security.Principal.NTAccount.TranslateToSids(IdentityReferenceCollection sourceAccounts, Boolean& someFailed) ...

確認記錄檔位於：

* `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.log`
* `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\rxLibs\RegisterRExt.log`
**因應措施**：解決網域信任問題，然後重試安裝。

**適用對象**：SQL Server 2019 CTP 2.0。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
