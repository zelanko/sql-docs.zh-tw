---
title: 連線至 Azure 中的 SSIS 目錄 (SSISDB) | Microsoft Docs
description: 尋找連線至 Azure SQL Database 伺服器上裝載之 SSIS 目錄 (SSISDB) 所需的連線資訊。
ms.date: 09/25/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 00e2c2e9ce845a6775ea4baee458253ba5e1162c
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35405670"
---
# <a name="connect-to-the-ssis-catalog-ssisdb-in-azure"></a>連線至 Azure 中的 SSIS 目錄 (SSISDB)

尋找連線至 Azure SQL Database 伺服器上裝載之 SSIS 目錄 (SSISDB) 所需的連線資訊。 您需要下列項目來進行連線：
- 完整伺服器名稱
- 資料庫名稱
- 登入資訊 

> [!IMPORTANT]
> 目前，需要在 Azure Data Factory 第 2 版中建立 Azure-SSIS Integration Runtime，才能在 Azure SQL Database 上建立 SSISDB 目錄資料庫。 Azure-SSIS IR 是在 Azure 上執行 SSIS 套件的執行階段環境。 如需處理序的逐步解說，請參閱[在 Azure 中部署和執行 SSIS 套件](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)。 

## <a name="prerequisites"></a>Prerequisites
開始之前，請確定您有 17.2 版或更新版本的 SQL Server Management Studio (SSMS)。 如果 SSISDB 目錄資料庫託管在 SQL Database 受控執行個體 (預覽) 上，請確定您具有 17.6 版或更新版本的 SSMS。 若要下載最新版的 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="get-the-connection-info-from-the-azure-portal"></a>從 Azure 入口網站取得連線資訊
1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 在 Azure 入口網站中，從左側功能表選取 [SQL 資料庫]，然後選取 [SQL 資料庫] 頁面上的 `SSISDB` 資料庫。 
3. 在 `SSISDB` 資料庫的 [概觀] 頁面上，檢閱完整伺服器名稱，如下列影像所示。 將滑鼠指標放在伺服器名稱上方，以顯示 [按一下以複製] 選項。

    ![伺服器連線資訊](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. 如果您忘了 SQL Database 伺服器的登入資訊，請巡覽至 [SQL 資料庫伺服器] 頁面。 在該處，您可以檢視伺服器系統管理員名稱，並於必要時重設密碼。

## <a name="connect-with-ssms"></a>使用 SSMS 連線
1. 開啟 SQL Server Management Studio。

2. **連線至伺服器**。 在 [連線至伺服器] 對話方塊中，輸入下列資訊：

   | 設定       | 建議值 | 描述 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器類型** | Database Engine | 這是必要的值。 |
   | **伺服器名稱** | 完整伺服器名稱 | 名稱的格式應如下所示：**mysqldbserver.database.windows.net**。 |
   | **驗證** | SQL Server 驗證 | |
   | **登入** | 伺服器系統管理員帳戶 | 這是您在建立伺服器時指定的帳戶。 |
   | **密碼** | 伺服器系統管理員帳戶的密碼 | 這是您在建立伺服器時指定的密碼。 |

    ![使用 SSMS 連線到伺服器](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-1.png)

3. **連線至 SSISDB 資料庫**。 選取 [選項] 以展開 [連線至伺服器] 對話方塊。 在展開的 [連線至伺服器] 對話方塊中，選取 [連線屬性] 索引標籤。在 [連線至資料庫] 欄位中，選取或輸入 `SSISDB`。

    > [!IMPORTANT]
    > 如果您在連線時沒有選取 `SSISDB`，則可能不會在 [物件總管] 中看到 SSIS 目錄。

    ![選取連線的 SSISDB 資料庫](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-2.png)

4. 然後選取 [連線]。

5. 在 [物件總管] 中，展開 [Integration Services 目錄]，然後展開 [SSISDB] 以檢視 SSIS 目錄資料庫中的物件。

    ![在 SSMS 中的物件總管中尋找 SSISDB 資料庫](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-3.png)

## <a name="next-steps"></a>後續步驟
- 部署套件。 如需詳細資訊，請參閱[使用 SQL Server Management Studio (SSMS) 部署 SSIS 專案](../ssis-quickstart-deploy-ssms.md)。
- 執行套件。 如需詳細資訊，請參閱[使用 SQL Server Management Studio (SSMS) 執行 SSIS 套件](../ssis-quickstart-run-ssms.md)。
- 排程套件。 如需詳細資訊，請參閱[在 Azure 中排程 SSIS 套件](ssis-azure-schedule-packages.md)
