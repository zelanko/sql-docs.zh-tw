---
title: SQL Server 2019 版本資訊 | Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 8f44927fb59e6d1b613b2a67e26aed980b3a080a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65993948"
---
# <a name="sql-server-2019-preview-release-notes"></a>SQL Server 2019 預覽版版本資訊
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文描述 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Community Technology Preview (CTP) 版本的限制和已知問題。 如需相關資訊，請參閱：
- [SQL Server 2019 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)

## <a name="ctp-30"></a>CTP 3.0

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0 是 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的最新公開版本。

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0 僅提供 Evaluation Edition。 沒有其他可用版本。 

如需完整的 CTP 版本支援和授權，請參閱 `license_Eval.rtf` 和您的安裝媒體。

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

## <a name="documentation"></a>文件集

- **問題和對客戶的影響**︰SQL Server 2019 (15.x) 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 文件集。 文中專門針對 SQL Server 2019 (15.x) 的內容會以**適用於**來標示。

- **問題和對客戶的影響**：可以依版本篩選 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文件。 使用每個文件頁面左上方控制項來篩選您的需求。

- **問題和對客戶的影響**︰SQL Server 2019 (15.x) 未提供任何離線內容。

## <a name="hardware-and-software-requirements"></a>硬體與軟體需求

- **問題和對客戶的影響**︰仍然會檢閱硬體和軟體需求，而且不是產品版本的最終需求。

  - **硬體**
    - [Windows - 處理器、記憶體和作業系統需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - 系統需求](../linux/sql-server-linux-setup.md#system)
  - **軟體**
    - Windows Server 2016 或更新版本。 如需其他需求，請參閱[安裝 SQL Server 的需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2。 可從[下載中心](https://www.microsoft.com/download/details.aspx?id=53344)取得。
    - 針對 Linux，請參閱 [Linux - 支援的平台](../linux/sql-server-linux-setup.md#supportedplatforms)

## <a name = "release-notes"></a>不支援的功能

- **問題和對客戶的影響**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]不支援下列元件、功能和案例：
  - SQL Sever Analysis Services
  - SQL Server Reporting Services
  - Kubernetes 上的 Always On 可用性群組
  - 加速資料庫復原
  - 經記憶體最佳化的 tempdb 中繼資料

- **因應措施**：無。 排除適用於所有客戶，包括 SQL 早期採用者方案的參與者。

- **適用於**：CTP 3.0

## <a name="updated-compiler"></a>更新的編譯器

- **問題和對客戶的影響**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 是以更新的編譯器所建置。 CTP 2.1 有個已知的問題，由於更新編譯器的緣故，浮點數和其他轉換案例可能傳回與舊版不同的值。 CTP 2.2 內含可確保受影響案例傳回與舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 相同結果的運作。 截至 CTP 3.0 版本，並沒有發現任何其他問題。 如果發現與 [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] 相較之下有任何結果異常，請立即回報 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 小組](http://aka.ms/sqlfeedback)。

- **因應措施**：不適用

- **適用於**：SQL Server 2019 CTP 3.0、CTP 2.5、CTP 2.4、CTP 2.3、CTP 2.2、CTP 2.1

## <a name="installation-wizard-may-wait-between-eula-pages"></a>安裝精靈可能會在使用者授權合約頁面之間等待

- **問題和對客戶的影響**︰在安裝精靈安裝期間，處理程序可能會在 R 服務的使用者授權合約 (EULA) 和 Python 的 EULA 之間等待很長時間。

- **因應措施**：等候安裝精靈繼續。 等待的時間可能會超過 30 分鐘。

- **適用於**：SQL Server 2019 CTP 3.0

## <a name="utf-8-collations"></a>UTF-8 定序

- **問題和對客戶的影響**︰啟用 UTF-8 的定序不能與某些其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能搭配使用。 使用下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能時不支援 UTF-8：

  - 記憶體內部 OLTP
  - PolyBase 的外部資料表
  - Always Encrypted

  > [!Note]
  > 在 Azure Data Studio 或 SQL Server Data Tools (SSDT) 中，目前沒有可選擇啟用 UTF-8 之定序的 UI 支援。 最新 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) 18 版支援在 UI 中選擇啟用 UTF-8 的定序。
 
- **因應措施**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 沒有任何因應措施。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0、CTP 2.5、CTP 2.4、CTP 2.3、CTP 2.2、CTP 2.1、CTP 2.0。

## <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted

- **問題和對客戶的影響**︰豐富計算會暫止數個效能最佳化，包含有限功能 (無索引等)，而且目前根據預設會停用。

- **因應措施**：若要啟用豐富計算，請執行 `DBCC traceon(127,-1)`。 如需詳細資料，請參閱[啟用豐富計算](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0、CTP 2.5、CTP 2.4、CTP 2.3、2.2、CTP 2.1、2.0。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
