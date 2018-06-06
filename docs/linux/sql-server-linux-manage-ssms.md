---
title: 使用 SSMS 管理 SQL Server on Linux |Microsoft 文件
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/21/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.custom: sql-linux
ms.openlocfilehash: 2b6293e7c0d80eb1ebe02d6cd03f17626d793c05
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>在 Windows 上使用 SQL Server Management Studio，來管理 SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介紹[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)和會逐步引導您透過幾個常見工作。 SSMS 是 Windows 應用程式，因此使用 SSMS 時可以連線到遠端的 SQL Server 執行個體，在 Linux 上的 Windows 電腦。

> [!TIP]
> 如果您沒有一部 Windows 電腦上執行 SSMS，請考慮新[SQL Server 作業 Studio](../sql-operations-studio/index.md)。 它提供圖形化工具來管理 SQL Server 和 Linux 及 Windows 上執行。

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)是一套的 Microsoft 提供免費的開發和管理的需求不需要支付費用的 SQL 工具的一部分。 SSMS 是一個整合式的環境，可存取、 設定、 管理、 管理和開發 SQL Server 的所有元件。 它可以連接到任何平台上執行這兩個內部部署，在 Docker 容器中部署和雲端中的 SQL Server。 它也會連接到 Azure SQL Database 和 Azure SQL 資料倉儲。 SSMS 利用許多豐富的指令碼編輯器，以提供開發人員和所有技能等級的系統管理員存取 SQL Server 合併了非常廣泛的圖形工具。

SSMS for SQL Server，包括工具，可提供一組廣泛的開發和管理功能：

- 設定、 監視和管理單一或多個 SQL Server 執行個體
- 部署、 監視以及升級資料層元件，例如資料庫和資料倉儲
- 備份和還原資料庫
- 建置並執行 T-SQL 查詢和指令碼，以及查看結果
- 產生資料庫物件的 T-SQL 指令碼
- 檢視和編輯資料庫中的資料
- 以視覺化方式設計 T-SQL 查詢和檢視表、 資料表和預存程序等資料庫物件

請參閱[SSMS 是什麼？](../ssms/sql-server-management-studio-ssms.md)如需有關 SSMS。

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>安裝最新版本的 SQL Server Management Studio (SSMS)

