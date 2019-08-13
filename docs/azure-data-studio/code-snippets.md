---
title: 建立可重複使用的程式碼片段
titleSuffix: Azure Data Studio
description: 了解如何在 Azure Data Studio 中建立和使用 SQL 程式碼片段
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 09a8432d10a70bb8530654d76bce874f735788a6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959705"
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>建立和使用程式碼片段，以便在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 中快速建立 Transact-SQL (T-SQL) 指令碼

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 中的程式碼片段是範本，讓您輕鬆建立資料庫和資料庫物件。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供數個 T-SQL 程式碼片段，協助您快速產生適當的語法。 

您也可以建立使用者定義的程式碼片段。

## <a name="using-built-in-t-sql-code-snippets"></a>使用內建 T-SQL 程式碼片段

1. 若要存取可用的程式碼片段，請在查詢編輯器中鍵入 *sql* 開啟清單：

   ![程式碼片段](media/code-snippets/sql-snippets.png)

1. 選取您要使用的程式碼片段，它會產生 T-SQL 指令碼。 例如，選取 *sqlCreateTable*：

   ![CREATE TABLE 程式碼片段](media/code-snippets/create-table.png)

1. 將醒目提示的欄位更新為您的特定值。 例如，將 *TableName* 和 *Schema* 取代為您的資料庫值：

   ![取代範本欄位](media/code-snippets/table-from-snippet.png)

   如果您要變更的欄位不再醒目提示 (當您在編輯器中四處移動游標時，就會發生這種情況)，請以滑鼠右鍵按一下您要變更的文字，然後選取 [變更所有發生次數]  ：

   ![取代範本欄位](media/code-snippets/change-all.png)

1. 更新或新增所選程式碼片段所需的其他 T-SQL。 例如，更新 *Column1*、*Column2*，並新增更多資料行。


 
## <a name="creating-sql-code-snippets"></a>建立 SQL 程式碼片段 

您可以定義自己的程式碼片段。 若要開啟 SQL 程式碼片段檔案進行編輯：

1. 開啟*命令選擇區* (**Shift+Ctrl+P**)，並鍵入 *snip*，然後選取 [喜好設定:  開啟使用者程式碼片段]：

   ![取代範本欄位](media/code-snippets/user-snippets.png)

1. 選取 [SQL]  ：

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)] 會從 Visual Studio Code 繼承程式碼片段功能，因此本文專門討論如何使用 SQL 程式碼片段。 如需詳細資訊，請參閱 Visual Studio Code 文件中的 [Creating your own snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets) (建立您自己的程式碼片段)。 

   ![取代範本欄位](media/code-snippets/select-sql.png)

1. 將下列程式碼貼到 *sql.json*：

   ```sql
   {
   "Select top 5": {
    "prefix": "sqlSelectTop5",
    "body": "SELECT TOP 5 * FROM ${1:TableName}",
    "description": "User-defined snippet example 1"
    },
    "Create Table snippet":{
    "prefix": "sqlCreateTable2",
    "body": [
    "-- Create a new table called '${1:TableName}' in schema '${2:SchemaName}'",
    "-- Drop the table if it already exists",
    "IF OBJECT_ID('$2.$1', 'U') IS NOT NULL",
    "DROP TABLE $2.$1",
    "GO",
    "-- Create the table in the specified schema",
    "CREATE TABLE $2.$1",
    "(",
    "   $1Id INT NOT NULL PRIMARY KEY, -- primary key column",
    "   Column1 [NVARCHAR](50) NOT NULL,",
    "   Column2 [NVARCHAR](50) NOT NULL",
    "   -- specify more columns here",
    ");",
    "GO"
    ],
   "description": "User-defined snippet example 2"
   }
   }
   ```

1. 儲存 sql.json 檔案。
1. 按一下 **Ctrl+N** 開啟新的查詢編輯器視窗。
2. 鍵入 **sql**，您會看到剛才新增的兩個使用者程式碼片段：*sqlCreateTable2* 和 *sqlSelectTop5*。

選取其中一個新的程式碼片段，並進行測試回合！


## <a name="additional-resources"></a>其他資源

如需 SQL 編輯器的資訊，請參閱[程式碼編輯器教學課程](tutorial-sql-editor.md)。
