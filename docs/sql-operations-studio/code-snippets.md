---
title: 建立程式碼片段中 SQL Operations Studio （預覽） |Microsoft 文件
description: 了解如何建立和使用 SQL Operations Studio （預覽） 中的 SQL 程式碼片段
ms.custom: tools|sos
ms.date: 11/15/2017
ms.reviewer: alayu; erickang; sstein
ms.prod: sql-non-specified
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4670c824b1e52776c3d81d097beeb4ccd9e62e2d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>建立並快速地建立 TRANSACT-SQL (T-SQL) 指令碼中的使用程式碼片段[!INCLUDE[name-sos](../includes/name-sos-short.md)]

程式碼片段中的[!INCLUDE[name-sos](../includes/name-sos-short.md)]是範本，讓您更輕鬆地建立資料庫和資料庫物件。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]提供數個的 T-SQL 程式碼片段以協助您進行快速產生適當的語法。 

您也可以建立使用者定義的程式碼片段。

## <a name="using-built-in-t-sql-code-snippets"></a>使用內建的 T-SQL 程式碼片段

1. 若要存取可用的程式碼片段，請輸入*sql*在查詢編輯器中開啟清單：

   ![程式碼片段](media/code-snippets/sql-snippets.png)

1. 選取您要使用的程式碼片段，並在產生 T-SQL 指令碼。 例如，選取*sqlCreateTable*:

   ![建立資料表的程式碼片段](media/code-snippets/create-table.png)

1. 更新的特定值的反白顯示的欄位。 例如，取代*TableName*和*結構描述*資料庫的值：

   ![取代範本欄位](media/code-snippets/table-from-snippet.png)

   如果您想要變更的欄位不會再反白顯示 （這樣當您移動游標周圍編輯器），以滑鼠右鍵按一下您想要變更，並選取的 word**變更所有相符項目**:

   ![取代範本欄位](media/code-snippets/change-all.png)

1. 更新或新增選取的程式碼片段所需任何額外 T-SQL。 例如，更新*Column1*， *Column2*，並加入更多的資料行。


 
## <a name="creating-sql-code-snippets"></a>建立 SQL 程式碼片段 

您可以定義您自己的程式碼片段。 若要開啟 SQL 程式碼片段檔案進行編輯：

1. 開啟*命令選擇區*(**Shift + Ctrl + P**)，然後輸入*剪取*，然後選取**喜好設定： 開啟使用者程式碼片段**:

   ![取代範本欄位](media/code-snippets/user-snippets.png)

1. 選取**SQL**:

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)]從 Visual Studio 程式碼繼承其功能的程式碼片段，因此這份文件特別說明如何使用 SQL 程式碼片段。 如需詳細資訊，請參閱[建立您自己的程式碼片段](https://code.visualstudio.com/docs/editor/userdefinedsnippets)Visual Studio 程式碼文件中。 

   ![取代範本欄位](media/code-snippets/select-sql.png)

1. 貼上下列程式碼*sql.json*:

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
1. 開啟新的 [查詢編輯器] 視窗，依序按一下**Ctrl + N**。
2. 型別**sql**，而且您會看到您剛才加入; 兩個使用者程式碼片段*sqlCreateTable2*和*sqlSelectTop5*。

選取其中一個新的程式碼片段，並為它提供的測試回合 ！


## <a name="additional-resources"></a>其他資源

SQL 編輯器的相關資訊，請參閱[教學課程中的程式碼編輯器](tutorial-sql-editor.md)。