---
title: 將資料表從一個資料庫關係圖複製到另一個（Visual Database Tools） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- copying tables
- duplicating tables
ms.assetid: 155a4f09-9321-4887-a7d4-aa2ce6b51277
author: stevestein
ms.author: sstein
ms.openlocfilehash: ea42bb5047daa0a291e9ab34bbec1e28f35f642e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058190"
---
# <a name="copy-tables-from-one-database-diagrams-to-another-visual-database-tools"></a>將資料表從一個資料庫圖表複製至另一個資料庫圖表 (Visual Database Tools)
  您可以在相同資料庫中，將資料表從一個資料庫圖表複製至另一個資料庫圖表中。  
  
 將資料表從一個資料庫圖表複製到另一個資料庫圖表，會在第二個圖表中加入該資料表的參考。 並未在資料庫中複製資料表。 例如，若要從一個資料庫圖表複製 `authors` 資料表至另一個資料庫圖表，則每個圖表都參考資料庫中相同的 `authors` 資料表。  
  
### <a name="to-copy-a-table-from-another-database-diagram"></a>若要從另一個資料庫圖表複製資料表  
  
1.  確定您已經連接想要複製其資料表的資料庫。  
  
2.  開啟來源和目標資料庫圖表，然後在來源圖表中選取要複製至目標圖表的資料表。  
  
3.  按一下工具列上的 [複製]  按鈕。 這一動作會將選取的資料表定義放在剪貼簿中。  
  
4.  切換至目標圖表。 這一圖表必須與來源圖表在同一資料庫中。  
  
5.  按一下工具列上的 [貼上]  按鈕。 剪貼簿的內容會出現在新位置，而且仍保持反白顯示，直到您按一下別處。 如果選取的資料表與目標圖表中的其他資料表之間有關聯性，則會自動繪出關聯線。  
  
 在任一圖表中編輯資料表時，您所做的變更會同時反應在兩個圖表中。 同理，在任一圖表中儲存資料表，則任一圖表中的資料表都不會再被視為「已修改」。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料庫關係圖 &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [將資料表新增至圖表 &#40;Visual Database Tools&#41;](add-tables-to-diagrams-visual-database-tools.md)  
  
  
