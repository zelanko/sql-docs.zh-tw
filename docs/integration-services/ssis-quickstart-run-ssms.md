---
title: "使用 SSMS 執行 SSIS 封裝 |Microsoft 文件"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: bbc17907311785ef98560493cb453b7b9b6d1556
ms.contentlocale: zh-tw
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>執行 SSIS 封裝的 SQL Server Management Studio (SSMS)
本快速入門示範如何使用 SQL Server Management Studio (SSMS) 連接到 SSIS 目錄資料庫，然後再執行 SSIS 封裝儲存在 SSIS 目錄，在 SSMS 中的 物件總管 中。

SQL Server Management Studio 是管理任何 SQL 基礎結構，從 SQL 資料庫的 SQL Server 的整合式的環境。 如需 SSMS 的詳細資訊，請參閱[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>必要條件

開始之前，請確定您有最新版本的 SQL Server Management Studio (SSMS)。 若要下載 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="connect-to-the-ssisdb-database"></a>連接到 SSISDB 資料庫

您可以使用 SQL Server Management Studio 來連接到 SSIS 目錄。 

> [!NOTE]
> Azure SQL Database 伺服器通訊埠 1433年上接聽。 如果您嘗試連接到 Azure SQL Database 伺服器從公司防火牆內，此連接埠必須開啟在公司防火牆中針對您已成功連接。

1. 開啟 SQL Server Management Studio。

2. 在**連接到伺服器**對話方塊方塊中，輸入下列資訊：

   | 設定       | 建議的值 | 其他資訊 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器類型** | 資料庫引擎 | 這是必要的值。 |
   | **伺服器名稱** | 完整的伺服器名稱 | 如果您要連線至 Azure SQL Database 伺服器，則名稱是以下列格式： `<server_name>.database.windows.net`。 |
   | **驗證** | SQL Server 驗證 | 本快速入門使用 SQL 驗證。 |
   | **登入** | 伺服器系統管理員帳戶 | 這是您在建立伺服器時指定的帳戶。 |
   | **密碼** | 伺服器系統管理員帳戶密碼 | 這是您在建立伺服器時指定的密碼。 |

3. 按一下 **[連接]**。 在 SSMS 中，開啟 [物件總管] 視窗。 

4. 在 物件總管 中，展開**Integration Services 目錄**，然後展開  **SSISDB** SSIS 目錄資料庫中檢視的物件。

## <a name="run-a-package"></a>執行封裝

1. 在 [物件總管] 中，選取您想要執行的封裝。

2. 以滑鼠右鍵按一下並選取**Execute**。 **執行封裝**對話方塊隨即開啟。

3.  設定封裝執行所使用的設定**參數**，**連接管理員**，和**進階**執行封裝對話方塊中的索引標籤。

4.  按一下 [確定] 以執行封裝。

## <a name="next-steps"></a>後續的步驟
- 考慮以其他方式來執行封裝。
    - [使用 TRANSACT-SQL (SSMS) 執行 SSIS 封裝](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 中執行 SSIS 封裝](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 封裝](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 封裝](ssis-quickstart-run-powershell.md)
    - [使用 C# 中執行 SSIS 封裝](./ssis-quickstart-run-dotnet.md) 

