---
title: 在 Azure 中執行 SSIS 套件 | Microsoft Docs
description: 提供可用於執行部署到 Azure SQL Database 之 SSIS 套件的方法概觀。
ms.date: 05/29/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
manager: craigg
ms.openlocfilehash: 8b91a1572e5c7cd477d8e112b68b8f9a46fb1153
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012331"
---
# <a name="run-sql-server-integration-services-ssis-packages-deployed-in-azure"></a>執行部署於 Azure 中的 SQL Server Integration Services (SSIS) 套件

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



您可以選擇本文中所述的其中一個方法，來執行部署到 Azure SQL Database 伺服器上 SSISDB 目錄的 SSIS 套件。 您可以直接執行套件，或將套件當作 Azure Data Factory 管線的一部分來執行。 如需 Azure 上 SSIS 的概觀，請參閱[在 Azure 中部署和執行 SSIS 套件](ssis-azure-lift-shift-ssis-packages-overview.md)。

- 直接執行套件

  - [使用 SSMS 執行](#ssms)

  - [使用預存程序執行](#sproc)

  - [使用指令碼或程式碼執行](#script)

- 將套件當作 Azure Data Factory 管線的一部分來執行

  - [使用執行 SSIS 套件活動執行](#exec_activity)

  - [使用預存程序活動執行](#sproc_activity)

> [!NOTE]
> 使用 `dtexec.exe` 執行套件的功能尚未在部署到 Azure 的套件上進行測試。

## <a name="ssms"></a> 使用 SSMS 執行套件

在 SQL Server Management Studio (SSMS) 中，您可以在部署到 SSIS 目錄資料庫 (SSISDB) 的套件上按一下滑鼠右鍵，然後選取 [執行]  以開啟 [執行套件]  對話方塊。 如需詳細資訊，請參閱[使用 SQL Server Management Studio (SSMS) 執行 SSIS 套件](../ssis-quickstart-run-ssms.md)。

## <a name="sproc"></a> 使用預存程序執行套件

在您可以連線到 Azure SQL Database 並執行 Transact-SQL 程式碼的任何環境中，您可以藉由呼叫下列預存程序來執行套件：

1. **[catalog].[create_execution]** 。 如需詳細資訊，請參閱 [catalog.create_execution](../system-stored-procedures/catalog-create-execution-ssisdb-database.md)。

2. **[catalog].[set_execution_parameter_value]** 。 如需詳細資訊，請參閱 [catalog.set_execution_parameter_value](../system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)。

3. **[catalog].[start_execution]** . 如需詳細資訊，請參閱 [catalog.start_execution](../system-stored-procedures/catalog-start-execution-ssisdb-database.md)。

如需詳細資訊，請參閱下列範例：

- [使用 Transact-SQL 從 SSMS 執行 SSIS 套件](../ssis-quickstart-run-tsql-ssms.md)

- [使用 Transact-SQL 從 Visual Studio Code 執行 SSIS 套件](../ssis-quickstart-run-tsql-vscode.md)

## <a name="script"></a> 使用指令碼或程式碼執行套件

在您可以呼叫受控 API 的任何開發環境中，您可以藉由呼叫 `Microsoft.SQLServer.Management.IntegrationServices` 命名空間中 `Package` 物件的 `Execute` 方法來執行套件。

如需詳細資訊，請參閱下列範例：

- [使用 PowerShell 執行 SSIS 套件](../ssis-quickstart-run-powershell.md)

- [在 .NET 應用程式中使用 C# 程式碼執行 SSIS 套件](../ssis-quickstart-run-dotnet.md)

## <a name="exec_activity"></a> 使用執行 SSIS 套件活動執行套件

如需詳細資訊，請參閱[在 Azure Data Factory 中使用執行 SSIS 套件活動執行 SSIS 套件](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)。

## <a name="sproc_activity"></a> 使用預存程序活動執行套件

如需詳細資訊，請參閱[在 Azure Data Factory 中使用預存程序活動執行 SSIS 套件](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity)。

## <a name="next-steps"></a>後續步驟

深入了解排程部署到 Azure 之 SSIS 套件的選項。 如需詳細資訊，請參閱[在 Azure 中排程 SSIS 套件](ssis-azure-schedule-packages.md)。
