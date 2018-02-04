---
title: "SQL Server on Linux 常見問題集 |Microsoft 文件"
description: "本文章會提供在 Linux 上執行 SQL Server 相關常見問題的解答。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/21/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Active
ms.openlocfilehash: 2da90e6cdf49531980e9014075d7b094b61271fd
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>SQL Server on Linux 常見問題集 (FAQ)

下列章節將提供常見的問題和解答的 SQL Server 在 Linux 上執行。

## <a name="general-questions"></a>一般問題

1. **支援哪些 Linux 平台？**

   Red Hat Enterprise Server、 SUSE Linux Enterprise Server 和 Ubuntu 上目前支援 SQL Server。 如需有關支援版本的最新資訊，請參閱[支援的平台](sql-server-linux-setup.md#supportedplatforms)。

1. **在 Linux 上支援的 SQL Server 功能？**

   如需支援的功能和已知的問題的完整清單，請參閱[版本資訊](sql-server-linux-release-notes.md)。

1. **什麼是 SQL Server 的支援原則？**

   若要了解的支援原則，檢閱[for SQL Server 的技術支援原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

1. **我來自 Windows SQL Server 背景。是否有資源可以幫助您了解如何使用 SQL Server on Linux？**

   [快速入門](sql-server-linux-setup.md#platforms)提供有關如何在 Linux 上安裝 SQL Server 和執行 TRANSACT-SQL 查詢的逐步指示。 其他教學課程提供使用 SQL Server on Linux 上的其他指示。 如需第三方的提示，請參閱[MSSQLTIPS 清單的 SQL Server on Linux 秘訣](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/)。

## <a name="installation"></a>安裝

1. **如何取得我的 Linux 伺服器上安裝 SQL Server？**

   Microsoft 維護安裝 SQL Server 的封裝儲存機制，支援透過原生封裝管理員 yum，zypper，例如的安裝和 apt。 若要快速安裝，請參閱其中[快速入門](sql-server-linux-setup.md#platforms)。

1. **可以在 Linux 子系統的 Windows 10 上安裝 SQL Server 嗎？**

   資料分割 在 Windows 10 上執行的 Linux 不目前支援的平台的 SQL Server 和相關的工具。

1. **SQL Server 2017 可以使用哪些 Linux 檔案系統的資料檔案？**

   目前 SQL Server on Linux 支援 ext4 和 XFS。 視需要在將來，將會加入其他檔案系統的支援。

1. **可以下載離線安裝 SQL Server 的安裝封裝嗎？**

   是的。 如需詳細資訊，請參閱封裝下載中的連結[版本資訊](sql-server-linux-release-notes.md)。 此外，請檢閱[離線安裝指示](sql-server-linux-setup.md#offline)。

1. **可以執行自動的安裝的 SQL Server on Linux 嗎？**

   是的。 如需自動安裝的討論，請參閱[SQL Server on Linux 的安裝指南](sql-server-linux-setup.md#unattended)。 請參閱範例指令檔[Red Hat](sample-unattended-install-redhat.md)， [SUSE Linux Enterprise Server](sample-unattended-install-suse.md)，和[Ubuntu](sample-unattended-install-ubuntu.md)。 您也可以檢閱[這個範例指令碼](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/)SQL Server 客戶諮詢團隊所建立。

## <a name="tools"></a>工具

1. **我可以存取 SQL Server on Linux Windows 中使用 SQL Server Management Studio 用戶端嗎？**

   是，您可以使用所有您現有的工具來存取 SQL Server on Linux 的 Windows 上執行。 其中包括工具，例如 SQL Server Management Studio (SSMS)、 SQL Server Data Tools (SSDT)，以及 OS 的 microsoft 和協力廠商工具。

1. **是否有這類工具會在 Linux 執行的 SSMS？**

   新的 Microsoft SQL 作業 Studio （預覽） 是用來管理 SQL Server 的跨平台工具。 如需詳細資訊，請參閱[什麼是 Microsoft SQL 作業 Studio （預覽）](../sql-operations-studio/what-is.md)。

1. **可用等 sqlcmd 和 bcp 命令在 Linux 上？**

   是， [sqlcmd 和 bcp](sql-server-linux-setup-tools.md)原生適用於 Linux、 macOS 和 Windows。 此外，使用 新[mssql scripter](https://github.com/Microsoft/mssql-scripter) Linux、 macOS 或產生 SQL 資料庫執行任何 T-SQL 指令碼的 Windows 上的命令列工具。 此外，請參閱 release preview [mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)。

1. **若要檢視活動監視器，透過在 Windows 上的 SSMS 連接之執行個體時可能在 Linux 上執行？**

   是，您可以在 Windows 上使用 SSMS 來連接遠端電腦上，並使用工具] / [功能如活動監視器 Linux 執行個體上的命令。

1. **哪些工具可用來監視 SQL Server on Linux 的效能？**

   您可以使用[系統動態管理檢視 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)收集各種類型的 SQL Server，包括 Linux 處理序資訊的相關資訊。 您可以使用[查詢存放區](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)來改善查詢效能。 其他工具，例如內建[績效儀表板](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)、 從遠端在 SQL Server Management Studio (SSMS) 從 Windows 工作。

## <a name="administration"></a>系統管理

1. **Microsoft 已在 Linux 上建立應用程式像是 SQL Server 組態管理員嗎？**

   是，有 SQL Server on Linux 的組態工具： [mssql conf](sql-server-linux-configure-mssql-conf.md)。

1. **SQL Server on Linux 支援多個執行個體上相同的主機嗎？**

   我們建議您將多個不同的執行個體的主機上執行多個容器。 每個容器將會需要不同的通訊埠上接聽。 如需詳細資訊，請參閱[執行 SQL Server 的多個容器](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers)。

1. **在 Linux 上支援的 Active Directory 驗證？**

   是的。 如需詳細資訊，請參閱[Active Directory 驗證與 SQL Server on Linux](sql-server-linux-active-directory-authentication.md)。

1. **Always On，而且在 Linux 中支援的叢集嗎？**

   容錯移轉叢集和在 Linux 上的高可用性，可達到 Pacemaker Linux 上使用。 如需詳細資訊，請參閱[商務持續性和資料庫復原-您的 SQL Server on Linux](sql-server-linux-business-continuity-dr.md)。

1. **它可能會設定從 Linux 及 Windows 的複寫？**

   向外延展讀取複本可以用於 Windows 和 Linux 間單向資料複寫。

1. **它可能會從 Windows 將在舊版的 SQL Server 中現有的資料庫移轉到 Linux？**

   是，有[數種方法](sql-server-linux-migrate-overview.md)達到這個目的。

1. **我可以移轉我的資料從 Oracle 和其他資料庫引擎在 Linux 上的 SQL server？**

   是的。 SSMA 支援從資料庫引擎的幾種類型： Microsoft Access、 DB2、 MySQL、 Oracle 和 SAP ASE (先前稱為 SAP Sybase ASE)。 如需如何使用 SSMA 的範例，請參閱[將 Oracle 結構描述移轉至 SQL Server 移轉小幫手與 Linux 上的 SQL Server 2017](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)。

1. **需要 SQL Server 檔案的權限？**

   中的所有檔案`/var/opt/mssql`檔案資料夾應該擁有的**mssql**使用者，而且屬於**mssql**群組。 這兩個**mssql**使用者和群組應該擁有的所有檔案和目錄的讀寫權限。 請注意下列特殊案例涉及檔案和目錄權限：

   * Mssql 擁有者和群組的權限所需的已掛接的網路共用，用來儲存 SQL Server 檔案。
   * 如果您在非預設目錄中找到資料庫檔案或備份，您也必須設定該目錄的權限。
   * 如果您將變更預設根 umask 0022，則會在安裝之後失敗的 SQL Server 組態。 您必須再手動套用必要的權限 SQL Server 啟動帳戶。

1. **可以從已安裝的 mssql 帳戶和群組變更 SQL Server 的檔案和目錄的擁有權嗎？**

   我們不支援變更從預設安裝的 SQL Server 目錄和檔案的擁有權。 Mssql 帳戶和群組特別適用於 SQL Server，沒有互動式登入的存取。

## <a name="next-steps"></a>後續的步驟

如需有關如何在 Linux 上執行 SQL Server 的詳細資訊，請參閱[概觀的 SQL Server on Linux](sql-server-linux-overview.md)。