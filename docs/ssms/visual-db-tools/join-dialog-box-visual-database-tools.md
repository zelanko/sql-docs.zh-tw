---
title: "聯結對話方塊 (Visual Database Tools) | Microsoft Docs"
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
- vdt.ppg.joinline
- vdtsql.chm:69638
ms.assetid: 0d9516bb-4ad3-4fcf-bb77-93474dea698f
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82c974b0a34c99af677eb783b12809e6d185072b
ms.lasthandoff: 04/11/2017

---
# <a name="join-dialog-box-visual-database-tools"></a>聯結對話方塊 (Visual Database Tools)
使用此對話方塊可指定聯結資料表的選項。 若要存取此對話方塊，請在 [設計]**** 窗格中選取聯結線 (Join Line)。 然後，在 [屬性]**** 視窗中按一下 [聯結條件及類型]****，並按一下顯示在屬性右邊的省略符號 (**…**)。  
  
依照預設，是使用根據包含聯結資料行中符合資訊資料列來建立結果集的內部聯結，將關聯資料表聯結在一起。 藉由設定 [聯結]**** 對話方塊中的選項，可以根據不同的運算子指定聯結，也可以指定外部聯結。  
  
如需聯結資料表的詳細資訊，請參閱[使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)。  
  
## <a name="options"></a>選項。  
  
|**詞彙**|**定義**|  
|------------|------------------|  
|**Table**|聯結中相關資料表或資料表值物件的名稱。 不能在這裡變更資料表的名稱 — 此資訊只用於顯示資訊。|  
|**資料行**|用於聯結資料表的資料行名稱。 運算子清單中的運算子會指定各資料行中資料之間的關係。 不能在這裡變更資料行的名稱 — 此資訊只用於顯示資訊。|  
|**運算子**|指定用於關聯聯結資料行的運算子。 若要指定等於 (=) 之外的運算子，請從清單中選取。 關閉屬性頁時，您選取的運算子會出現在聯結線的菱形圖中，如下所示：<br /><br />![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbii.gif "Visual Database Tools icon")|  
|**選取所有資料列，從 <table1>**|指定輸出中顯示左邊資料表裡全部的資料列，即使右邊資料表中沒有對應的符合也一樣。 右邊資料表中沒有符合資料的資料行會顯示為 null。 選擇此選項就等於在 SQL 陳述式中指定 LEFT OUTER JOIN。|  
|**選取所有資料列，從 <table2>**|指定輸出中顯示右邊資料表裡全部的資料列，即使左邊資料表中沒有對應的符合也一樣。 左邊資料表中沒有符合資料的資料行會顯示為 null。 選擇此選項就等於在 SQL 陳述式中指定 RIGHT OUTER JOIN。|  
  
同時選取 [選取所有資料列，從 <table1>]**** 和 [選取所有資料列，從 <table2>]****，與在 SQL 陳述式中指定 FULL OUTER JOIN 相同。  
  
選取某個選項建立外部聯結時，聯結線中的菱形圖就會改變，以指示聯結為左邊外部、右邊外部或完整外部聯結。  
  
> [!NOTE]  
> 「左邊」和「右邊」這兩個字不一定對應到 [圖表] 窗格中的資料表位置。 「左邊」指的是在 SQL 陳述式中名稱出現在關鍵字 JOIN 左邊的資料表，「右邊」指的是名稱出現在關鍵字 JOIN 右邊的資料表。 如果在 [圖表]**** 窗格中移動資料表，則不必變更資料表是左邊或右邊的考量。  
  
## <a name="see-also"></a>另請參閱  
[使用聯結查詢 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  

