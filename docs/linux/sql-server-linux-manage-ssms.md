---
title: "使用 SSMS 管理 SQL Server on Linux |Microsoft 文件"
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 07/19/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 1b16a5e8168f18a3e687fdf0249f93cd3549f27d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>在 Windows 上使用 SQL Server Management Studio，來管理 SQL Server on Linux

本主題將介紹[SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/en-us/library/hh213248.aspx)和會逐步引導您透過幾個常見工作。 SSMS 是 Windows 應用程式，因此使用 SSMS 時可以連線到遠端的 SQL Server 執行個體，在 Linux 上的 Windows 電腦。

[SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/en-us/library/hh213248.aspx)是一套的 Microsoft 提供免費的開發和管理的需求不需要支付費用的 SQL 工具的一部分。 SSMS 是一個整合式的環境，可存取、 設定、 管理、 管理和開發 SQL Server 的執行在內部部署或雲端，在 Linux、 Windows 或 macOS 和 Azure SQL Database 上的 Docker 和 Azure SQL 資料倉儲中的所有元件。 SSMS 利用許多豐富的指令碼編輯器，以提供開發人員和所有技能等級的系統管理員存取 SQL Server 合併了非常廣泛的圖形工具。

SSMS for SQL Server，包括工具，可提供一組廣泛的開發和管理功能：
- 設定、 監視及管理單一或多個 SQL Server 執行個體
- 部署、 監視以及升級資料層元件，例如資料庫和資料倉儲
- 備份和還原資料庫
- 建置並執行 T-SQL 查詢和指令碼，以及查看結果
- 產生資料庫物件的 T-SQL 指令碼
- 檢視和編輯資料庫中的資料
- 以視覺化方式設計 T-SQL 查詢和檢視表、 資料表和預存程序等資料庫物件

請參閱[使用 SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx)如需詳細資訊。

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>安裝最新版本的 SQL Server Management Studio (SSMS)

當使用 SQL Server，您應該一律使用最新版本的 SQL Server Management Studio (SSMS)。 SSMS 的最新版本而不斷更新並最佳化，目前適用於 SQL Server 2017 on Linux。 若要下載並安裝最新版本，請參閱[下載 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。 若要保持最新狀態，最新版本的 SSMS 會提示您有新的版本可供下載時。 

## <a name="before-you-begin"></a>開始之前
- 請參閱[使用 SSMS 連接到 SQL Server on Linux 的 Windows 上](sql-server-linux-develop-use-ssms.md)如何連接及查詢使用 SSMS
- 讀取[已知問題](sql-server-linux-release-notes.md)Linux 上的 SQL Server 2017 rc2

## <a name="create-and-manage-databases"></a>建立和管理資料庫
連線到時*主要*資料庫，您可以在伺服器上建立資料庫並修改或卸除現有資料庫。 下列步驟說明如何完成幾個一般資料庫管理工作，透過 Management Studio。 若要執行這些工作，確定您已連線至*主要*與伺服器層級主體登入您設定在 Linux 上的 SQL Server 2017 RC2 時所建立的資料庫。

### <a name="create-a-new-database"></a>建立新的資料庫

1. 啟動 SSMS 並連接到您的伺服器，在 Linux 上的 SQL Server 2017 RC2

2. 在 [物件總管] 中，以滑鼠右鍵按一下*資料庫*資料夾，然後再按一下 * 新的資料庫...」

3. 在*新資料庫* 對話方塊中，輸入您的新資料庫的名稱，然後按一下*確定*

在您的伺服器已成功建立新的資料庫。 如果您想要建立新的資料庫使用 T-SQL，則請參閱[CREATE DATABASE (SQL Server TRANSACT-SQL&AMP;)](https://msdn.microsoft.com/en-us/library/ms176061.aspx)。

### <a name="drop-a-database"></a>卸除資料庫

1. 啟動 SSMS 並連接到您的伺服器，在 Linux 上的 SQL Server 2017 RC2

2. 在 [物件總管] 中，展開*資料庫*資料夾，以查看在伺服器上的所有資料庫的清單。

3. 在 物件總管 中，以滑鼠右鍵按一下您想要卸除的資料庫，然後按一下 *刪除*

4. 在*刪除物件*] 對話方塊中，核取*關閉現有連接*，然後按一下 [ *[確定]*

從您的伺服器，順利卸除資料庫。 如果您想要卸除資料庫，使用 T-SQL，則請參閱[DROP DATABASE (SQL Server TRANSACT-SQL&AMP;)](https://msdn.microsoft.com/en-us/library/ms178613.aspx)。

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>使用 活動監視器來查看 SQL Server 活動相關資訊

[活動監視器](https://msdn.microsoft.com/en-us/library/hh212951.aspx)工具是內建到 SQL Server Management Studio (SSMS)，並顯示 SQL Server 處理序以及這些處理序如何影響目前的 SQL Server 執行個體的相關資訊。

1. 啟動 SSMS 並連接到您的伺服器，在 Linux 上的 SQL Server 2017 RC2

2. 在 [物件總管] 中，以滑鼠右鍵按一下*伺服器*節點，然後再按一下*活動監視器*

活動監視器顯示可展開及摺疊的窗格具有下列相關資訊：
- 概觀
- 處理序
- 資源等候
- 資料檔案 I/O
- 最近且費時的查詢
- 使用中且費時的查詢

展開窗格時，活動監視器會查詢資訊的執行個體。 摺疊某個窗格時，該窗格的所有查詢活動就會停止。 您可以檢視不同種類的活動執行個體上同時展開一或多個窗格。

## <a name="see-also"></a>另請參閱
- [使用 SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx)
- [匯出和匯入資料庫，以使用 SSMS](sql-server-linux-migrate-ssms.md)
- [教學課程：SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/bb934498.aspx)
- [教學課程：撰寫國際性通用的 Transact-SQL 陳述式](https://msdn.microsoft.com/en-us/library/ms365303.aspx)
- [伺服器效能與活動監視](https://msdn.microsoft.com/en-us/library/ms191511.aspx)

