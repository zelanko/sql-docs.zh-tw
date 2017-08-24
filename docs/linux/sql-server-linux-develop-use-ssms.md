---
title: "管理 SQL Server on Linux 使用 SSMS |Microsoft 文件"
description: "本教學課程會示範如何使用 Windows 上的 SQL Server Management Studio 來連接到 SQL Server 在 Linux 上執行。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 30cc4564-f389-4707-9b25-8ba782cc5150
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: a999ca0248e83d2d9ef59f7ec04ad2dd58378132
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="use-sql-server-management-studio-ssms-on-windows-to-manage-sql-server-on-linux"></a>使用 Windows 上的 SQL Server Management Studio (SSMS) 來管理 SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

本主題示範如何使用[SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)連接到在 Linux 上的 SQL Server 2017 RC2。 SSMS 是 Windows 應用程式，因此使用 SSMS 時可以連線到遠端的 SQL Server 執行個體，在 Linux 上的 Windows 電腦。 

已成功連接之後，您可以執行簡單的 TRANSACT-SQL (T-SQL) 查詢，以便驗證與資料庫通訊。

## <a name="install-the-newest-version-of-sql-server-management-studio"></a>安裝最新版本的 SQL Server Management Studio

當使用 SQL Server，您應該一律使用最新版本的 SQL Server Management Studio (SSMS)。 SSMS 的最新版本而不斷更新並最佳化，目前適用於 SQL Server 2017 on Linux。 若要下載並安裝最新版本，請參閱[下載 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。 若要保持最新狀態，最新版本的 SSMS 會提示您有新的版本可供下載時。 

## <a name="connect-to-sql-server-on-linux"></a>連接到 SQL Server on Linux

下列步驟顯示如何連接到 SQL Server 2017 on Linux 使用 SSMS。

1. 啟動 SSMS 輸入**Microsoft SQL Server Management Studio** windows 搜尋] 方塊中，然後按一下 [桌面應用程式。

    ![Transact-SQL](./media/sql-server-linux-develop-use-ssms/ssms.png)

2. 在**連接到伺服器**視窗中，輸入下列資訊 (如果 SSMS 已在執行中，按一下**連接 > Database Engine**開啟**連接到伺服器**視窗):

   | 設定 | Description |
   |-----|-----|
   | **伺服器類型** | 預設值是資料庫引擎。請勿變更此值。 |
   | **伺服器名稱** | 輸入目標 Linux SQL Server 電腦或 IP 位址的名稱。 |
   | **驗證** | 在 Linux 上的 SQL Server 2017，對於使用**SQL Server 驗證**。 |
   | **登入** | 輸入資料庫伺服器上具有存取權的使用者名稱 (例如，預設值**SA**在安裝期間建立的帳戶)。 |
   | **密碼** | 指定的使用者輸入的密碼 (如**SA**帳戶，您這在安裝期間建立)。 |

    ![SQL Server Management Studio： 連接到 SQL Database 伺服器](./media/sql-server-linux-develop-use-ssms/connect.png)

3. 按一下 **[連接]**。

    > [!TIP]
    > 如果您收到連線失敗，請先嘗試從錯誤訊息診斷問題。 然後檢閱[連線疑難排解建議](sql-server-linux-troubleshooting-guide.md#connection)。
 
5. 順利連接到您 SQL Sever 之後,**物件總管 中**隨即開啟，您現在可以存取您的資料庫來執行管理工作，或查詢資料。
 
     ![物件總管](./media/sql-server-linux-develop-use-ssms/object-explorer.png)
     
## <a name="run-sample-queries"></a>執行範例查詢

您連接到您的伺服器之後，您可以連接到資料庫並執行範例查詢。 如果您不熟悉撰寫查詢，請參閱[撰寫 TRANSACT-SQL 陳述式](https://msdn.microsoft.com/library/ms365303.aspx)。

1. 識別要用來執行針對查詢資料庫。 這可能是您在建立新資料庫[TRANSACT-SQL 教學課程](https://msdn.microsoft.com/library/ms365303.aspx)。 或者，它可以是**AdventureWorks**範例資料庫，您[下載及還原](sql-server-linux-migrate-restore-database.md)。
2. 在**物件總管 中**，瀏覽至目標資料庫伺服器上。
2. 以滑鼠右鍵按一下資料庫，然後選取**新查詢**:

    ![新的查詢。 連接到 SQL 資料庫伺服器： SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/new-query.png)

3. 在查詢視窗中，撰寫 TRANSACT-SQL 查詢，以選取資料從一個資料表。 下列範例會選取從資料**Production.Product**資料表**AdventureWorks**資料庫。

        SELECT TOP 10 Name, ProductNumber
        FROM Production.Product
        ORDER BY Name ASC

4. 按一下**Execute**按鈕：

    ![成功。 連接到 SQL 資料庫伺服器： SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/execute-query.png)

## <a name="next-steps"></a>後續的步驟

除了查詢之外，您可以使用 T-SQL 陳述式來建立和管理資料庫。

如果您還不熟悉 T-SQL，請參閱[教學課程： 撰寫 TRANSACT-SQL 陳述式](https://msdn.microsoft.com/library/ms365303.aspx)和[TRANSACT-SQL 參考 (Database Engine)](https://msdn.microsoft.com/library/bb510741.aspx)。

如需有關如何使用 SSMS 的詳細資訊，請參閱[使用 SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)。

