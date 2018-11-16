---
title: SQL Server 2019 版本資訊 | Microsoft Docs
ms.date: 11/06/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 2c21ac917845b8162348b93fec3b868f1f748592
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51703856"
---
# <a name="sql-server-2019-preview-release-notes"></a>SQL Server 2019 預覽版版本資訊

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文描述 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Community Technology Preview (CTP) 版本的限制和已知問題。 如需相關資訊，請參閱：
- [SQL Server 2019 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 預覽版本可供您體驗即將推出版本的功能。 它們不支援或授權用於生產環境。 明確不支援下列情節：
>
> - 與其他版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 並存安裝
> - 從任何版本升級 SQL Server 的現有執行個體

**請試用 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]！**
- [![從評估中心下載](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [下載 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 以安裝於 Windows](https://go.microsoft.com/fwlink/?LinkID=862101)
- 安裝於 Linux for [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md)、[SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 和 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)。
- [在 Docker 的 SQL Server 2019 上執行](../linux/quickstart-install-connect-docker.md)。

## <a name="ctp-21-november-2018"></a>CTP 2.1 (2018 年 11 月)
[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 是 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的最新公開版本。

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 僅提供評估版。 沒有其他可用版本。 針對 CTP 2.1 的支援已在安裝媒體隨附的 license_Eval.rtf 中描述。

在下列其中一個位置可以找到有限支援：

- 論壇
  - [SQL Server 意見反應](https://aka.ms/sqlfeedback)
  - [SQL Server 使用者入門](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [SQL Server 文件](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- 或具有 [#sqlhelp](https://twitter.com/search?q=%23sqlhelp) 的推文 [@SQLServer](https://twitter.com/SQLServer)

### <a name="documentation-ctp-21"></a>文件 (CTP 2.1)

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
    - Microsoft .NET Framework 4.6.2。 可從[下載中心](https://www.microsoft.com/download/details.aspx?id=53344)取得。
    - 針對 Linux，請參閱 [Linux - 支援的平台](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="floating-point-results"></a>浮點結果

- **問題與對客戶的影響**：SQL Server 2019 預覽會使用更新的編譯器來建置 SQL Server。 在某些情況下，使用新編譯器編譯的程式碼可能會傳回與舊版 SQL Server 不同的浮點數值。 在未來的 CTP 中，行為變更將會被限制為新的相容性層級 (150)。

- **因應措施**：N/A

- **適用對象**：SQL Server 2019 CTP 2.1

### <a name="sql-server-integration-services-ssis-page-deployment-after-switching-db-to-single-user-mode-and-then-switching-back"></a>SQL Server Integration Services (SSIS) 頁面部署會在將 DB 切換至單一使用者模式，然後再切換回來之後發生

- **問題與對客戶的影響**：在將 SSISB 從單一使用者模式切換回多使用者模式之後，系統可能會在部署套件時報告下列錯誤：

  `Cannot continue the execution because the session is in the kill state.`

- **因應措施**：停止並重新啟動 SQL Server 執行個體，然後將 SSISDB 切換回多使用者模式。 

- **適用於**：SQL Server 2019 預覽 CTP 2.1


### <a name="udf-inlining"></a>UDF 內嵌 

- **問題與對客戶的影響**：目前存在針對使用者定義函數內嵌的巢狀呼叫不會正確驗證安全性的邊角案例。
  
- **因應措施**：針對這類 UDF 使用 `INLINE = OFF` 設定來停用 UDF 內嵌。

- **適用對象**：SQL Server 2019 CTP 2.1

### <a name="lightweight-query-profiling-infrastructure"></a>輕量型查詢分析基礎結構

- **問題和對客戶的影響**：執行命令 `ALTER DATABASE SCOPED CONFIGURATION SET LIGHTWEIGHT_QUERY_PROFILING = ON` 會傳回語法錯誤。 任何取決於執行此命令的情節都會失敗。

  > [!NOTE]
  > 目前，無法在個別資料庫層級控制輕量型查詢分析基礎結構 (LWP)，而且根據預設，針對所有資料庫，它都會保持已啟用。 如需 LWP 的詳細資訊，請參閱 [SQL Server 2019 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

- **因應措施**：沒有適用於 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 的因應措施。

- **適用對象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 和 CTP 2.0。

### <a name="utf-8-collations"></a>UTF-8 定序

- **問題和對客戶的影響**：啟用 UTF-8 的定序不能與一些其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能搭配使用。 使用下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能時不支援 UTF-8：

  - SQL Server 複寫
  - 連結的伺服器
  - 記憶體內部 OLTP
  - PolyBase 的外部資料表

    另請注意，在 Azure Data Studio 或 SSDT 中，目前沒有 UI 支援可選擇啟用 UTF-8 的定序。 最新 SSMS 版本支援在 UI 中選擇啟用 UTF-8 的定序。

- **因應措施**：沒有適用於 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 的因應措施。

- **適用對象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1、CTP 2.0。

### <a name="sql-graph"></a>SQL Graph

- **問題和對客戶的影響**：相依於 DacFx 的工具 (例如匯入-匯出) 將不適用於新的圖形功能，亦即邊緣條件約束或合併 DML。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的指令碼可能無法運作。

- **因應措施**：將會撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼，並使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 SQLCMD 針對伺服器執行它們。 匯出或匯入可建立邊緣條件約束的資料庫物件、具有新的合併 DML 語法，或在圖形物件上建立衍生資料表/檢視將無法運作。 使用者必須使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼，在其資料庫中手動建立這類物件。 

- **適用對象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1、2.0。

### <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted

- **問題和對客戶的影響**：豐富計算目前尚有數個效能最佳化 (包含無編製索引等有限功能) 處於擱置狀態，且目前預設會予以停用。

- **因應措施**：若要啟用豐富計算，請執行 `DBCC traceon(127,-1)`。 如需詳細資料，請參閱[啟用豐富計算](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

- **適用對象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1、2.0。

### <a name="sql-server-integration-service---fuzzy-lookup-transformation"></a>SQL Server Integration Services - 模糊查閱轉換

- **問題/對客戶的影響**：如果將模糊查閱轉換設定為重複使用索引，其將會失敗並顯示下列錯誤：

  `The specified delimiters do not match the delimiters used to build the pre-existing match index "...". This error occurs when the delimiters used to tokenize fields do not match. This can have unknown effects on the matching behavior or results.`

- **因應措施**：N/A

- **詳細資訊**：N/A  

- **適用對象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1

## <a name="ctp-20-september-2018"></a>CTP 2.0 (2018 年 9 月)

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 是第一個公用版本的 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]。

### <a name="sql-server-integration-services-ssis-transfer-database-task"></a>SQL Server Integration Services (SSIS) 傳送資料庫工作

- **問題和對客戶的影響**：`Transfer Database Task` 設定為以 `Database Online` 模式傳送資料庫時，可能會因下列錯誤而失敗：

  >工作上的 Execute 方法已傳回錯誤碼 0x80131500 (傳輸資料時發生錯誤。 如需詳細資料，請參閱內部例外狀況)。 Execute 方法必須成功，並使用 "out" 參數表示結果。

- **因應措施**：在伺服器上執行 `DBCC TRACEON (7416,-1)`並重試。

- **適用對象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
