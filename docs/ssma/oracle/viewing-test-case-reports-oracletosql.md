---
title: 檢視測試案例報表 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8da14323-9dd6-4019-bf79-3e8b972a9bc0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: ce59e126ce24e30e091b4a5456d8b78c84355e88
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47641766"
---
# <a name="viewing-test-case-reports-oracletosql"></a>檢視測試案例報表 (OracleToSQL)
測試案例報表會顯示測試驗證結果和一般測試的資訊。 如果測試失敗，也會顯示已驗證的物件中的任何不相符資料的相關資訊。  
  
## <a name="report-structure"></a>報表結構  
報表的頂端會顯示這些統計資料：  
  
-   已測試的物件和測試已順利完成的物件數目的總數。  
  
-   資料表和成功比對的外部索引鍵的數目和已驗證的資料表和外部索引鍵的總數。  
  
-   開始時間、 結束時間的測試案例和執行所花費的總時間。  
  
報表的其餘部分會顯示四個類別的資訊：  
  
**必要條件錯誤**  
顯示在發生任何錯誤**必要條件步驟。** 通常，它會略過。  
  
**初始化**  
顯示執行狀態**成功**或是**失敗**。  
  
**測試物件的結果**  
結果 （成功或失敗） 和 SSMA 軟體測試人員偵測到失敗時不相符的比較。  
  
**最終處理**  
顯示執行狀態**成功**或是**失敗**。  
  
## <a name="see-also"></a>另請參閱  
[執行測試案例&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[測試移轉的資料庫物件&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
