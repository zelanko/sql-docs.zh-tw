---
title: "將資料表加入圖表 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inserting tables
- adding tables
ms.assetid: 5440fdf7-ac04-4325-9f32-181f4cd402e5
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ae6c38826ce111508e88de0948ffe8e1ecb35c24
ms.lasthandoff: 04/11/2017

---
# <a name="add-tables-to-diagrams-visual-database-tools"></a>將資料表加入圖表 (Visual Database Tools)
您可以加入資料表至資料庫圖表中，以編輯其結構或使它關聯圖表中的其他資料表。 也可以加入現有的資料庫資料表至圖表中，或插入尚未在資料庫中定義的新資料表。  
  
### <a name="to-insert-a-new-table-into-a-diagram"></a>若要將新資料表插入圖表中  
  
1.  確定您已經連接想要建立資料表的資料庫。  
  
    若要在目前的圖表中建立資料表，請按一下工具列上的 [新增資料表] 按鈕。  
  
    -或-  
  
    在圖表上按一下滑鼠右鍵，然後選取 [新增資料表]。  
  
2.  在 [選擇名稱] 對話方塊中，修改或接受系統指派的資料表名稱，然後選擇 [確定]。  
  
    新資料表會以標準檢視顯示於圖表中。  
  
3.  在新資料表的第一個資料格中，輸入資料行名稱。 然後按下 TAB 鍵以移至下一個資料格。  
  
4.  在 [資料類型] 下，選取資料行的資料類型。 每個資料行都必須有名稱和資料類型。  
  
    您可以在 [資料表設計工具] 中設定資料行的其他屬性。  
  
5.  對想要加入資料表的每個資料行重複步驟 3 和 4。  
  
> [!NOTE]  
> 在儲存資料庫圖表時，新資料表就會加入資料庫中。  
  
### <a name="to-add-an-existing-table-to-a-diagram"></a>若要將現有的資料表加入圖表中  
  
1.  確定您已經連接到想要編輯資料表的資料庫。  
  
2.  在 [資料表] 資料夾中選取資料表。  
  
3.  將資料表拖曳至資料庫圖表中。  
  
4.  放開滑鼠按鈕。  
  
> [!NOTE]  
> 如果選定的資料表與圖表中其他資料表之間有關聯性，則會自動繪出其關聯線。  
  
### <a name="to-add-related-tables-to-a-diagram"></a>若要將關聯資料表加入圖表  
  
1.  在資料庫圖表中選取一個或多個具有外部索引鍵條件約束的資料表。  
  
2.  在選取的資料表上按一下滑鼠右鍵，然後選擇 [加入關聯資料表]。  
  
> [!NOTE]  
> 選定的資料表的外部索引鍵條件約束所參考的資料表，以及參考具有外部索引鍵條件約束的選定資料表的資料表，都會加入圖表中。  
  
## <a name="see-also"></a>另請參閱  
[使用資料庫圖表 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[使用資料庫圖表中的資料表 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
  

