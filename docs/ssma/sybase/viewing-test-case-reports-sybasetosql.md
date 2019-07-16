---
title: 檢視測試案例報表 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8a6d45f7e621f9b6516d4cc1211a8627174ae9b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944602"
---
# <a name="viewing-test-case-reports-sybasetosql"></a>檢視測試案例報表 (SybaseToSQL)
測試案例報表會顯示測試驗證結果和一般測試的資訊。 如果測試失敗，也會顯示已驗證的物件中的任何不相符資料的相關資訊。  
  
## <a name="report-structure"></a>報表結構  
報表的頂端會顯示這些統計資料：  
  
-   已測試的物件和測試已順利完成的物件數目的總數。  
  
-   資料表和成功比對的外部索引鍵的數目和已驗證的資料表和外部索引鍵的總數。  
  
-   開始時間、 結束時間的測試案例和執行所花費的總時間。  
  
報表的其餘部分會顯示四個類別的資訊：  
  
**必要條件錯誤**  
顯示在發生任何錯誤**必要條件**步驟。 通常，它會略過。  
  
**初始化**  
顯示執行狀態**成功**或是**失敗**。  
  
**測試物件的結果**  
結果 （成功或失敗） 和 SSMA 軟體測試人員偵測到失敗時不相符的比較。  
  
**最終處理**  
顯示執行狀態**成功**或是**失敗**。  
  
## <a name="see-also"></a>另請參閱  
[執行測試案例&#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[測試移轉的資料庫物件&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
