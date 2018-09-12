---
title: 使用 查詢和檢視表設計工具操作國際資料 (Visual Database Tools) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Visual Database Tools [SQL Server], international data
- queries [SQL Server], international data
- languages [SQL Server], Query and View Designer
- international considerations [SQL Server], Query and View Designer
- Criteria pane
- View Designer, international data
- Query Designer [SQL Server], international data
- localized information in Query and View Designer [SQL Server]
- global considerations [SQL Server], Query and View Designer
- SQL pane [Visual Database Tools]
- multiple language support [SQL Server], Query and View Designer
ms.assetid: 4b51c56f-f902-4e72-b919-e36127369b63
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b0e08dfcd8c87ece10ee8a741a9f0ba1737b5423
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43807595"
---
# <a name="use-the-query-and-view-designer-with-international-data-visual-database-tools"></a>使用查詢和檢視表設計工具操作國際資料 (Visual Database Tools)
  您可以使用[查詢和檢視表設計工具](visual-database-tools.md)處理任何語言的資料，並在任何版本的 Windows 作業系統中執行。 下列方針即簡要說明您將注意到的不同處，並提供管理國際應用程式資料的資訊。  
  
## <a name="localized-information-in-the-criteria-and-sql-panes"></a>準則和 SQL 窗格的當地語系化文化資訊  
 如果使用 [準則] 窗格建立查詢，可以用符合於您電腦的 Windows [地區選項] 的格式來輸入資訊。 例如，如果您要搜尋資料，您可以使用您習慣使用的格式在 [準則] 資料行中輸入資料，但以下為例外情況：  
  
-   不支援長資料格式。  
  
-   [準則] 窗格中無法輸入貨幣符號。  
  
-   貨幣符號將不會顯示在 [結果] 窗格中。  
  
    > [!NOTE]  
    >  在 [結果] 窗格中，雖然實際上可以輸入符合您電腦的 Windows 地區設定之貨幣符號，但是在 [結果] 窗格中，此符號將會移除且不會顯示。  
  
-   不論 [區域設定] 選項為何，一元 (Unary) 負號固定出現在左邊 (例如，-1)。  
  
 相對的，[SQL] 窗格的資料和關鍵字必須一律為 ANSI (U.S.) 格式。 例如，查詢和檢視設計師建置某個查詢，該查詢插入所有 ANSI 格式的 SQL 關鍵字，如 SELECT 和 FROM。 如果您新增項目至 [SQL] 窗格的陳述式，請務必使用該元件的 ANSI 標準格式。  
  
 當您在 [準則] 窗格中使用特定地區設定格式輸入資料時，[查詢和檢視設計師] 會在 [SQL] 窗格中自動將該資料轉譯為 ANSI 格式。 例如，如果您的 [地區設定] 為 Standard German，您可以使用 "31.12.96" 的格式在 [準則] 窗格中輸入資料。 然而，資料將以 ANSI 日期時間的格式出現在 [SQL] 窗格中，如 `{ ts '1996-12-31 00:00:00' }.` 。如果直接在 [SQL] 窗格中輸入資料，則必須以 ANSI 格式輸入。  
  
## <a name="sort-order"></a>[排序順序]  
 資料庫將決定您查詢中資料的排序次序。 您在 Windows [區域設定] 對話方塊中設定的選項並不會影響查詢的排序次序。 但在特定查詢中，您可以要求使用特定順序傳回資料列。  
  
## <a name="using-double-byte-characters"></a>使用雙位元組字元  
 您可以輸入 DBCS 字元做為常值或資料庫物件名稱，如資料表和檢視名稱或別名。 您也可以使用 DBCS 字元做為參數名稱或參數標記字元。 但是您無法在 SQL 項目中 (如函數名稱或 SQL 關鍵字) 使用 DBCS 字元。  
  
## <a name="see-also"></a>另請參閱  
 [設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
