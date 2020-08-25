---
title: Azure Data Studio 中的 SQL 核心筆記本
description: 本教學課程說明如何建立和執行 SQL Server 筆記本。
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray, alayu
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 07/01/2020
ms.openlocfilehash: 022950fa27887618f16e5569ffe3370c069ea71c
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745858"
---
# <a name="create-and-run-a-sql-server-notebook"></a>建立並執行 SQL Server 筆記本

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本教學課程示範如何使用 SQL Server 在 Azure Data Studio 中建立及執行筆記本。

## <a name="prerequisites"></a>Prerequisites

- [已安裝 Azure Data Studio](download-azure-data-studio.md)
- 已安裝 SQL Server
  - [Windows](../database-engine/install-windows/install-sql-server.md)
  - [Linux](../linux/sql-server-linux-setup.md)

## <a name="create-a--notebook"></a>建立筆記本

下列步驟說明如何在 Azure Data Studio 中建立筆記本檔案：

1. 在 Azure Data Studio 中，連線到 SQL Server。

1. 在 [伺服器]  視窗中，於 [連線]  下方選取。 然後選取 [新增筆記本]  。

   ![開啟筆記本](media/notebook-tutorial/azure-data-studio-open-notebook.png)

1. 等候 [核心]  和目標內容 ([附加至]  ) 填入。 確認 [核心] 已設定為 [SQL]，並為 SQL Server 設定 [附加至] (在此範例為 *localhost*)。

   ![設定 [核心] 和 [附加至]](media/notebook-tutorial/set-kernel-and-attach-to.png)

您可從 [檔案] 功能表使用 [儲存] 或 [另存新檔...] 命令來儲存筆記本。 

若要開啟筆記本，您可從 [檔案] 功能表使用 [開啟檔案...] 命令，在 [歡迎使用] 頁面上選取 [開啟檔案]，或從命令選擇區使用 [檔案:開啟] 命令。

## <a name="change-the-sql-connection"></a>變更 SQL 連線

若要變更筆記本的 SQL 連線：

1. 選取筆記本工具列中的 [附加至]  功能表，然後選取 [變更連線]  。

   ![按一下筆記本工具列中的 [附加至] 功能表](./media/notebook-tutorial/select-attach-to-1.png)

2. 您現在可以選取最近的連線伺服器，或輸入新的連線詳細資料來連線。

   ![從 [附加至] 功能表選取伺服器](./media/notebook-tutorial/select-attach-to-2.png)

## <a name="run-a-code-cell"></a>執行程式碼資料格

您可建立資料格，其中包含可藉由按一下資料格左邊 [執行資料格] 按鈕 (圓形黑色箭號) 來就地執行的 SQL 程式碼。 資料格完成執行之後，會在筆記本中顯示結果。

例如：

1. 選取工具列中的 [+程式碼]  命令來新增程式碼儲存格。

   ![筆記本工具列](media/notebooks-guidance/notebook-toolbar.png)

1. 將下列範例複製並貼到資料格中，然後按一下 [執行資料格]。 此範例會建立新的資料庫。

   ```sql
   USE master
   GO
   
   -- Drop the database if it already exists
   IF  EXISTS (
           SELECT name
           FROM sys.databases
           WHERE name = N'TestNotebookDB'
      )
   DROP DATABASE TestNotebookDB
   GO
   
   -- Create the database
   CREATE DATABASE TestNotebookDB
   GO
   ```

   ![執行筆記本資料格](media/notebook-tutorial/run-notebook-cell.png)

## <a name="save-the-result"></a>儲存結果

如果執行會傳回結果的指令碼，則可使用結果上方所顯示的工具列，將該結果儲存為不同的格式。

- 另存為 CSV
- 另存為 Excel
- 另存為 JSON
- 另存為 XML

例如，下列程式碼會傳回 [PI](../t-sql/functions/pi-transact-sql.md) 的結果。

```sql
SELECT PI() AS PI;
GO
```

![執行筆記本資料格](media/notebook-tutorial/run-notebook-cell-2.png)

## <a name="next-steps"></a>後續步驟

深入了解筆記本：

- [如何在 Azure Data Studio 中使用筆記本](notebooks-guidance.md)
- [建立及執行 Python 筆記本](notebooks-tutorial-python-kernel.md)
- [執行使用 Spark 的範例筆記本](../big-data-cluster/notebooks-tutorial-spark.md)