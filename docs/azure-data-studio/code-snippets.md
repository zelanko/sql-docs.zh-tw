---
title: 在 Azure 資料 Studio 中建立程式碼片段 |Microsoft Docs
description: 了解如何建立和使用 Azure Data Studio 中的 SQL 程式碼片段
ms.custom: tools|sos
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.prod_service: sql-tools
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e24d1adc2c6a77d8416d63e205abc3c6c3e2f872
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "48037987"
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>透過建立與使用程式碼片段，在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 內快速地建立 TRANSACT-SQL (T-SQL) 指令碼

程式碼片段中的[!INCLUDE[name-sos](../includes/name-sos-short.md)]是範本，讓您輕鬆地建立資料庫與資料庫物件。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供數個的 T-SQL 程式碼片段，協助您快速產生正確的語法。 

也可以建立使用者定義的程式碼片段。

## <a name="using-built-in-t-sql-code-snippets"></a>使用內建的 T-SQL 程式碼片段

1. 若要存取可用的程式碼片段，請在查詢編輯器中輸入 *sql* 以開啟清單：

   ![程式碼片段](media/code-snippets/sql-snippets.png)

1. 選取您要使用的程式碼片段，並產生 T-SQL 指令碼。 例如，選取*sqlCreateTable*:

   ![建立資料表的程式碼片段](media/code-snippets/create-table.png)

1. 將反白顯示的欄位更新為特定值。 例如，依據您的資料庫，取代 *TableName* 和 *Schema* 值：

   ![取代範本欄位](media/code-snippets/table-from-snippet.png)

   如果您想要變更的欄位不再反白顯示 (當您在編輯器周圍移動游標時)，請以滑鼠右鍵按一下您想要變更文字，並選取**變更所有相符項目**：

   ![取代範本欄位](media/code-snippets/change-all.png)

1. 針對選取的程式碼片段，依據您的需求更新或加入任何額外 T-SQL。 例如，更新 *Column1*、*Column2*，並加入更多的資料欄位。


 
## <a name="creating-sql-code-snippets"></a>建立 SQL 程式碼片段 

您可以定義您自己的程式碼片段。 開啟 SQL 程式碼片段檔案進行編輯：

1. 開啟*命令選擇區* (**Shift + Ctrl + P**)，然後輸入 *snip* 並選取**喜好設定: 開啟使用者程式碼片段**：


   ![取代範本欄位](media/code-snippets/user-snippets.png)

1. 選取  **SQL**:

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)] 從 Visual Studio Code 繼承其程式碼片段的功能，因此這份文件特別說明如何使用 SQL 程式碼片段。 如需詳細資訊，請參閱 Visual Studio 程式碼文件中的[建立您自己的程式碼片段](https://code.visualstudio.com/docs/editor/userdefinedsnippets)。 

   ![取代範本欄位](media/code-snippets/select-sql.png)

1. 貼上下列程式碼插入*sql.json*:

   ```sql
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
   ```

1. 儲存 sql.json 檔案。
1. 透過按一下 **Ctrl + N** 以開啟新的 [查詢編輯器] 視窗。
2. 輸入 **sql**，然後您會看到您剛加入的兩個使用者程式碼片段：*sqlCreateTable2* 和 *sqlSelectTop5*。

選取其中一個新的程式碼片段，並進行測試 ！



## <a name="additional-resources"></a>其他資源

SQL 編輯器的相關資訊，請參閱[教學課程中的程式碼編輯器](tutorial-sql-editor.md)。
