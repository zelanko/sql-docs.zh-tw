---
title: 計算資料表中的資料列 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- totals [SQL Server], row counts
- row counts [SQL Server]
- column values [SQL Server]
- number of rows
- number of values
- counting rows
ms.assetid: dda4296a-1d16-4e77-8d6f-e295f6dd4e87
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 04b836a53b4b9928118221053d1fbc2c3a89dfdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63217817"
---
# <a name="count-rows-in-a-table-visual-database-tools"></a>計算資料表中的資料列 (Visual Database Tools)
  您可以計算資料表中的資料列，以判斷：  
  
-   在資料表中的資料列總數，例如，在 `titles` 資料表中所有書籍的計數。  
  
-   符合特定條件的資料表資料列數目，例如，在 `titles` 資料表中某簽發者的書籍數目。  
  
-   特定資料行中的值數目。  
  
 在計算資料行中的值時，null 不包含在計數中。 例如，您可能會計算 `titles` 資料表中 `advance` 資料行有值的書籍數目。 依照預設，計數包含所有的值，而不只是唯一的值。  
  
 所有三種類型計數的程序都相互類似。  
  
### <a name="to-count-all-the-rows-in-a-table"></a>若要計算資料表中的所有資料列  
  
1.  請確定您要摘要的資料表已經出現在 [圖表] 窗格中。  
  
2.  在 [圖表] 窗格的背景上按一下滑鼠右鍵，然後從快速鍵功能表中選擇 [新增群組依據]  。 [查詢和檢視表設計工具](visual-database-tools.md)會將 [群組依據]  資料行新增至 [準則] 窗格的方格中。  
  
3.  在代表資料表或資料表值物件的矩形中，選取** \* [（所有資料行）** ]。  
  
     查詢和檢視表設計工具會自動將 [計數]  一詞填入至 [準則] 窗格的 [群組依據]  資料行，並且將資料行別名指定至您所摘要的資料行。 您可以使用較有意義的別名取代這個自動產生的別名。 如需詳細資訊，請參閱[建立資料行別名 &#40;Visual Database Tools&#41;](create-column-aliases-visual-database-tools.md)。  
  
4.  執行查詢。  
  
### <a name="to-count-all-the-rows-that-meet-a-condition"></a>若要計算符合條件的所有資料列  
  
1.  請確定您要摘要的資料表已經出現在 [圖表] 窗格中。  
  
2.  在 [圖表] 窗格的背景上按一下滑鼠右鍵，然後從快速鍵功能表中選擇 [新增群組依據]  。 查詢和檢視表設計工具會將 [群組依據]  資料行新增至 [準則] 窗格的方格中。  
  
3.  在代表資料表或資料表結構化物件的矩形中，選取** \*[（所有資料行）** ]。  
  
     查詢和檢視表設計工具會自動將 [計數]  一詞填入至 [準則] 窗格的 [群組依據]  資料行，並且將資料行別名指定至您所摘要的資料行。 若要在查詢輸出中建立更有用的資料行標題，請參閱[建立資料行別名 &#40;Visual Database Tools&#41;](create-column-aliases-visual-database-tools.md)。  
  
4.  新增要搜尋的資料行，然後清除 [輸出]  資料行中的核取方塊。  
  
     查詢和檢視表設計工具會自動將 [群組依據]  一詞填入至方格的 [群組依據]  資料行中。  
  
5.  將 [群組依據]  資料行中的 [群組依據]  變更為 [Where]  。  
  
6.  在想要搜尋資料行的 [過濾]  資料行中，輸入搜尋條件。  
  
7.  執行查詢。  
  
### <a name="to-count-the-values-in-a-column"></a>若要計算資料行中的值  
  
1.  請確定您要摘要的資料表已經出現在 [圖表] 窗格中。  
  
2.  在 [圖表] 窗格的背景上按一下滑鼠右鍵，然後從快速鍵功能表中選擇 [新增群組依據]  。 查詢和檢視表設計工具會將 [群組依據]  資料行新增至 [準則] 窗格的方格中。  
  
3.  將您要計算的資料行加入至 [準則] 窗格。  
  
     查詢和檢視表設計工具會自動將 [群組依據]  一詞填入至方格的 [群組依據]  資料行中。  
  
4.  將 [群組依據]  資料行中的 [群組依據]  變更為 [計數]  。  
  
    > [!NOTE]  
    >  若只要計算唯一的值，則選擇 [Count Distinct]  。  
  
5.  執行查詢。  
  
## <a name="see-also"></a>另請參閱  
 [排序和分組查詢結果 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [摘要查詢結果 &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)  
  
  
