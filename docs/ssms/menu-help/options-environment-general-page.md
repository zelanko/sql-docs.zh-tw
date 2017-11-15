---
title: "選項 (環境 - 一般頁面) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.TOOLSOPTIONSPAGES.ENVIRONMENT.GENERAL
- VS.ToolsOptionsPages.Environment.SQLEnvironmentOptions
- DevLang-TSQL
ms.assetid: c32ccdb8-2cf8-4c78-b474-a3abd3dbbd13
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a3862d6f6b622ddd0496b23234287443e179810
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="options-environment---general-page"></a>選項 (環境 - 一般頁面)
使用 [選項] 對話方塊，來設定 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 的啟動動作、一般視窗管理選項，以及其他一般設定。 在 [工具] 功能表上按一下 [選項]、展開 [環境] 資料夾，然後按一下 [一般]。  
  
## <a name="uielement-list"></a>UIElement 清單  
**啟動時**  
選取 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 啟動時要執行的動作。 選項包括：  
  
-   [開啟物件總管] 會提示進行連接，然後開啟物件總管。  
  
-   [開啟新增查詢視窗] 會提示進行連接，然後開啟 SQL 查詢編輯器。  
  
-   [開啟物件總管和新增查詢] 會提示進行連接，然後使用該連接開啟物件總管和 SQL 查詢編輯器。  
  
-   [開啟空白環境] 會開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]，但沒有 SQL 查詢編輯器視窗，且不會將物件總管連接到伺服器。  
  
**在 [物件總管] 中隱藏系統物件**  
選取此核取方塊，即可從 [物件總管] 中的樹狀檢視裡，移除系統資料庫、系統資料表、系統檢視，以及系統預存程序。 系統函數與系統資料類型並未隱藏。 此選項僅適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的執行個體，且不會影響在 [物件總管] 中已經連接的伺服器。  
  
## <a name="environment-layout"></a>環境配置  
您必須關閉再重新開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ，才能在索引標籤式文件與多重文件介面 (MDI) 環境模式之間變更。  
  
**索引標籤式文件**  
選取此選項即可顯示在編輯器內，以索引標籤組合在一起的多個文件視窗。 索引標籤式文件視窗適用於組織多個開啟的文件以及在它們之間切換。  
  
**MDI 環境**  
選取此選項即可在 MDI 環境中開啟文件。 MDI 文件視窗可以讓螢幕空間更大，因為原來由索引標籤式文件環境中之索引標籤佔據的螢幕空間，也可以使用。 以 MDI 模式工作時，您可以按下 CTRL+TAB，或使用位於 [視窗] 功能表上的並列選項，在文件之間切換。  
  
## <a name="docked-tool-window-behavior"></a>停駐工具視窗行為  
**關閉按鈕只會影響使用中的索引標籤**  
指定若選取了此核取方塊，只會關閉目前具有焦點的工具視窗，而不會關閉停駐集內的所有工具視窗。 依預設，這個核取方塊為已選取。  
  
**自動隱藏按鈕只會影響使用中的索引標籤**  
指定若選取了此核取方塊，只會自動隱藏目前具有焦點的工具視窗，而不會隱藏停駐集內的所有工具視窗。 依預設，不會勾選此核取方塊。  
  
## <a name="display"></a>顯示器  
**顯示最近使用清單中的 n 個檔案**  
自訂 [檔案] 功能表上所顯示之最近使用的專案與最近使用之檔案的數目。 輸入介於 1 到 24 之間的數字。 預設值是 4。 這是方便用來擷取最近使用過的指令碼專案和檔案，以及編寫專案的方式。  
  
