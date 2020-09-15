---
description: 查詢定義差異對話方塊 (Visual Database Tools)
title: 查詢定義差異對話方塊
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69639
- vdtsql.chm:69640
- vdt.dlgbox.querydefinitionsdiffer
ms.assetid: 90383473-2922-40e5-9682-3850849aa856
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: a2517d930333f9a17e7746db29074456281ecf9d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88313854"
---
# <a name="query-definitions-differ-dialog-box-visual-database-tools"></a>查詢定義差異對話方塊 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
這個對話方塊會通知您，無法在 [圖表] 和 [準則] 窗格中以圖形顯示查詢，而且您只能在 [SQL] 窗格中編輯查詢。  
  
當您在 [SQL] 窗格中輸入或編輯 SQL 陳述式，然後移至另一個窗格、驗證查詢或嘗試執行查詢時，如果發生下列情況，此對話方塊便會出現：  
  
-   SQL 陳述式不完整或是包含一或多個語法錯誤。  
  
-   SQL 陳述式有效，但是圖形窗格並不支援 (例如，聯合查詢)。  
  
-   SQL 陳述式有效，但包含所使用資料連接的特定語法。  
  
> [!TIP]  
> 您可以使用 [查詢]**** 工具列中的 [驗證 SQL 陳述式]**** 按鈕，檢查陳述式是否有效。  
  
此對話方塊會顯示訊息，說明 SQL 陳述式無法顯示的原因，並詢問該如何繼續進行。  
  
> [!NOTE]  
> 如果您已經隱藏 [圖表] 和 [準則] 窗格，[查詢定義差異]**** 對話方塊就不會出現。  
  
## <a name="options"></a>選項  
**忽略按鈕**  
選擇此按鈕可指定要接受 SQL 陳述式，以繼續編輯或直接執行。 如果接受陳述式，[圖表] 和 [準則] 窗格將呈現暗灰色的 (Dimmed) 狀態，表示它們不會顯示 [SQL] 窗格中的陳述式。  
  
**復原按鈕**  
選擇此按鈕可捨棄對 [SQL] 窗格所做的變更。  
  
> [!NOTE]  
> 如果陳述式正確無誤，但是 [查詢和檢視設計師] 無法提供圖形方面的支援，這個陳述式還是可以執行，只是無法顯示在 [圖表] 和 [準則] 窗格中。 例如，如果您輸入聯合查詢 (Union Query)，陳述式可以執行，但不會顯示在其他窗格中。  
  
## <a name="see-also"></a>另請參閱  
[查詢和檢視表設計工具 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  
