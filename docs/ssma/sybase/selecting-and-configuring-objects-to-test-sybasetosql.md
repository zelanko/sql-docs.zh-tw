---
title: 選取並設定測試 (SybaseToSQL) 的物件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 09103b9294754a7634a1d28109f3129286acae94
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "40394000"
---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>選取並設定要測試的物件 (SybaseToSQL)
在此步驟中，您選取測試，並設定為比較程序的函式的輸出參數，以及函式的傳回值的物件。  
  
## <a name="selection-of-objects-to-test"></a>要測試之物件的選取範圍  
位於視窗左側的 Sybase 物件樹狀目錄，請檢查您想要在測試過程中叫用的物件。 請參閱中的可測試物件的完整清單[測試移轉的資料庫物件&#40;SybaseToSQL&#41; ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)主題。  
  
如果 SSMA Tester 不支援任何測試所選取的物件，您會看到標示為連結**有些選取的物件包含錯誤**物件樹狀結構下方。 按一下此連結來檢視這些物件無法測試為何的原因，並清除選取錯誤的物件。  
  
在右側，您可以檢視數頁**SQL**頁面會顯示目前的物件定義。 在**Pre SQL**並**Post SQL**頁面可以指定的引動過程的物件開始進行測試前後執行的指令碼。 這是可能很有用，當物件需要額外的物件，這類的暫存資料表或資料指標。 **參數**頁面列出的參數，如果物件為預存程序或函式。 **屬性**頁面會顯示物件的其他特性。 請參閱的說明**參數 Comparsions**並**呼叫值**下方頁面。  
  
## <a name="parameter-comparison-settings"></a>參數比較設定  
建立輸出參數的比較規則，並傳回值**參數比較**頁面。 您可以進行下列設定。  
  
### <a name="use-during-comparisons"></a>在比較期間的使用  
使用的測試結果相較之下選取的參數來啟用。  
  
-   如果您選擇 **，則為 True**，SSMA 會比較此參數的輸出值上執行的程序在 Sybase 上具有對應值之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   如果您選擇**False**，參數將會排除驗證結果。  
  
### <a name="use-custom-scale"></a>使用自訂的小數位數  
近似和固定長度數值資料型別參數，您可以設定自訂的小數位數，用於比較。  
  
-   如果您選擇 **，則為 True**，會捨入數字值，根據**比較擴展**值之前它們進行比較。  
  
-   如果您選擇**False**，數字的比較會精確。  
  
### <a name="comparing-scale"></a>比較小數位數  
適用於只有當**使用自訂縮放**選項設定為 **，則為 True**。 這是數值比較的有效位數。  
  
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
  
-   如果您選擇**False**，比較會區分大小寫。  
  
### <a name="ignore-trailing-spaces"></a>忽略尾端空白  
控制如何尾端的空格會被視為在比較時。  
  
-   如果您選擇 **，則為 True**，比較的字串會是右邊修剪比較之前。  
  
-   如果您選擇**False**，比較的字串將會保留尾端空白。  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>指定輸入的值的程序和函式 （呼叫的值）  
您可以指定輸入的參數值**呼叫值**頁面。 **新增呼叫**按鈕會將新的呼叫使用空白參數值。 **移除呼叫**按鈕會移除目前的呼叫。  
  
## <a name="next-step"></a>下一個步驟  
[選取並設定受影響的物件&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[測試移轉的資料庫物件&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
