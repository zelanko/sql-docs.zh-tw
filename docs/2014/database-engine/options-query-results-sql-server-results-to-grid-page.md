---
title: 選項（查詢結果-SQL Server-以方格顯示結果頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToGrid
ms.assetid: f88a0f5c-e800-473b-ae23-c3943de5ed63
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: b67926706674abb116b4f3075089853e6fbb665e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089305"
---
# <a name="options-query-results-sql-server-results-to-grid-page"></a>選項（查詢結果-SQL Server-以方格顯示結果頁面）
  使用這個頁面即可指定選項，使查詢結果集以方格的格式顯示。 這些選項的變更僅適用於新的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢。 若要變更目前查詢的選項，請按一下 [**查詢**] 功能表上的 [**查詢選項**]，或在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]查詢視窗中按一下滑鼠右鍵，然後選取 [**查詢選項**]。 在 [查詢選項]**** 對話方塊的左窗格中，於 [結果]**** 之下，按一下 [方格]****。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **在結果集裡包含查詢**  
 將查詢的文字傳回作為查詢輸出的一部分。  
  
 **複製或儲存結果時包含資料行標頭**  
 將結果複製到剪貼簿或儲存在檔案中時，選取此核取方塊即可包含資料行標頭。 如果您想要儲存或複製的結果資料中只有資料，而不要有資料行標頭，請清除這個核取方塊。  
  
 **執行之後捨棄結果**  
 避免查詢結果顯示在檢閱窗格中。 執行之後會立即捨棄結果。 指定這個選項有助於節省記憶體。  
  
 **在其他索引標籤中顯示結果**  
 核取此核取方塊即可在新的索引標籤中顯示結果集，而不是顯示在查詢文件視窗的底部。  
  
 **執行查詢後，切換至結果索引標籤**  
 按一下即可在開始執行查詢時，自動將螢幕焦點設定為結果窗格。  
  
 **已擷取的最大字元數**  
 **非 XML 資料**：  
  
 輸入從 1 到 65535 的數字，來指定每個資料格中會顯示的最大字元數。  
  
> [!NOTE]  
>  指定大量字元可能造成結果集內顯示的資料截斷。 每個資料格中所顯示的最大字元數，會視字型大小而定。 若傳回了大量的結果集，且此方塊中所設定的值較大，就可能會造成 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的可用記憶體不足而降低系統的效能。  
  
 **XML 資料**：  
  
 選取 [1 MB]****、[2 MB]**** 或 [5 MB]****。 選取 [無限制]**** 以擷取所有字元。  
  
 **重設為預設值**  
 將此頁面上的所有值重設為原始預設值。  
  
  
