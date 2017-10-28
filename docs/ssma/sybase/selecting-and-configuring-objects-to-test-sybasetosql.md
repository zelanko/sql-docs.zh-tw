---
title: "選取和設定物件以測試 (SybaseToSQL) |Microsoft 文件"
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
- Tester Component,Parameter Comparision Setting
- Tester Component,Selecting Objects
ms.assetid: 89c23aad-bfee-4917-bc16-175288390ac0
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e1cc9bf3ed4348e3875885c1c7bb6face6562753
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>選取和設定測試 (SybaseToSQL) 的物件
在這個步驟中選取測試，並設定設定值比較程序和函式的輸出參數，以及函式的傳回值的物件。  
  
## <a name="selection-of-objects-to-test"></a>要測試之物件的選取範圍  
位於視窗左側的 Sybase 物件樹狀目錄，請檢查您想要在測試過程中叫用的物件。 請參閱中的可測試物件的完整清單[測試移轉的資料庫物件 &#40;SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)主題。  
  
如果 SSMA Tester 不支援任何測試選取的物件，您會看到標示為連結**有些選取的物件包含錯誤**物件樹狀結構下方。 按一下此連結來檢視的理由為何無法測試這些物件，並清除選取錯誤的物件。  
  
在右側，您可以檢視數個頁面**SQL**頁面會顯示目前的物件定義。 在**前 SQL**和**Post SQL**頁面可以指定指令碼執行之前和之後叫用的物件開始進行測試。 這是可能是很有用的物件需要額外的物件，這類的暫存資料表或資料指標。 **參數**頁面列出的參數，如果物件是預存程序或函式。 **屬性**頁面會顯示物件的其他特性。 請參閱描述**參數 Comparsions**和**呼叫值**頁面下方。  
  
## <a name="parameter-comparison-settings"></a>參數比較設定  
建立輸出參數的比較規則，並傳回值中的**參數比較**頁面。 您可以進行下列設定。  
  
### <a name="use-during-comparisons"></a>使用在進行比較  
使用測試結果比較在所選取的參數來啟用。  
  
-   如果您選擇**True**，SSMA 會比較此參數的輸出值上執行 Sybase 具有對應值的程序之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   如果您選擇**False**，驗證結果將會排除參數。  
  
### <a name="use-custom-scale"></a>使用自訂縮放比例  
近似和固定長度數值資料型別參數，您可以設定自訂的縮放比例進行比較。  
  
-   如果您選擇**True**，數字的值會捨入根據**比較小數位數**值之前在進行比較。  
  
-   如果您選擇**False**，數值比較，都會是精確。  
  
### <a name="comparing-scale"></a>比較小數位數  
適用於只有當**使用自訂縮放**選項設定為**True**。 這是數值比較的有效位數。  
  
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
  
-   如果您選擇**False**，比較會區分大小寫。  
  
### <a name="ignore-trailing-spaces"></a>忽略尾端空白  
控制如何尾端的空格會被視為在比較時。  
  
-   如果您選擇**True**，比較的字串右邊修剪再將比較。  
  
-   如果您選擇**False**，比較的字串將會保留尾端空白。  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>指定輸入的值的程序和函式 （呼叫值）  
您可以指定輸入的參數值在**呼叫值**頁面。 **加入呼叫**按鈕會將新的呼叫，以空的參數值。 **移除呼叫**按鈕會移除目前的呼叫。  
  
## <a name="next-step"></a>下一個步驟  
[選取並設定受影響的物件 &#40;SybaseToSQL &#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[測試移轉的資料庫物件 &#40;SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

