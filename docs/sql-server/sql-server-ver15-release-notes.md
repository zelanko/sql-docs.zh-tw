---
title: SQL Server 2019 版本資訊 | Microsoft Docs
ms.date: 03/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 6336e6ebc549d1be2787bb8a100efec1ea9b6836
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492850"
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

## <a name="ctp-24"></a>CTP 2.4
[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4 是 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的最新公開版本。

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.3 僅提供評估版。 沒有其他可用版本。 CTP 版本的支援說明於安裝媒體隨附的 `license_Eval.rtf` 中。

在下列其中一個位置可以找到有限支援：

- 論壇
  - [SQL Server 意見反應](https://aka.ms/sqlfeedback)
  - [SQL Server 使用者入門](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [SQL Server 文件](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- 或具有 [#sqlhelp](https://twitter.com/search?q=%23sqlhelp) 的推文 [@SQLServer](https://twitter.com/SQLServer)

### <a name="documentation-ctp-24"></a>文件 (CTP 2.4)

- **問題和對客戶的影響**︰SQL Server 2019 (15.x) 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 文件集。 文中專門針對 SQL Server 2019 (15.x) 的內容會以**適用於**來標示。

- **問題和對客戶的影響**：可以依版本篩選 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文件。 使用每個文件頁面左上方控制項來篩選您的需求。

- **問題和對客戶的影響**︰SQL Server 2019 (15.x) 未提供任何離線內容。

### <a name="hardware-and-software-requirements-ctp-24"></a>硬體和軟體需求 (CTP 2.4)

- **問題和對客戶的影響**︰仍然會檢閱硬體和軟體需求，而且不是產品版本的最終需求。

  - **硬體**
    - [Windows - 處理器、記憶體和作業系統需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - 系統需求](../linux/sql-server-linux-setup.md#system)
  - **軟體**
    - Windows Server 2016 或更新版本。 如需其他需求，請參閱[安裝 SQL Server 的需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2。 可從[下載中心](https://www.microsoft.com/download/details.aspx?id=53344)取得。
    - 針對 Linux，請參閱 [Linux - 支援的平台](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="updated-compiler"></a>更新的編譯器

- **問題和對客戶的影響**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 是以更新的編譯器所建置。 CTP 2.1 有個已知的問題，由於更新編譯器的緣故，浮點數和其他轉換案例可能傳回與舊版不同的值。 CTP 2.2 內含可確保受影響案例傳回與舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 相同結果的運作。 截至 CTP 2.3 版本，並沒有發現任何其他問題。 如果發現與 [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] 相較之下有任何結果異常，請立即回報 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 小組](http://aka.ms/sqlfeedback)。

- **因應措施**：不適用

- **適用於**：SQL Server 2019 CTP 2.4、CTP 2.3、CTP 2.2、CTP 2.1

### <a name="utf-8-collations"></a>UTF-8 定序

- **問題和對客戶的影響**︰啟用 UTF-8 的定序不能與某些其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能搭配使用。 使用下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能時不支援 UTF-8：

  - 連結的伺服器
  - 記憶體內部 OLTP
  - PolyBase 的外部資料表
  - Always Encrypted

  > [!Note]
  > 在 Azure Data Studio 或 SQL Server Data Tools (SSDT) 中，目前沒有可選擇啟用 UTF-8 之定序的 UI 支援。 最新 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) 版本支援在 UI 中選擇啟用 UTF-8 的定序。
 
- **因應措施**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 沒有任何因應措施。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4、CTP 2.3、CTP 2.2、CTP 2.1、CTP 2.0。

### <a name="sql-graph"></a>SQL Graph

- **問題和對客戶的影響**︰相依於 DacFx 的工具 (例如匯入-匯出) 將不適用於新的圖形功能，亦即邊緣條件約束或合併 DML。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的指令碼可能無法運作。

- **因應措施**：可行方式是使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 SQLCMD 撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼，並對伺服器執行它們。 匯出或匯入可建立邊緣條件約束的資料庫物件、具有新的合併 DML 語法，或在圖形物件上建立衍生資料表/檢視將無法運作。 使用者必須使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼，在其資料庫中手動建立這類物件。 

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4、CTP 2.3、CTP 2.2、CTP 2.1、2.0。

### <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted

- **問題和對客戶的影響**︰豐富計算會暫止數個效能最佳化，包含有限功能 (無索引等)，而且目前根據預設會停用。

- **因應措施**：若要啟用豐富計算，請執行 `DBCC traceon(127,-1)`。 如需詳細資料，請參閱[啟用豐富計算](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4、CTP 2.3、2.2、CTP 2.1、2.0。

### <a name="system-dynamic-management-views"></a>系統動態管理檢視

- **問題和對客戶的影響**︰系統資料表值函式 [sys.dm_db_objects_disabled_on_compatibility_level_change](../relational-databases/system-dynamic-management-views/spatial-data-sys-dm-db-objects-disabled-on-compatibility-level-change.md) 會在 `dependency` 資料行傳回隨機值。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4、CTP 2.3。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
