---
title: 選取並設定受影響的物件 (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Columns Comparison Settings
- Selection of Affected Objects
ms.assetid: 545eeda2-9829-4187-a858-619a96b4b71d
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: d212f53d9cdd366ec6105ca6d44b345112d2f4fe
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="selecting-and-configuring-affected-objects-oracletosql"></a>選取並設定受影響的物件 (OracleToSQL)
在此頁面中，您可以選取資料表和外部索引鍵，在其中變更應該比較當 SSMA 確認上一個步驟中所選擇的物件執行的結果。 此外，您可以自訂的驗證參數。  
  
## <a name="selection-of-affected-objects"></a>選取受影響的物件  
在 Oracle 物件樹狀目錄，位於視窗的左半部，請檢查資料表和外部索引鍵，在其中變更應該比較的完全相同。  
  
如果 SSMA 軟體測試人員無法驗證任何這些物件，您會看到標示為連結**有些選取的物件包含錯誤**物件樹狀結構下方。 按一下此連結來檢視的理由為何無法比較這些物件，並清除選取錯誤的物件。  
  
## <a name="table"></a>Table  
[資料表] 索引標籤包含方格檢視選取的資料表。 方格包含選取之資料表的下列資訊：  
  
-   資料行名稱  
  
-   資料類型  
  
-   有效位數  
  
-   小數位數  
  
-   規則  
  
-   預設值  
  
-   識別  
  
-   可為 Null  
  
## <a name="sql"></a>Sql  
SQL 索引標籤包含 「 建立資料表 」 選取的資料表的 SQL。  
  
## <a name="data"></a>資料  
資料索引標籤會顯示選取的資料表中存在的資料。  
  
## <a name="properties"></a>屬性  
屬性索引標籤會顯示選取之資料表的屬性。 下列欄位會出現在 [屬性] 索引標籤：  
  
-   建立或上次修改  
  
-   Object Name  
  
## <a name="columns-comparison-settings"></a>資料行比較設定  
上所建立的資料表資料行的比較規則**資料行比較**頁面。 您可以進行下列設定。  
  
### <a name="use-during-test-comparisons"></a>在進行比較測試的使用  
決定此資料行的測試結果驗證將會參與。  
  
-   如果您選擇**True**，SSMA 會比較此資料行的內容在 Oracle 上執行測試，SQL Server 中的資料行的內容之後。 
  
-   如果您選擇**False**，驗證結果將會排除資料行。  
  
### <a name="use-custom-scale"></a>使用自訂縮放比例  
數值資料類型的資料行，您可以設定自訂的縮放比例進行比較。  
  
-   如果您選擇**True**，數字的值會捨入根據**比較小數位數**值之前在進行比較。  
  
-   如果您選擇**False**，數值比較，都會是精確。  
  
### <a name="comparing-scale"></a>比較小數位數  
  
-   適用於只有當**使用自訂縮放**選項設定為**True**。 這是數值比較的有效位數。  
  
### <a name="date-time-comparing"></a>日期時間比較  
定義如何日期/時間值進行比較。  
  
-   如果您選取**比較整個日期**，將會執行完整的值從兩個平台比較。  
  
-   如果您選取**只比較日期**、 部分將會略過的時間。  
  
-   如果您選取**只有比較時間**、 組件將會忽略的日期。  
  
-   如果您選取**忽略毫秒**，結果將會比較最多秒數。  
  
-   如果您選取**忽略日期和毫秒**，結果會是第二個比較僅由時間部分，並忽略小數部分。  
  
### <a name="ignore-strings-case"></a>忽略字串的大小寫  
控制比較區分大小寫。  
  
-   如果您選擇**True**，比較會區分大小寫。  
  
-   如果您選擇**False**，比較將負責字母大小寫。  
  
## <a name="comparing-sql"></a>比較 SQL  
您可以檢視 SELECT 陳述式上產生的 SSMA Tester**比較 SQL**頁面。 測試人員將會比較為基礎的資料列的資料列的這些陳述式的結果集。 Oracle 結果集的每個下一個資料列應該會等於在 SQL Server 產生的結果集的下一個資料列。
  
您可以編輯這些 SELECT 陳述式，以提供自訂驗證。 若要儲存變更，Oracle 和 SQL Server 陳述式中，使用**套用**跟著按鈕底下的來源和目標 SQL。  
  
## <a name="next-step"></a>下一個步驟  
[自訂呼叫順序&#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[完成測試案例準備&#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
[執行測試案例&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[測試移轉的資料庫物件&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
