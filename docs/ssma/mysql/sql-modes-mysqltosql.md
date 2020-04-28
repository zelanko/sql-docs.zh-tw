---
title: SQL 模式（MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2c9dbd2b42ebde4cdfea602c3ad50c4b7d100bb2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67944650"
---
# <a name="sql-modes-mysqltosql"></a>SQL 模式 (MySQLToSQL)
適用于 MySQL 的 SSMA 可以在不同的 SQL 模式下運作，而且可以針對不同的用戶端以不同的方式套用這些模式。  
  
模式會定義 MySQL 應該支援的 SQL 語法，以及應該執行的資料驗證檢查類型。 這可讓您更輕鬆地在不同的環境中使用 MySQL，並使用 SQL Server 的 MySQL。  
  
## <a name="sql-modes-grid"></a>SQL 模式格線：  
  
-   根層級的 SQL 模式方格包含下列資料行： **Sql 模式名稱**、**載入的 Sql 模式**和**有效的 sql 模式**。  
  
-   [資料庫] 類別、[資料庫]、[資料表類別目錄]、[語句類別]、[Views] 類別、[資料表]、[視圖]、[函數]、[程式]、 **[** UDF]**和 [事件**物件層級] 的 sql 模式方格包含下列資料行： **SQL 模式名稱**、繼承的 sql  
  
-   預存程式、預存函數和觸發層級的 SQL 模式方格包含下列資料行： **SQL 模式名稱**、**原始 Sql 模式**和**有效的 sql 模式**。  
  
> [!NOTE]  
> 群組模式會以粗體顯示，在「SQL 模式名稱」資料行底下。  
  
## <a name="loaded-sql-modes"></a>已載入 SQL 模式  
這些是在會話或根層級設定的 SQL 模式。 載入目標資料庫後的 SQL 模式無法編輯或修改。  
  
## <a name="inherited-sql-modes"></a>繼承的 SQL 模式  
這些是 SQL 模式，繼承自對應的父節點。  
  
除了函式類別、程式分類、事件類別目錄和觸發程式以外，這些 SQL 模式會出現在所有層級（資料庫、資料表類別、語句類別、Views 分類、資料表、視圖、函數、程式、UDF 和事件物件）。  
  
> [!NOTE]  
> 藉由選取 [**繼承自父系**] 核取方塊，繼承的 SQL 模式可以繼承自父節點。 根據預設，此核取方塊會保持選取狀態。  
  
## <a name="original-sql-modes"></a>原始 SQL 模式  
這些是只有函數、程式和觸發層級出現的 SQL 模式。  
  
> [!NOTE]  
> 藉由選取 [**使用原始**的] 核取方塊，就可以使用原本用於對應函式或程式或觸發程式的 SQL 模式。 根據預設，此核取方塊會保持選取狀態。  
  
## <a name="effective-sql-modes"></a>有效的 SQL 模式  
有效的 SQL 模式可以透過下列方式在各種層級上定義：  
  
-   **在工作階段層級：**  
  
    1.  所有已載入的 SQL 模式都可以呼叫「有效的 SQL 模式」。  
  
    2.  在此層級，有效的 SQL 模式可以直接和明確地修改。  
  
    3.  明確設定的有效 SQL 模式不會反映為載入的 SQL 模式，最後會套用至物件。  
  
-   **在函式或程式或觸發層級：**  
  
    1.  所有的原始 SQL 模式都可以稱為「有效的 SQL 模式」。  
  
    2.  在此層級中，只有在未核取 [**使用原始**] 核取方塊時，才可以明確修改有效的 SQL 模式。  
  
    3.  明確設定的有效 SQL 模式不會反映為原始 SQL 模式，最後會套用至物件。  
  
-   **在函數或程式或觸發層級以外的節點上：**  
  
    1.  所有繼承的 SQL 模式都可以呼叫「有效的 SQL 模式」。  
  
    2.  在此層級中，只有在未核取 [**從父系繼承**] 核取方塊時，才可以明確修改有效的 SQL 模式。  
  
    3.  明確設定的有效 SQL 模式不會反映為繼承的 SQL 模式，最後會套用至物件。  
  
