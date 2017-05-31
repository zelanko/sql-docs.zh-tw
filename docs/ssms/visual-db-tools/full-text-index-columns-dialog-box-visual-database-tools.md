---
title: "全文檢索索引資料行對話方塊 (Visual Database Tools) | Microsoft Docs"
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
- vdt.dlgbox.fulltextcolumn
ms.assetid: a6f41c5c-d950-4d64-9e42-d062925917b6
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b88b6ec8c86c16709b9fd22f1ef93f0c32b4f10c
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="full-text-index-columns-dialog-box-visual-database-tools"></a>全文檢索索引資料行對話方塊 (Visual Database Tools)
這個對話方塊會列出 [資料表設計工具] 開啟的資料表中，參與全文檢索索引的資料行。 若要存取這個對話方塊，請在資料表設計工具中的資料表上按一下滑鼠右鍵、選擇 [全文檢索索引]，然後在 [全文檢索索引] 對話方塊中，依序按一下想要檢視或編輯之資料行索引、右邊方格的 [資料行] 欄位，再按一下省略符號 (**…**)。  
  
## <a name="options"></a>選項。  
**資料行**  
顯示參與全文檢索索引之資料行的名稱。 若要加入資料行，請按一下第一個空的資料格，然後從下拉式清單中選擇資料行。 只可以存取資料類型為文字基礎或影像的資料行。  
  
**資料類型**  
顯示每一資料行的資料類型。 這是一個唯讀屬性。 若要變更資料類型，請在資料表設計工具中開啟資料表、按一下資料行，然後編輯 [資料行屬性] 索引標籤中的資料類型。  
  
**依資料行排列類型**  
只適用於資料類型為 **image**的資料行。 提供下拉式清單，您可在此選取代表本資料行之資料類型的其他資料行。 如果此資料行的資料類型不是 **image** ，值將會是 [無]。  
  
資料類型為 **image** 的資料行可包含 Microsoft Office 檔案 (.doc、.xls 與 .ppt 檔案)、文字檔 (.txt 檔) 與 HTML 檔案 (.htm 檔)，將該資料行之資料類型設定為影像，可使全文檢索搜尋進行檔案內容的搜尋。  
  
**語言**  
列出可用的語言。 從下拉式清單選擇適合您資料行資料的語言。 例如，如果您使用英文作業系統，但您要索引含有德文文字的資料行，則請從下拉式清單中選擇 [德文]，以提升索引的效能。  
  
**統計語意**  
選取是否要針對選取的資料行啟用語意索引。 如需詳細資訊，請參閱 [語意搜尋預留位置](http://msdn.microsoft.com/en-us/cd8faa9d-07db-420d-93f4-a2ea7c974b97)。  
  
如果您在選取 **[統計語意]** 之前選取 **[語言]**，而且選取的語言沒有相關聯的語意語言模型，則會停用 **[統計語意]** 核取方塊。 如果您在選取 [語言] 之前選取 [統計語意]，則下拉式方塊中提供的語言將受限為有語意語言模型支援的語言。  
  
## <a name="see-also"></a>另請參閱  
[全文檢索索引對話方塊 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/full-text-index-dialog-box-visual-database-tools.md)  
  

