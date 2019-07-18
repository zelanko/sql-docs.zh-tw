---
title: SQL 模式 (MySQLToSQL) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944650"
---
# <a name="sql-modes-mysqltosql"></a>SQL 模式 (MySQLToSQL)
SSMA for MySQL 可在不同的 SQL 模式中操作，而且可以不同的用戶端以不同的方式套用這些模式。  
  
模式定義應該支援 MySQL、 SQL 語法，以及資料驗證的類型會檢查它應該執行。 這可讓您輕鬆地在不同的環境中使用 MySQL，並使用 MySQL 和 SQL Server。  
  
## <a name="sql-modes-grid"></a>SQL 模式方格：  
  
-   在根層級的 SQL 模式方格包含下列資料行：**SQL 模式名稱**，**載入 SQL 模式**，以及**有效 SQL 模式**。  
  
-   資料庫類別目錄、 資料庫、 資料表類別目錄、 陳述式的類別、 檢視類別目錄、 資料表、 檢視、 函式、 程序、 UDF，和事件物件層級的 SQL 模式方格包含下列資料行：**SQL 模式名稱**，**繼承 SQL 模式**，以及**有效 SQL 模式**。  
  
-   SQL 預存程序、 預存函式和觸發程序層級的模式方格包含下列資料行：**SQL 模式名稱**，**原始 SQL 模式**，以及**有效 SQL 模式**。  
  
> [!NOTE]  
> 群組模式中會顯示的資料行底下，bold 'SQL 模式 Name'。  
  
## <a name="loaded-sql-modes"></a>載入的 SQL 模式  
這些是 SQL 模式中，設定工作階段或根層級。 無法編輯或修改一次載入到目標資料庫的 SQL 模式。  
  
## <a name="inherited-sql-modes"></a>繼承的 SQL 模式  
這些是 SQL 模式中，繼承自對應的父節點。  
  
除了函式類別目錄、 程序類別目錄、 事件的類別目錄和觸發程序，這些 SQL 模式會出現在所有層級 （資料庫、 資料表類別、 陳述式的類別目錄、 檢視類別、 資料表、 檢視、 函式、 程序、 UDF 和事件的物件）。  
  
> [!NOTE]  
> 藉由選取**繼承從父代**核取方塊，繼承 SQL 模式可以繼承自父節點。 根據預設，此核取方塊保持選取狀態。  
  
## <a name="original-sql-modes"></a>原始 SQL 模式  
這些是存在 SQL 模式只函式、 程序和觸發程序的層級。  
  
> [!NOTE]  
> 藉由選取**使用原始**核取方塊，SQL 模式最初用在對應的函式或程序或觸發程序可用。 根據預設，此核取方塊保持選取狀態。  
  
## <a name="effective-sql-modes"></a>有效的 SQL 模式  
有效的 SQL 模式可定義各種不同層級，方式如下：  
  
-   **在工作階段層級：**  
  
    1.  所有載入 SQL 模式可以呼叫 「 有效的 SQL 模式 」。  
  
    2.  在此層級，有效的 SQL 模式可以直接且明確地修改。  
  
    3.  明確設定的有效 SQL 模式不會反映為載入 SQL 模式，以及最後會套用至物件。  
  
-   **在函式或程序或觸發程序層級：**  
  
    1.  所有的原始 SQL 模式可以呼叫 「 有效的 SQL 模式 」。  
  
    2.  在此層級，有效的 SQL 模式可以明確地修改時，才**使用原始**核取方塊未核取。  
  
    3.  明確設定的有效 SQL 模式無法反映做為原始的 SQL 模式，且最後會套用至物件。  
  
-   **在函式或程序或觸發程序層級以外的節點：**  
  
    1.  所有繼承 SQL 模式可以呼叫 「 有效的 SQL 模式 」。  
  
    2.  在此層級，有效的 SQL 模式可以明確地修改時，才**繼承從父代**核取方塊未核取。  
  
    3.  明確設定的有效 SQL 模式不會反映為繼承 SQL 模式，以及最後會套用至物件。  
  