當使用 SQL Server，您應該一律使用最新版本的 SQL Server Management Studio (SSMS)。 SSMS 的最新版本而不斷更新並最佳化，目前適用於 SQL Server 2017 on Linux。 若要下載並安裝最新版本，請參閱[下載 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 若要保持最新狀態，最新版本的 SSMS 會提示您有新的版本可供下載時。

> [!NOTE]
> 使用 SSMS 來管理 Linux 之前, 檢閱[已知問題](sql-server-linux-release-notes.md)Linux 上的 ssms。

## <a name="connect-to-sql-server-on-linux"></a>連接到 SQL Server on Linux

若要取得連線使用下列基本步驟：

1. 啟動 SSMS 輸入**Microsoft SQL Server Management Studio** windows 搜尋] 方塊中，然後按一下 [桌面應用程式。

    ![Transact-SQL](./media/sql-server-linux-manage-ssms/ssms.png)

1. 在**連接到伺服器**視窗中，輸入下列資訊 (如果 SSMS 已在執行中，按一下**連接 > Database Engine**開啟**連接到伺服器**視窗):

   | 設定 | Description |
   |-----|-----|
   | **伺服器類型** | 預設值是資料庫引擎。請勿變更此值。 |
   | **伺服器名稱** | 輸入目標 Linux SQL Server 電腦或 IP 位址的名稱。 |
   | **驗證** | 在 Linux 上的 SQL Server 2017，對於使用**SQL Server 驗證**。 |
   | **登入** | 輸入資料庫伺服器上具有存取權的使用者名稱 (例如，預設值**SA**在安裝期間建立的帳戶)。 |
   | **密碼** | 指定的使用者輸入的密碼 (如**SA**帳戶，您這在安裝期間建立)。 |

    ![SQL Server Management Studio： 連接到 SQL Database 伺服器](./media/sql-server-linux-manage-ssms/connect.png)

1. 按一下 **[連接]**。

    > [!TIP]
    > 如果您收到連線失敗，請先嘗試從錯誤訊息診斷問題。 然後檢閱[連線疑難排解建議](sql-server-linux-troubleshooting-guide.md#connection)。
 
1. 已成功連接到您的 SQL Server 後**物件總管 中**隨即開啟，您現在可以存取您的資料庫來執行管理工作，或查詢資料。

## <a name="run-transact-sql-queries"></a>執行 TRANSACT-SQL 查詢

您連接到您的伺服器之後，您可以連接到資料庫並執行 TRANSACT-SQL 查詢。 Transact SQL 查詢可用於幾乎任何資料庫 」 工作。

1. 在**物件總管 中**，瀏覽至目標資料庫伺服器上。 例如，展開 **系統資料庫**使用**主要**資料庫。

1. 以滑鼠右鍵按一下資料庫，然後選取**新查詢**。

1. 在查詢視窗中，您的伺服器上的所有資料庫名稱撰寫 TRANSACT-SQL 查詢，以選取傳回。

   ```sql
   SELECT [Name]
   FROM sys.Databases
   ```

   如果您不熟悉撰寫查詢，請參閱[撰寫 TRANSACT-SQL 陳述式](../t-sql/tutorial-writing-transact-sql-statements.md)。

1. 按一下**Execute**按鈕來執行查詢並查看結果。

   ![成功。 連接到 SQL 資料庫伺服器： SQL Server Management Studio](./media/sql-server-linux-manage-ssms/execute-query.png)

雖然可以執行幾乎任何 TRANSACT-SQL 查詢與管理工作，SSMS 是圖形工具，可讓您輕鬆地管理 SQL Server。 下列章節提供使用圖形化使用者介面的一些範例。

## <a name="create-and-manage-databases"></a>建立和管理資料庫

連線到時*主要*資料庫，您可以在伺服器上建立資料庫並修改或卸除現有資料庫。 下列步驟說明如何完成幾個一般資料庫管理工作，透過 Management Studio。 若要執行這些工作，確定您已連線至*主要*與伺服器層級主體登入您設定在 Linux 上的 SQL Server 2017 時所建立的資料庫。

### <a name="create-a-new-database"></a>建立新的資料庫

1. 啟動 SSMS 並連接到您的伺服器，在 Linux 上的 SQL Server 2017

2. 在 [物件總管] 中，以滑鼠右鍵按一下*資料庫*資料夾，然後再按一下 * 新的資料庫...」

3. 在*新資料庫* 對話方塊中，輸入您的新資料庫的名稱，然後按一下*確定*

在您的伺服器已成功建立新的資料庫。 如果您想要建立新的資料庫使用 T-SQL，則請參閱[CREATE DATABASE (SQL Server TRANSACT-SQL&AMP;)](../t-sql/statements/create-database-sql-server-transact-sql.md)。

### <a name="drop-a-database"></a>卸除資料庫

1. 啟動 SSMS 並連接到您的伺服器，在 Linux 上的 SQL Server 2017

2. 在 [物件總管] 中，展開*資料庫*資料夾，以查看在伺服器上的所有資料庫的清單。

3. 在 物件總管 中，以滑鼠右鍵按一下您想要卸除的資料庫，然後按一下 *刪除*

4. 在*刪除物件*] 對話方塊中，核取*關閉現有連接*，然後按一下 [ *[確定]*

從您的伺服器，順利卸除資料庫。 如果您想要卸除資料庫，使用 T-SQL，則請參閱[DROP DATABASE (SQL Server TRANSACT-SQL&AMP;)](../t-sql/statements/drop-database-transact-sql.md)。

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>使用 活動監視器來查看 SQL Server 活動相關資訊

[活動監視器](../relational-databases/performance-monitor/activity-monitor.md)工具內建到 SQL Server Management Studio (SSMS)，並顯示 SQL Server 處理序以及這些處理序如何影響目前的 SQL Server 執行個體的相關資訊。

1. 啟動 SSMS 並連接到您的伺服器，在 Linux 上的 SQL Server 2017

1. 在 [物件總管] 中，以滑鼠右鍵按一下*伺服器*節點，然後再按一下*活動監視器*

活動監視器顯示可展開及摺疊的窗格包含下列資訊：

- 概觀
- 處理序
- 資源等候
- 資料檔案 I/O
- 最近且費時的查詢
- 使用中且費時的查詢

展開窗格時，活動監視器會查詢資訊的執行個體。 摺疊某個窗格時，該窗格的所有查詢活動就會停止。 您可以檢視不同種類的活動執行個體上同時展開一或多個窗格。

## <a name="see-also"></a>另請參閱
- [什麼是 SSMS？](../ssms/sql-server-management-studio-ssms.md)
- [匯出和匯入資料庫，以使用 SSMS](sql-server-linux-migrate-ssms.md)
- [教學課程：SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
- [教學課程：撰寫國際性通用的 Transact-SQL 陳述式](../t-sql/tutorial-writing-transact-sql-statements.md)
- [伺服器效能與活動監視](../relational-databases/performance/server-performance-and-activity-monitoring.md)
