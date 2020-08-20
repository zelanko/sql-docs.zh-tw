---
description: SQL 模式 (MySQLToSQL)
title: SQL 模式 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 8d0631b35d2631e04cfad5c509d6084ba0a30aaf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497715"
---
# <a name="sql-modes-mysqltosql"></a>SQL 模式 (MySQLToSQL)
適用于 MySQL 的 SSMA 可在不同的 SQL 模式下運作，而且可以針對不同的用戶端以不同的方式套用這些模式。  
  
模式會定義 MySQL 應該支援的 SQL 語法，以及它應該執行的資料驗證檢查類型。 這可讓您更輕鬆地在不同的環境中使用 MySQL，以及搭配 SQL Server 使用 MySQL。  
  
## <a name="sql-modes-grid"></a>SQL 模式方格：  
  
-   根層級的 SQL 模式方格包含下列資料行： **Sql 模式名稱**、 **載入的 sql 模式**，以及 **有效的 sql 模式**。  
  
-   資料庫類別目錄、資料庫、資料表類別目錄、語句類別目錄、Views 類別目錄、資料表、視圖、函式、程式、UDF 和事件物件層級的 SQL 模式方格包含下列資料行： **SQL 模式名稱**、 **繼承的 sql 模式**，以及 **有效的 SQL 模式**。  
  
-   預存程式、預存函式和觸發層級的 SQL 模式方格包含下列資料行： **SQL 模式名稱**、  **原始 sql 模式**，以及 **有效的 sql**模式。  
  
> [!NOTE]  
> 群組模式會以粗體顯示在 [SQL 模式名稱] 資料行底下。  
  
## <a name="loaded-sql-modes"></a>載入的 SQL 模式  
這些是在會話或根層級設定的 SQL 模式。 一旦載入目標資料庫之後，就無法編輯或修改 SQL 模式。  
  
## <a name="inherited-sql-modes"></a>繼承的 SQL 模式  
這些是 SQL 模式，會繼承自對應的父節點。  
  
除了函數類別目錄、程式類別目錄、事件類別目錄和觸發程式以外，這些 SQL 模式都存在於所有層級 (資料庫、資料表類別目錄、語句類別目錄、Views 類別、資料表、視圖、函式、程式、UDF 和事件物件) 。  
  
> [!NOTE]  
> 藉由選取 [ **從父系繼承** ] 核取方塊，可以繼承自父節點的繼承 SQL 模式。 依預設，這個核取方塊會保持選取狀態。  
  
## <a name="original-sql-modes"></a>原始 SQL 模式  
這些是只存在於函式、程式和觸發層級的 SQL 模式。  
  
> [!NOTE]  
> 藉由選取 [ **使用原始** ] 核取方塊，就可以使用原本在對應函式或程式或觸發程式中使用的 SQL 模式。 依預設，這個核取方塊會保持選取狀態。  
  
## <a name="effective-sql-modes"></a>有效的 SQL 模式  
您可以透過下列方式，在不同層級定義有效的 SQL 模式：  
  
-   **在工作階段層級：**  
  
    1.  所有已載入的 SQL 模式都可以呼叫「有效的 SQL 模式」。  
  
    2.  在此層級中，可以直接且明確地修改有效的 SQL 模式。  
  
    3.  明確設定的有效 SQL 模式不會反映為已載入的 SQL 模式，最後會套用至物件。  
  
-   **在函數或程式或觸發層級：**  
  
    1.  所有的原始 SQL 模式都可以呼叫「有效的 SQL 模式」。  
  
    2.  在此層級，只有在未核取 [ **使用原始** ] 核取方塊時，才可以明確修改有效的 SQL 模式。  
  
    3.  明確設定的有效 SQL 模式不會反映為原始 SQL 模式，最後會套用至物件。  
  
-   **在函數或程式或觸發層級以外的節點：**  
  
    1.  所有繼承的 SQL 模式都可以呼叫「有效的 SQL 模式」。  
  
    2.  在此層級，只有在未核取 [ **繼承自父系** ] 核取方塊時，才可以明確修改有效的 SQL 模式。  
  
    3.  明確設定的有效 SQL 模式不會反映為繼承的 SQL 模式，最後會套用至物件。  
  
