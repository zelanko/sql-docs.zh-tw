---
title: SQL Server on Linux 常見問題集 |Microsoft Docs
description: 本文章提供有關 SQL Server 常見問題的解答，在 Linux 上執行。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/10/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 50397d605b8cb34d1093aec573b973cdbc301da5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719407"
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>Linux 上的 SQL Server 常見問題集 (Faq)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列各節提供常見問答集適用於 SQL Server 在 Linux 上執行。

## <a name="general-questions"></a>一般問題

1. **支援哪些 Linux 平台？**

   SQL Server 目前支援在 Red Hat Enterprise Server、 SUSE Linux Enterprise Server 和 Ubuntu 上。 它也支援使用 Docker 容器中執行。 如需有關支援版本的最新資訊，請參閱[支援的平台](sql-server-linux-setup.md#supportedplatforms)。

1. **將在其他平台上運作在 Linux 上的 SQL Server**嗎？

   測試並如先前所列的散發套件支援在 Linux 上 SQL Server。 其他 Linux 散發套件密切相關，而且可能無法執行 SQL Server （例如，CentOS 密切相關 Red Hat Enterprise Server）。 但如果您選擇不支援的作業系統上安裝 SQL Server，請檢閱**的支援原則**一節[Microsoft SQL Server 的技術支援原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)若要了解支援影響。 也請注意，某些社群維護的 Linux 散發套件沒有正式的方法，才能獲得支援，如果基礎作業系統是問題所在。

1. **是在 Linux 上的 SQL Server 和 Windows 上的相同嗎？**

   因為它是在 Windows 上的 SQL Server Database Engine 的核心都是在 Linux 上相同的。 不過，某些功能目前不支援在 Linux 上。 如需不支援在 Linux 的功能，請參閱[不支援的功能與服務](sql-server-linux-release-notes.md#Unsupported)。 也檢閱[已知問題](sql-server-linux-release-notes.md#known-issues)。 除非在這些清單中指定，其他 SQL Server 功能和服務支援在 Linux 上。

1. **適用於 SQL Server 的支援原則為何？**

   若要了解的支援原則，請檢閱[技術支援的原則，適用於 SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

1. **我來自 Windows SQL Server 的背景。有資源可以幫助您了解如何在 Linux 上使用 SQL Server 嗎？**

   [快速入門](sql-server-linux-setup.md#platforms)提供有關如何在 Linux 上安裝 SQL Server 和執行 TRANSACT-SQL 查詢的逐步指示。 其他教學課程會提供有關在 Linux 上使用 SQL Server 的其他指示。 如需第三方的秘訣，請參閱[MSSQLTIPS 清單中的 SQL Server on Linux 的秘訣](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/)。

## <a name="licensing"></a>授權

1. **在 Linux 上的授權方式為何？**

   SQL Server 會將相同的方式授權適用於 Windows 和 Linux。 事實上，SQL Server 授權，然後您可以選擇使用您選擇的平台上的該授權。 如需詳細資訊，請參閱 < [SQL Server 授權如何](https://www.microsoft.com/sql-server/sql-server-2017-pricing)。

1. **我已購買時，我有選擇哪些版本的 SQL Server 應該？**

   當您執行 mssql conf 安裝程式會有下列選項：
   
   ```
   Choose an edition of SQL Server:
      1. Evaluation (free, no production use rights, 180-day limit)
      2. Developer (free, no production use rights)
      3. Express (free)
      4. Web (PAID)
      5. Standard (PAID)
      6. Enterprise (PAID)
      7. Enterprise Core (PAID)
      8. I bought a license through a retail sales channel and have a product key to enter.
   ```
     
   如果您已取得您透過大量授權 Enterprise 合約的一部分，或透過您的 MSDN 訂閱的授權，您需要選取選項 4 到 7。 此步驟不會要求您輸入授權，但您必須先前已購買的適當授權您的組態。 如果您已購買透過零售通路的 Standard edition，請選取 [8] 選項。 這個選項的提示您輸入金鑰。 

1. **如何驗證版本的 Linux 上的 SQL Server 的已安裝的版本？**

   例如連接到 SQL Server 執行個體，使用用戶端工具**sqlcmd**， **mssql cli**，或 Visual Studio Code。 然後執行下列 TRANSACT-SQL 查詢來確認您正在執行的 SQL server 的版本： 

   ```sql
   SELECT @@VERSION
   SELECT SERVERPROPERTY('Edition')
   ```

## <a name="installation"></a>安裝

1. **如何取得我的 Linux 伺服器上安裝 SQL Server？**

   Microsoft 會維護 SQL Server 安裝的套件存放庫，並支援透過 yum，zypper，例如原生的套件管理員安裝及 apt。 若要快速安裝，請參閱其中一個[快速入門](sql-server-linux-setup.md#platforms)。

1. **可以在 Linux 子系統的 Windows 10 上安裝 SQL Server 嗎？**

   資料分割 在 Windows 10 上執行的 Linux 目前不支援的平台，適用於 SQL Server 和相關的工具。

1. **SQL Server 可以使用的 Linux 檔案系統的資料檔案？**

   目前在 Linux 上的 SQL Server 支援 ext4 和 XFS。 視需要在未來，則會加入支援其他檔案系統。

1. **我可以下載離線安裝 SQL Server 應用程式套件嗎？**

   是的。 如需詳細資訊，請參閱套件下載中的連結[版本資訊](sql-server-linux-release-notes.md)。 此外，請檢閱[離線安裝指示](sql-server-linux-setup.md#offline)。

1. **我可以在 Linux 上執行自動的安裝的 SQL Server？**

   是的。 如需自動安裝的討論，請參閱 <<c0> [ 在 Linux 上的 SQL Server 的安裝指引](sql-server-linux-setup.md#unattended)。 請參閱範例指令碼，如[Red Hat](sample-unattended-install-redhat.md)， [SUSE Linux Enterprise Server](sample-unattended-install-suse.md)，並[Ubuntu](sample-unattended-install-ubuntu.md)。 您也可以檢閱[這個範例指令碼](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/)SQL Server 客戶諮詢小組所建立。

## <a name="tools"></a>工具

1. **我可以存取 Linux 上的 SQL Server Windows 中使用 SQL Server Management Studio 用戶端？**

   是，您可以使用所有現有的工具來存取 SQL Server on Linux 的 Windows 上執行。 其中包括 Microsoft SQL Server Management Studio (SSMS)、 SQL Server Data Tools (SSDT) 和 OSS 等的工具和協力廠商工具。

1. **有在 Linux 執行的 SSMS 之類的工具嗎？**

   新的 Azure Data Studio 是用於管理 SQL Server 的跨平台工具。 如需詳細資訊，請參閱 <<c0> [ 什麼是 Azure Data Studio](../azure-data-studio/what-is.md)。

1. **Sqlcmd 和 bcp 等的命令是在 Linux 上使用的？**

   是， [sqlcmd 和 bcp](sql-server-linux-setup-tools.md)是在 Linux、 macOS 和 Windows 上的原生功能。 此外，使用 新[mssql scripter](https://github.com/Microsoft/mssql-scripter)上 Linux、 macOS 或 Windows 產生的任何地方執行您的 SQL database 的 T-SQL 指令碼的命令列工具。 此外，請參閱預覽版本[mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)。

1. **若要檢視活動監視器，透過在 Windows 上的 SSMS 執行個體進行連接時可能在 Linux 上執行？**

   是，您可以在 Windows 上使用 SSMS 來連線遠端電腦上，並使用工具] / [等功能在 Linux 執行個體上的活動監視器命令。

1. **哪些工具可用來監視在 Linux 上的 SQL Server 效能？**

   您可以使用[系統動態管理檢視 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)收集各種類型的 SQL Server，包括 Linux 處理序資訊的相關資訊。 您可以使用[查詢存放區](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)來改善查詢效能。 其他工具，例如內建[績效儀表板](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)、 從遠端在 SQL Server Management Studio (SSMS) 從 Windows 工作。

   > [!TIP]
   > 正確設定您的 Linux 作業系統和 SQL Server insance 為一種方法改善效能。 如需詳細資訊，請參閱 <<c0> [ 效能最佳做法和 Linux 上的 SQL Server 組態指導方針](sql-server-linux-performance-best-practices.md)。

## <a name="administration"></a>系統管理

1. **Microsoft 已在 Linux 上建立應用程式 SQL Server 組態管理員 」 等？**

   沒錯，的確在 Linux 上的 SQL Server 組態工具： [mssql conf](sql-server-linux-configure-mssql-conf.md)。

1. **在 Linux 上的 SQL Server 支援多個執行個體上相同的主機嗎？**

   建議要有多個不同的執行個體的主機上執行多個容器。 這其實很容易使用 docker，但每個容器都必須在不同的連接埠上接聽。 如需詳細資訊，請參閱 <<c0> [ 執行 SQL Server 的多個容器](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers)。

1. **在 Linux 上支援的 Active Directory 驗證？**

   是的。 如需詳細資訊，請參閱 <<c0> [ 在 Linux 上的 SQL server 的 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。

1. **Always On，而且僅在 Linux 中支援叢集嗎？**

   容錯移轉叢集和 Linux 上的高可用性被透過 Linux 上的 Pacemaker。 如需詳細資訊，請參閱 <<c0> [ 商務持續性與資料庫復原-SQL Server on Linux](sql-server-linux-business-continuity-dr.md)。

1. **是否可以設定從 Linux 到 Windows，反之亦然的複寫？**

   讀取級別複本可以用於 Windows 與 Linux 之間單向資料複寫。

1. **是否可以從 Windows 的較舊版本的 SQL Server 中現有的資料庫移轉到 Linux？**

   當然還有[幾種方法](sql-server-linux-migrate-overview.md)達到這個目的。

1. **我可以移轉我的資料從 Oracle 和其他資料庫引擎到 Linux 上的 SQL Server 嗎？**

   是的。 SSMA 支援從數種類型的資料庫引擎移轉：Microsoft Access、 DB2、 MySQL、 Oracle 和 SAP ASE (前身為 SAP Sybase ASE)。 如需如何使用 SSMA 的範例，請參閱 < [Oracle 結構描述移轉至 SQL Server，在 Linux 上使用 SQL Server Migration Assistant](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=/sql/toc/toc.json)。

1. **SQL Server 檔案需要哪些權限？**

   中的所有檔案`/var/opt/mssql`檔案的資料夾必須由擁有**mssql**使用者，而且屬於**mssql**群組。 這兩個**mssql**使用者和群組應該擁有的所有檔案和目錄的讀寫權限。 請注意下列的特殊案例，涉及檔案和目錄的權限：

   * Mssql 擁有者和群組權限所需的已掛接的網路共用，用來儲存 SQL Server 檔案。
   * 如果您在非預設目錄中找到資料庫檔案或備份，您也必須設定該目錄的權限。
   * 如果您變更預設根 umask 0022，SQL Server 組態失敗之後安裝。 您必須接著手動套用必要的權限 SQL Server 啟動帳戶。

1. **可以變更 SQL Server 檔案和目錄的擁有權從已安裝的 mssql 帳戶及群組嗎？**

   我們不支援變更 SQL Server 目錄和檔案的擁有權從預設的安裝。 Mssql 帳戶和群組專門用於 SQL Server，並且沒有互動式登入存取權。

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
