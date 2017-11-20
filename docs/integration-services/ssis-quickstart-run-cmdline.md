---
title: "從命令提示字元中執行 SSIS 封裝 |Microsoft 文件"
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
ms.openlocfilehash: a33b8518ec3284f5de73d38c87209057dc1c7487
ms.contentlocale: zh-tw
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>從 DTExec.exe 在命令提示字元中執行 SSIS 封裝
本快速入門教學課程示範如何從命令提示字元中執行 SSIS 封裝，藉由執行`DTExec.exe`以適當的參數。

> [!NOTE]
> 在本文中所述的方法尚未經過測試與部署到 Azure SQL Database 伺服器的封裝。

如需詳細資訊`DTExec.exe`，請參閱[dtexec 公用程式](https://docs.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility)。

## <a name="run-a-package-with-dtexec"></a>使用 dtexec 執行封裝

如果資料夾包含`DTExec.exe`不在您`path`可能要使用的環境變數`cd`命令來變更為它的目錄。 若是 SQL Server 2017，此資料夾通常位於`C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`。

下列範例中所使用的參數值，程式會執行封裝中指定的資料夾路徑 SSIS 伺服器-也就是裝載 SSIS 目錄資料庫 (SSISDB) 的伺服器上。 `/Server`參數可讓您的伺服器名稱。 程式會以目前的使用者使用 Windows 整合式驗證連接。 若要使用 SQL 驗證，指定`/User`和`Password`參數以適當的值。

1. 開啟 [命令提示字元] 視窗。

2. 執行`DTExec.exe`並至少提供的值`ISServer`和`Server`參數，如下列範例所示：

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>後續的步驟
- 考慮以其他方式來執行封裝。
    - [使用 SSMS 執行 SSIS 封裝](./ssis-quickstart-run-ssms.md)
    - [使用 TRANSACT-SQL (SSMS) 執行 SSIS 封裝](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 中執行 SSIS 封裝](ssis-quickstart-run-tsql-vscode.md)
    - [使用 PowerShell 執行 SSIS 封裝](ssis-quickstart-run-powershell.md)
    - [使用 C# 中執行 SSIS 封裝](./ssis-quickstart-run-dotnet.md) 

