---
title: 查詢選項結果 （方格頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.grid.f1
ms.assetid: 764bf435-3aab-4c62-b4e0-64fe020a5a95
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7c50957f59ef4e4743ca1667d6eb7a97869bec18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089010"
---
# <a name="query-options-results-grid-page"></a>查詢選項結果 (方格頁面)
  使用這個頁面即可指定選項，使查詢結果集以方格的格式顯示。  
  
## <a name="options"></a>選項  
 **在結果集裡包含查詢**  
 將查詢的文字當成結果集的一部分傳回。  
  
 **複製或儲存結果時包含資料行標頭**  
 將結果複製到剪貼簿或儲存在檔案中時，請包含資料行標頭 (標題)。 如果您不想將結果資料儲存或複製為只有資料而沒有資料行標題，請清除此核取方塊。  
  
 **執行之後捨棄結果**  
 在螢幕顯示已收到查詢結果後，將查詢結果捨棄以釋放記憶體。  
  
 **在其他索引標籤中顯示結果**  
 在新的文件視窗中顯示結果集，而非在查詢文件視窗的下方顯示。  
  
 **執行查詢後，切換至結果索引標籤**  
 自動將螢幕焦點設定為結果集。  
  
 **已擷取的最大字元數**  
 **非 XML 資料**：  
  
 輸入從 1 到 65535 的數字，來指定每個資料格中會顯示的最大字元數。  
  
> [!NOTE]  
>  指定大量字元可能造成結果集內顯示的資料截斷。 每個資料格中所顯示的最大字元數，會視字型大小而定。 若傳回了大量的結果集，且此方塊中所設定的值較大，就可能會造成 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的可用記憶體不足而降低系統的效能。  
  
 **XML 資料**：  
  
 選取 [1 MB]  、[2 MB]  或 [5 MB]  。 選取 [無限制]  以擷取所有字元。  
  
 **重設為預設值**  
 將此頁面上的所有值重設為原始預設值。  
  
  
