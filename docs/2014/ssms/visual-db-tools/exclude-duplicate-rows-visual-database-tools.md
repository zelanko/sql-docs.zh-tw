---
title: 排除重複的資料列 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 017385370989983d37f045379de926d0ebbf333f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146872"
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>排除重複的資料列 (Visual Database Tools)
  如果您只想在結果集中查看唯一的值，您可以指定您要從結果集排除重複的項目。  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>若要從結果集排除重複資料列  
  
1.  在 [圖表] 窗格的背景上按一下滑鼠右鍵，然後從快速鍵功能表中選擇 [屬性]。  
  
2.  在 [屬性] 視窗中，按一下 [重複資料僅顯示一筆]，並且將值設定為 [是]。  
  
     [查詢和檢視設計師] 會將關鍵字 DISTINCT 插入至 SQL 陳述式中顯示資料行清單的前面。  
  
    > [!NOTE]  
    >  如果使用 DISTINCT 關鍵字，您可能無法在 [結果] 窗格中修改結果集。  
  
## <a name="see-also"></a>另請參閱  
 [指定搜尋準則&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [排序及分組查詢結果 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  