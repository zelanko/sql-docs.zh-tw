---
title: "連接到 Azure 上的 SSISDB 目錄資料庫 |Microsoft 文件"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: dbe6f832d4af55ddd15e12fba17a4da490fe19ae
ms.openlocfilehash: 646999095957abb4e615b59b316b6ca59155dea3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/25/2017

---
# <a name="connect-to-the-ssisdb-catalog-database-on-azure"></a>連接到 Azure 上的 SSISDB 目錄資料庫

取得您需要連接到裝載於 Azure SQL Database 伺服器上的 SSISDB 目錄資料庫的連接資訊。 您需要下列項目，來連接：
- 完整的伺服器名稱
- 資料庫名稱
- 登入資訊 

## <a name="prerequisites"></a>必要條件
開始之前，請確定您有 17.2 或更新版本的 SQL Server Management Studio 的版本。 若要下載最新版本的 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="get-the-connection-info-from-the-azure-portal"></a>從 Azure 入口網站取得的連接資訊
1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 在 Azure 入口網站中，選取**SQL 資料庫**從左側功能表，然後選取`SSISDB`資料庫**SQL 資料庫**頁面。 
3. 在**概觀**頁面`SSISDB`資料庫，請檢閱完整的伺服器名稱，如下列影像所示。 將滑鼠停留在 伺服器名稱以帶出**按一下以複製**選項。

    ![伺服器連接資訊](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. 如果您忘了 SQL Database 伺服器的登入資訊之後，瀏覽至 [SQL 資料庫伺服器] 頁面。 您可以檢視伺服器管理員名稱，然後必要時，重設密碼。

## <a name="connect-with-ssms"></a>使用 SSMS 連接
1. 開啟 SQL Server Management Studio。

2. **連接到伺服器**。 在**連接到伺服器**對話方塊方塊中，輸入下列資訊：

   | 設定       | 建議的值 | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器類型** | Database Engine | 這是必要的值。 |
   | **伺服器名稱** | 完整的伺服器名稱 | 名稱應該採用下列格式： **mysqldbserver.database.windows.net**。 |
   | **驗證** | SQL Server 驗證 | 本快速入門使用 SQL 驗證。 |
   | **登入** | 伺服器系統管理員帳戶 | 這是您在建立伺服器時指定的帳戶。 |
   | **密碼** | 伺服器系統管理員帳戶密碼 | 這是您在建立伺服器時指定的密碼。 |

3. **連接到 SSISDB 資料庫**。 選取**選項**展開**連接到伺服器** 對話方塊。 在展開**連接到伺服器**對話方塊中，選取**連接屬性** 索引標籤。在**連接至資料庫**欄位中，選取或輸入`SSISDB`。

4. 然後選取**連接**。

5. 在 物件總管 中，展開**Integration Services 目錄**，然後展開  **SSISDB** SSIS 目錄資料庫中檢視的物件。

## <a name="next-steps"></a>後續的步驟
- 部署封裝。 如需詳細資訊，請參閱[SSIS 專案部署與 SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md)。
- 執行封裝。 如需詳細資訊，請參閱[與 SQL Server Management Studio (SSMS) 執行 SSIS 封裝](../ssis-quickstart-run-ssms.md)。
- 排程的封裝。 如需詳細資訊，請參閱[排程 SSIS 封裝在 Azure 上的執行](ssis-azure-schedule-packages.md)

