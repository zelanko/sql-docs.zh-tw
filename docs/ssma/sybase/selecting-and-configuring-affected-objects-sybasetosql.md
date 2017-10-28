---
title: "選取並設定受影響的物件 (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e5f4fcb5af81da2b78520542e2b57bd66bc4fd1
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>選取並設定受影響的物件 (SybaseToSQL)
在此頁面中，您可以選取資料表和外部索引鍵，在其中變更應該比較當 SSMA 確認上一個步驟中所選擇的物件執行的結果。 此外，您可以自訂的驗證參數。  
  
## <a name="selection-of-affected-objects"></a>選取受影響的物件  
位於視窗左側的 Sybase 物件樹狀目錄，請檢查資料表和外部索引鍵，在其中變更應該比較的完全相同。  
  
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
  
## <a name="table-comparison-settings"></a>資料表比較設定  
在建立資料表的比較規則**資料表比較**頁面。 您可以進行下列設定。  
  
### <a name="comparison-mode"></a>比較模式  
定義資料表內容上，將會執行比較。  
  
-   如果您選取**只變更**，將會執行完整資料表的資料列的比較。  
  
-   如果您選取**完整**，將執行已變更的資料列的比較。  
  
## <a name="column-comparison-settings"></a>資料行比較設定  
上所建立的資料表資料行的比較規則**資料行比較**頁面。 您可以進行下列設定。  
  
### <a name="use-during-test-comparisons"></a>在進行比較測試的使用  
決定此資料行的測試結果驗證將會參與。  
  
-   如果您選擇**True**，SSMA 會比較此資料行的內容之後 Sybase 上執行測試，以 SQL Server 中的資料行的內容。
  
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
您可以檢視 SELECT 陳述式上產生的 SSMA Tester**比較 SQL**頁面。 測試人員將會比較為基礎的資料列的資料列的這些陳述式的結果集。 Sybase 結果集的每個下一個資料列應該會等於下一個資料列，結果集所產生的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
您可以編輯這些 SELECT 陳述式，以提供自訂驗證。 若要儲存變更，在 Sybase 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]陳述式，使用**套用**跟著按鈕底下的來源和目標 SQL。  
  
## <a name="next-step"></a>下一個步驟  
[自訂呼叫順序 &#40;SybaseToSQL &#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[執行測試案例 &#40;SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[測試移轉的資料庫物件 &#40;SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

