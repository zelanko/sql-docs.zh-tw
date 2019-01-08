---
title: 選取並設定受影響的物件 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 48d5305854d214e61036e00ca23a94b85313138a
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52402255"
---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>選取並設定受影響的物件 (SybaseToSQL)
在此頁面中，您可以選取資料表和 SSMA 確認在上一個步驟中選擇之物件的執行結果時，所要比較的外部索引鍵，在其中變更。 此外，您可以自訂的驗證參數。  
  
## <a name="selection-of-affected-objects"></a>選取受影響的物件  
Sybase 物件樹狀結構，位於左邊視窗中檢查的資料表和外部索引鍵，在其中變更應該要比對完全相同。  
  
如果 SSMA 軟體測試人員無法驗證任何這些物件，您會看到標示為連結**有些選取的物件包含錯誤**物件樹狀結構下方。 按一下此連結來檢視為什麼無法比較這些物件的原因，並清除選取錯誤的物件。  
  
## <a name="table"></a>資料表  
[資料表] 索引標籤包含方格檢視選取的資料表。 方格包含選取之資料表的下列資訊：  
  
-   資料行名稱  
  
-   資料類型  
  
-   有效位數  
  
-   小數位數  
  
-   規則  
  
-   預設  
  
-   身分識別  
  
-   可為 Null  
  
## <a name="sql"></a>Sql  
SQL 索引標籤包含 「 建立資料表 」 中所選取資料表的 SQL。  
  
## <a name="data"></a>資料  
資料索引標籤會顯示選取之資料表中的資料。  
  
## <a name="properties"></a>屬性  
屬性索引標籤會顯示所選資料表的屬性。 下列欄位會出現在 [屬性] 索引標籤：  
  
-   建立或上次修改  
  
-   Object Name  
  
## <a name="table-comparison-settings"></a>資料表比較設定  
在 建立資料表的比較規則**資料表比較**頁面。 您可以進行下列設定。  
  
### <a name="comparison-mode"></a>比較模式  
在定義資料表內容，將會執行比較。  
  
-   如果您選取**只變更**，將會執行完整資料表的資料列的比較。  
  
-   如果您選取**完整**，將會執行已變更的資料列的比較。  
  
## <a name="column-comparison-settings"></a>資料行比較設定  
在 建立資料表的資料行的比較規則**資料行比較**頁面。 您可以進行下列設定。  
  
### <a name="use-during-test-comparisons"></a>測試比較期間使用  
決定這個資料行的測試結果驗證將會參與。  
  
-   如果您選擇 **，則為 True**，SSMA 會比較此資料行的內容在 Sybase 上執行測試，SQL Server 中的資料行的內容之後。
  
-   如果您選擇**False**，驗證結果將會排除資料行。  
  
### <a name="use-custom-scale"></a>使用自訂的小數位數  
數值資料類型的資料行，您可以設定自訂的縮放比例進行比較。  
  
-   如果您選擇 **，則為 True**，會捨入數字值，根據**比較擴展**值之前它們進行比較。  
  
-   如果您選擇**False**，數字的比較會精確。  
  
### <a name="comparing-scale"></a>比較小數位數  
  
-   適用於只有當**使用自訂縮放**選項設定為 **，則為 True**。 這是數值比較的有效位數。  
  
### <a name="date-time-comparing"></a>日期時間比較  
定義如何日期/時間值進行比較。  
  
-   如果您選取**比較整個日期**，將會執行完整的兩個平台的值比較。  
  
-   如果您選取**只比較日期**、 組件將被略過的時間。  
  
-   如果您選取**只比較時間**、 組件將會忽略日期。  
  
-   如果您選取**忽略毫秒**，結果會比較最多秒數。  
  
-   如果您選取**忽略的日期和毫秒**，結果會是比較，只有時間部分並略過的秒的小數部分。  
  
### <a name="ignore-strings-case"></a>忽略字串大小寫  
控制比較區分大小寫。  
  
-   如果您選擇 **，則為 True**，比較會區分大小寫。  
  
-   如果您選擇**False**，比較會負責處理字母大小寫。  
  
## <a name="comparing-sql"></a>比較 SQL  
您可以檢視 SELECT 陳述式上產生的 SSMA Tester**比較 SQL**頁面。 測試人員將會比較這些陳述式逐列為基礎的結果集。 Sybase 結果集的每個下一個資料列應該等於下一個資料列，結果集所產生的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
您可以編輯這些 SELECT 陳述式，以提供自訂的驗證。 若要儲存的變更在 Sybase[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]陳述式，使用**套用**對應來源與目標 SQL，下方按鈕。  
  
## <a name="next-step"></a>下一個步驟  
[自訂呼叫順序&#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[執行測試案例&#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[測試移轉的資料庫物件&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
