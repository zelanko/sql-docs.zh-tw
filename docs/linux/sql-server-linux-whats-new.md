---
title: "新功能 SQL Server on Linux 2017 |Microsoft 文件"
description: "本主題中，反白顯示目前版本的 SQL Server 2017 Linux 上的新功能。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 381dcb3e22f123bfa07c2b387598d3429398e21f
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>在 Linux 上的 SQL Server 2017 的新功能

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本主題說明在 Linux 上執行的 SQL Server 2017 的新功能。

## <a name="ga"></a>GA

一般 Availaiblity (GA) 版本包含下列增強功能和修正程式：

- 現在可以在 NFS 上裝載資料庫檔案。 這會修正問題的 NFS 共用磁碟案例中，掛接遠端儲存體容器的平台，及掛接 Docker Windows 的資料夾。
- 其他的其他錯誤修正和增強功能。

## <a name="rc2"></a>RC2

RC2 版本包含其他錯誤修正和增強功能。

## <a name="rc1"></a>RC1

RC1 版本包含下列增強功能和修正程式：

- 啟用透明層安全性 (TLS) 加密連接。 如需詳細資訊，請參閱[加密的 SQL Server on Linux 連接](sql-server-linux-encrypted-connections.md)。
- 啟用[Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。
- 啟用[DB 郵件](../relational-databases/database-mail/database-mail.md)。
- 新增的 IPV6 的支援。
- 初始的 SQL Server 安裝程式的新增的環境變數。 如需詳細資訊，請參閱[Linux 上的環境變數與設定 SQL Server 設定](sql-server-linux-configure-environment-variables.md)。
- 移除**sqlpackage**安裝二進位檔。 SqlPackage 還是可以執行對 Linux 遠端從 Windows。
- 共用磁碟叢集資源代理程式設定 Windows SQL Server 容錯移轉叢集執行個體沒有與它類似的資源名稱。 `@@ServerName`傳回 SQL Server 共用的磁碟叢集資源名稱。在 RC1 之前，它會傳回叢集節點所擁有之資源的名稱。

## <a name="ctp-21"></a>CTP 2.1

CTP 2.1 版本包含下列增強功能和修正程式：

- 加入[環境變數，以設定 SQL Server 服務](sql-server-linux-configure-environment-variables.md)。
- [mssql conf](sql-server-linux-configure-mssql-conf.md)設定現在需要兩個部分的命名慣例。
- [Mssql scripter](https://github.com/Microsoft/sql-xplat-cli)工具。 此公用程式可讓開發人員、 Dba 和產生的 non-sysadmins`CREATE`和`INSERT`從 SQL Server、 Azure SQL DB、 和 Azure SQL DW 資料庫，從命令列中的資料庫物件的 TRANSACT-SQL 指令碼。
- [DBFS 工具](https://github.com/Microsoft/dbfs)。 這是可公開 SQL Server 動態管理檢視 (Dmv) 的即時資料，更輕鬆地監視 SQL Server 的 Dba 和 non-sysadmins 讓 Linux 作業系統上的虛擬目錄中的虛擬檔案為開放原始碼工具。
- SQL Server Integration Services (SSIS) 現在會在 Linux 上執行。 此外，還有可讓您在 Linux 上執行 SSIS 封裝，從命令列的新封裝。 如需詳細資訊，請參閱[部落格文章宣佈適用於 SSIS 支援適用於 Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。 與 Linux CTP 2.1 重新整理 SSIS，SSIS 封裝可以在 Linux 上使用 ODBC 連接。 如需詳細資訊，請參閱[部落格文章發表的 ODBC 支援在 Linux 上](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

## <a name="ctp-20"></a>CTP 2.0

CTP 2.0 版包含下列增強功能和修正程式：

- 加入**記錄傳送**SQL Server 代理程式的功能。
- Mssql configuration manager 的當地語系化的訊息
- Linux 路徑格式現在是整個 SQL Server 引擎相容。 但支援"c:\\"帶有前置詞的路徑將會繼續。
- 啟用 DMV **sys.dm_os_file_exists**。
- 啟用 DMV **sys.fn_trace_gettable**。
- 加入[CLR 嚴格的安全性模式](/sql/database-engine/configure-windows/clr-strict-security)。
- SQL 圖形。
- 擱置的線上索引重建。
- 彈性查詢處理。
- 已加入 utf-8 編碼系統檔案，包括記錄檔。
- 修正記憶體中資料庫的位置限制。 
- 加入新的叢集類型`CLUSTER_TYPE = EXTERNAL`設定高可用性的可用性群組。
- 修正針對唯讀路由的可用性群組接聽程式。
- 早期採用程式 」 (EAP) 客戶的生產環境支援。 註冊[這裡](http://aka.ms/eapsignup)。

## <a name="ctp-14"></a>CTP 1.4

CTP 1.4 版本包含下列增強功能和修正程式：

- 啟用[SQL Server Agent](sql-server-linux-setup-sql-agent.md)。
  - 啟用 T-SQL 作業功能。
- 固定的時區 bug:
  - 亞洲/加爾各答時區支援。
  - 固定 getdate （） 函式。
- 網路非同步 I / 0 增強功能：
  - 記憶體內部 OLTP 工作負載效能明顯的改進。
- Docker 映像現在包含 SQL Server 命令列公用程式。 (sqlcmd/bcp)。
- 啟用虛擬裝置介面 (VDI) 之備份支援。
- TempDB 位置現在可以修改後使用安裝`ALTER DATABASE`。

## <a name="ctp-13"></a>CTP 1.3

CTP 1.3 版本包含下列增強功能和修正程式：

- 啟用[全文檢索搜尋](sql-server-linux-setup-full-text-search.md)功能。
- 啟用 Always On[可用性群組功能](sql-server-linux-availability-group-overview.md)高可用性。
- 中的其他功能**mssql conf**:
  - 第一次安裝使用**mssql conf**。 請參閱 mssql-conf 中使用[安裝指南](sql-server-linux-setup.md#platforms)。
  - 啟用可用性群組。 請參閱[可用性群組主題](sql-server-linux-availability-group-overview.md)。
- 固定的原生 Linux 路徑支援的記憶體內 OLTP 檔案群組。
- 啟用 dm_os_host_info DMV 功能。

## <a name="ctp-12"></a>CTP 1.2

CTP 1.2 版本包含下列增強功能和修正程式：

- 支援[SUSE Linux Enterprise Server v12 SP2](quickstart-install-connect-suse.md)。
- 核心引擎和穩定性改進功能的 bug 修正。
- Docker 映像： 
  - 固定[發出 #1](https://github.com/Microsoft/mssql-docker/issues/1) Python 新增至映像。
  - 移除`/opt/mssql/data`做為預設的磁碟區。
- .Net 4.6.2 更新。

## <a name="ctp-11"></a>CTP 1.1

CTP 1.1 版本包含下列增強功能和修正程式：

- Red Hat Enterprise Linux 版本 7.3 支援。
- Ubuntu 16.10 的支援。
- Ubuntu 16.04 之 Docker 作業系統層級升級。
- 已修正遙測問題 Docker 映像中。
- 固定的 SQL Server 安裝程式指令碼相關的 bug。
- 原生編譯的 T-SQL 模組包括增強的效能：
  - **OPENJSON**， **FOR JSON**， **JSON**內建。
  - （唯一索引允許上保存的計算資料行，但不是能在非保存計算資料行對於記憶體中資料表） 的計算資料行。
  - **CROSS APPLY**作業。
- 新語言功能：
  - 字串函數：**修剪**， **CONCAT_WS**，**翻譯**和**STRING_AGG**支援**WITHIN GROUP (ORDER BY)**。
  - **大量匯入**現在支援 CSV 格式和 Azure Blob 儲存體做為檔案的來源。

在相容性模式下 140:

- 改善效能的更新案例中的非叢集資料行存放區索引資料列位於差異存放區。 變更從刪除和插入作業來更新。 也會變更整個從用來縮小計劃圖形。
- 批次模式查詢現在支援"memory grant 意見反應迴圈 」。 這可以改善並行存取，以及執行重複使用之查詢的批次模式的系統上的輸送量。 這會讓更多的查詢，否則封鎖之前啟動的查詢記憶體的系統上執行。
- 忽略批次模式計劃，以允許平行計劃，以針對 columnstores 改為選取的一般計畫的批次模式平行處理原則中已改良的效能。 

[Service Pack 1 的改良功能](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)CTP1.1 本版：
- CLR、 Filestream/Filetable、 記憶體和查詢存放區物件複製的資料庫。
- **建立**或**ALTER**運算子可程式性物件。
- 新**USE 提示**查詢選項，以提供查詢處理器的提示。 深入了解：[查詢提示](../t-sql/queries/hints-transact-sql-query.md)。
- SQL 服務帳戶現在可以透過程式設計方式識別啟用鎖定的分頁記憶體和立即檔案初始化的權限。
- TempDB 檔案計數、 檔案大小和檔案成長設定支援。
- Showplan XML 中的診斷延伸。
- 輕量級的每個運算子查詢執行分析。
- 新的動態管理函數**sys.dm_exec_query_statistics_xml**。
- 新動態管理函數的累加統計資料。
- 移除雜訊記憶體從錯誤記錄檔相關記錄訊息。
- 改善 AlwaysOn 延遲診斷。
- 清除手動變更追蹤。
- **DROP TABLE**支援進行複寫。
- **BULK INSERT**到與堆積**自動 TABLOCK**下 TF 715。
- 平行**INSERT...選取**本機暫存資料表的變更。

深入了解在這些修正程式[Service Pack 1 發行版本描述](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)。

許多資料庫引擎增強功能適用於 Windows 和 Linux。 目前不支援在 Linux 的 database engine 功能的是唯一的例外。 如需詳細資訊，請參閱[What's New in SQL Server 2017 (Database Engine)](https://msdn.microsoft.com/library/mt775028)。

## <a name="see-also"></a>另請參閱

安裝需求、 不支援的功能區域和已知的問題，請參閱[Linux 上的 SQL Server 2017 的版本資訊](sql-server-linux-release-notes.md)。

