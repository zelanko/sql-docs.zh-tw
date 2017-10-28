---
title: "SQL 模式 (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 175e135f99f8ed96754ff255cbad7f32cc202479
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="sql-modes-mysqltosql"></a>SQL 模式 (MySQLToSQL)
SSMA for MySQL 可以在不同的 SQL 模式中運作，而且可以不同的用戶端以不同的方式套用這些模式。  
  
模式會定義 SQL 語法支援 MySQL、 和資料驗證的類型會檢查它應該執行。 這可讓您更容易使用 MySQL 的不同環境中，以及使用 SQL Server 與 MySQL。  
  
## <a name="sql-modes-grid"></a>SQL 模式方格：  
  
-   根層級上的 SQL 模式方格包含下列資料行： **SQL 模式名稱**，**載入 SQL 模式**，和**有效 SQL 模式**。  
  
-   資料庫類別目錄、 資料庫、 資料表類別、 陳述式的類別目錄、 檢視類別、 資料表、 檢視、 函式、 程序，UDF 和事件的物件層級 SQL 模式方格包含下列資料行： **SQL 模式名稱**，**繼承 SQL 模式**，和**有效 SQL 模式**。  
  
-   SQL 預存程序、 預存函式和觸發程序層級模式方格包含下列資料行： **SQL 模式名稱**，**原始 SQL 模式**，和**有效 SQL 模式**。  
  
> [!NOTE]  
> 群組模式中會顯示的資料行底下粗體 'SQL 模式名稱'。  
  
## <a name="loaded-sql-modes"></a>載入的 SQL 模式  
這些是 SQL 模式中，設定工作階段或根層級。 無法編輯或修改一次載入到目標資料庫的 SQL 模式。  
  
## <a name="inherited-sql-modes"></a>繼承的 SQL 模式  
這些是 SQL 模式中，繼承自相對應的父節點。  
  
除了函式類別、 程序類別目錄、 事件類別，以及觸發程序，這些 SQL 模式都出現在所有層級 （資料庫、 資料表類別目錄、 陳述式的類別目錄、 檢視類別、 資料表、 檢視、 函數、 程序、 UDF 和事件的物件）。  
  
> [!NOTE]  
> 藉由選取**從父代繼承**核取方塊，繼承 SQL 模式可以繼承自父節點。 根據預設，此核取方塊保持選取狀態。  
  
## <a name="original-sql-modes"></a>原始的 SQL 模式  
這些是存在 SQL 模式只函式、 程序和觸發程序層級。  
  
> [!NOTE]  
> 藉由選取**使用原始**核取方塊中，原本所對應的函式中使用 SQL 模式或使用程序或觸發程序。 根據預設，此核取方塊保持選取狀態。  
  
## <a name="effective-sql-modes"></a>有效的 SQL 模式  
有效的 SQL 模式可定義各種不同層級，以下列方式：  
  
-   **在工作階段層級：**  
  
    1.  所有載入 SQL 模式可以呼叫 「 有效 SQL 模式 >。  
  
    2.  在此層級，有效的 SQL 模式可以直接且明確地修改。  
  
    3.  明確設定的有效 SQL 模式不會反映為載入 SQL 模式，以及最後套用至物件。  
  
-   **在函式或程序或觸發程序層級：**  
  
    1.  在原始的 SQL 模式可以呼叫 「 有效 SQL 模式 >。  
  
    2.  在此層級，有效的 SQL 模式可以明確地修改時，才**使用原始**未選取核取方塊。  
  
    3.  明確設定的有效 SQL 模式不會反映為原始的 SQL 模式，以及最後套用至物件。  
  
-   **在函式或程序或觸發程序層級以外的節點：**  
  
    1.  所有繼承 SQL 模式可以呼叫 「 有效 SQL 模式 >。  
  
    2.  在此層級，有效的 SQL 模式可以明確地修改時，才**從父代繼承**未選取核取方塊。  
  
    3.  明確設定的有效 SQL 模式不會反映為繼承 SQL 模式，以及最後套用至物件。  
  

