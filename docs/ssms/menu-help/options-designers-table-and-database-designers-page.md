---
title: "選項 (設計工具 - 資料表和資料庫設計工具頁面) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Designers.Table_Designer
ms.assetid: b43f4b97-17b9-4004-a824-f77b9e145741
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 79e728f7cf2c300338e202b3e9cae27226f70a50
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="options-designers---table-and-database-designers-page"></a>選項 (設計工具 - 資料表和資料庫設計工具頁面)
使用此頁面來決定設計師的預設行為。 若要存取設定，請在 [工具] 功能表上按一下 [選項]、展開 [設計工具] 資料夾，然後按一下 [資料表設計工具]。  
  
## <a name="uielement-list"></a>UIElement 清單  
**覆寫資料表設計師更新的連接字串逾時值**  
允許針對資料表設計師之動作設定新的逾時值。 當資料表設計師影響大型資料表而需要額外的時間來完成資料表修改時，這就非常有用。  
  
**交易逾時設定值**  
設定資料表設計師的逾時值。  
  
**自動產生變更指令碼**  
自動建立指令碼以實作資料表設計師中所定義的變更。  
  
**針對 Null 主索引鍵產生警告**  
當選取作為主索引鍵的欄位可以包含 Null 值時，提供警告對話方塊。  
  
**警告差異偵測**  
如果核取這個方塊，則當儲存變更時，有一個訊息方塊會列出您所進行之變更與另一位使用者所進行之變更的任何衝突。  
  
**警告受影響資料表**  
提供一個警告對話方塊，其中會列出受此動作影響的資料表並提示確認。  
  
**防止儲存需要資料表重建的變更**  
便免使用者進行需要資料表重建的變更。 下列動作可能需要重新建立資料表：  
  
-   將新的資料行加入資料表的中間  
  
-   卸除資料行  
  
-   變更資料行的 Null 屬性  
  
-   變更資料行的順序  
  
-   變更資料行的資料類型  
  
**預設資料表檢視**  
選取在設計師中查看資料表的方式：  
  
-   **Standard**  
  
    顯示資料表標頭、所有資料行名稱、資料類型以及允許 Null 設定。  
  
-   **資料行名稱**  
  
    顯示資料行名稱。  
  
-   **索引鍵**  
  
    顯示資料表標頭與主索引鍵資料行。  
  
-   **僅顯示名稱**  
  
    只顯示具有其名稱的資料表標頭。  
  
-   **Custom**  
  
    允許您選擇要檢視的資料行。  
  
**在新圖表上啟動加入資料表對話方塊**  
在開啟設計師時自動開啟 [新增資料表] 對話方塊。  
  

