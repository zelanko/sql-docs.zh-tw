---
title: 選項 (查詢結果-SQL Server-以結果文字頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToText
ms.assetid: 2ccbdf17-e14f-42f1-a836-ca999a3432c9
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 2810a8738368f87651bc90d6cb15ae34195258ab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105520"
---
# <a name="options-query-results-sql-server-results-to-text-page"></a>選項 (查詢結果-SQL Server-以結果文字頁面）
  使用此頁面，即可指定以文字格式顯示查詢結果集的選項。 這些選項的變更僅適用於新的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢。 若要變更目前查詢的選項，請按一下 [查詢] 功能表上的 [查詢選項]，或以滑鼠右鍵按一下 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢] 視窗，然後選取 [查詢選項]。 在 **[查詢選項]** 對話方塊中，於 **[結果]** 之下，按一下 **[文字]**。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **輸出格式**  
 根據預設，輸出會顯示在以空格填補結果所建立的資料行中。 其他選項為使用逗號、定位點或空格來分隔資料行。 在此下拉式清單中選取 [自訂分隔符號]，即可在 [自訂分隔符號] 文字方塊中指定不同的分隔字元。  
  
 **自訂分隔符號**  
 指定您要用來分隔資料行的字元。 此文字方塊只有在 [輸出格式] 下拉式清單方塊中，按一下自訂分隔符號時才能使用。  
  
 **在結果集內包含資料行標頭**  
 如果您不要每個資料行均標示有資料行標題，請清除此核取方塊。  
  
 **在結果集裡包含查詢**  
 選取此核取方塊，即可在查詢結果的前面，包含正在結果窗格中執行之查詢的查詢文字。  
  
 **收到結果時捲動**  
 選取此核取方塊，將顯示焦點放在結果集尾端最新傳回的記錄。 清除此核取方塊，即可將作用中的顯示保持為接收到的第一組資料列。  
  
 **數值靠右對齊**  
 選取此核取方塊，即可將數值靠資料行的右邊對齊。 如此可便於檢閱有固定小數位數的數字。  
  
 **執行查詢之後捨棄結果**  
 選取此核取方塊，當查詢結果顯示於查詢視窗的結果窗格之後，即捨棄查詢結果。  
  
 **在其他索引標籤中顯示結果**  
 選取此核取方塊，即可在新的文件視窗中顯示結果集，而非在查詢文件視窗的下方顯示。  
  
 **執行查詢後，切換至結果索引標籤**  
 選取此核取方塊以自動將螢幕焦點設定為結果集。  
  
 **每個資料行中顯示的最大字元數**  
 這個值預設為 256。 增加這個值即可顯示較大的結果集而不會截斷。 最大值為 8,192。  
  
 **重設為預設值**  
 將此頁面上的所有值重設為原始預設值。  
  
  
