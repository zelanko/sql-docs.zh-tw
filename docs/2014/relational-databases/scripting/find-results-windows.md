---
title: 尋找結果視窗
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vs.findresults2
helpviewer_keywords:
- Find Results Windows dialog box
ms.assetid: 3b68dbb7-26d6-4bc9-bd2c-c27e5dc385c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88fb0cda002694d87cad94dd8032811f6451f1cd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245131"
---
# <a name="find-results-windows"></a>尋找結果視窗
  在 [**尋找和取代**] 對話方塊的 [檔案**中尋找**] 或 [檔案**中取代**] 索引標籤中，兩個 [尋找結果] 視窗顯示找到的相符專案。 
  **[檔案中尋找]** 和 **[檔案中取代]** 的 **[結果選項]** 命令允許您選擇 [尋找結果] 視窗，其中會列出所有找到的相符結果。  
  
 選取的 [尋找結果] 視窗只要找到相符結果就會自動開啟。 若要手動顯示 [尋找結果] 視窗，請在 **[檢視]** 功能表上按一下 **[其他視窗]** ，然後按一下 **[尋找結果 1]** 或 **[尋找結果 2]**。  
  
 若要顯示程式碼檔案並跳至出現相符結果的行位置，請按兩下結果清單中的任一行。 來源檔案顯示在程式碼編輯器中，且插入點置於符合文字開始處。 符號出現在編輯器的指標邊界，以標示包含相符項目的行，並於狀態列顯示全文。  
  
## <a name="toolbar-buttons"></a>工具列按鈕  
 下列工具列按鈕可用來協助您掃描整個結果清單，並跳至您程式碼中找到相符項目的行。  
  
 **頁面旗標 + 向上鍵**  
 移至找到選取之相符項目的行。  
  
 **頁面 + 向左箭號**  
 移至上一個相符項目的行。  
  
 **頁面 + 向右箭號**  
 移至下一個相符項目的行。  
  
 **全部清除**  
 移除 [結果]**** 清單中的所有相符項目。  
  
## <a name="shortcut-keys"></a>快速鍵  
 下列快速鍵可用來協助您快速導覽所有找到的相符項目。  
  
 CTRL+HOME  
 捲動到尋找結果視窗的頂端。  
  
 CTRL+END  
 捲動到尋找結果視窗的底部。  
  
 PAGE UP  
 向上捲動至下一個相符項目群組。  
  
 PAGE DOWN  
 向下捲動至下一個相符項目群組。  
  
 向上鍵  
 選取上一個相符項目。  
  
 DOWN ARROW  
 選取下一個相符項目。  
  
## <a name="search-result-entries"></a>搜尋結果項目  
 結果清單中每個項目都提供下列資訊：  
  
-   完整路徑  
  
-   檔案名稱  
  
-   行號  
  
-   行中包含相符項目的全文檢索  
  
> [!TIP]  
>  您可以使用 **[快速尋找]** 來掃描長度較長的結果清單。 開啟並停駐尋找結果視窗，然後按一下 **[尋找]** 索引標籤上的三角形 **[檢視]** 按鈕，並切換至 **[快速尋找]**。 將搜尋的 **[查詢]** 欄位設定為 **[使用中視窗]**，輸入 **[尋找目標]** 字串，然後按一下 **[找下一個]**。 這樣您就可以掃描在特定資料夾或檔案中找到之相符項目的結果清單，或者其他關鍵詞彙出現在程式碼行中的相符項目。  
  
## <a name="summary-lines"></a>摘要行  
 每個搜尋結果集的第一行皆為陳述搜尋參數，最後一行則為統計資料。 例如，以 **[檔案中尋找]** 搜尋所有開啟的文件，找出任何與規則運算式「`var[1-3]&par`」相符的字串，進而產生的結果清單，可能會以此搜尋參數行開始：  
  
 `Find all "var[1-3]&par" Regular Expression, All Open Documents`  
  
 而且可能會以此行的統計資料結束：  
  
 `Total found: 57  Matching files: 23  Total files searched: 59`  
  
 以 **[檔案中取代]** 搜尋所有開啟的文件，找出任何與規則運算式「`var[1-3]&par`」相符的字串，並以「`sample`」字串取代，進而產生的結果清單，可能會以此搜尋參數行開始：  
  
 `Replace "var[1-3]&par", "sample", Regular Expression, All Open Documents`  
  
 而且可能會以此行的統計資料結束：  
  
 `Total replaced: 57  Matching files: 23  Total files searched: 59`  
