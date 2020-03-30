---
title: 重新排列輸出資料行順序
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- reordering output columns [SQL Server]
- output columns [SQL Server]
ms.assetid: 76462885-de4a-4290-a26b-90696d3671f4
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 33739ef70de87ece117d57a9091dda83d60138fb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75255194"
---
# <a name="reorder-output-columns-visual-database-tools"></a>重新排列輸出資料行順序 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
資料行加入選取查詢中的順序，決定資料行出現在結果中的順序。 第一個加入的資料行會出現在結果的最左側，接著是第二個資料行，依此類推。  
  
如果您建立了更新或插入查詢，加入資料行的順序會影響資料處理的順序。  
  
若要控制資料行出現在結果集的位置，或是使用的順序，您可以重新排序資料行。  
  
### <a name="to-reorder-columns-for-output"></a>若要重新排序輸出的資料行  
  
1.  在 [準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，按一下資料列左側的資料列資料列選取器按鈕，選取包含資料行的資料列。  
  
2.  指向資料列選取器按鈕，將資料列拖曳到新的位置。  
  
    -或-  
  
    在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中編輯資料行名稱順序。  
  
> [!TIP]  
> 您可以在 [準則] 窗格中先插入空白資料列，然後指定想要插入的資料行，這樣就可以將資料列加入到 [準則] 窗格中的指定位置。 如需詳細資訊，請參閱[將資料行新增至查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
[排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[摘要查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[使用查詢執行基本作業 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
