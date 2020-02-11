---
title: 查看測試案例報表（SybaseToSQL） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944602"
---
# <a name="viewing-test-case-reports-sybasetosql"></a>檢視測試案例報表 (SybaseToSQL)
測試案例報表會顯示測試驗證結果和一般測試資訊。 在測試失敗的情況下，也會顯示已驗證物件中任何不相符資料的相關資訊。  
  
## <a name="report-structure"></a>報表結構  
報表的頂端會顯示這些統計資料：  
  
-   已測試物件的總數，以及測試成功的物件數目。  
  
-   已驗證的資料表和外鍵的總數，以及成功符合的資料表和外鍵數目。  
  
-   測試案例的開始時間、結束時間，以及執行所花費的總時間。  
  
報表的其餘部分會顯示四個類別中的資訊：  
  
**必要條件錯誤**  
顯示**必要條件**步驟中發生的任何錯誤。 通常會略過。  
  
**初始**  
將執行狀態顯示為**成功**或**失敗**。  
  
**測試物件結果**  
比較結果（成功或失敗），以及 SSMA 測試器在失敗時所偵測到的不相符。  
  
**完成**  
將執行狀態顯示為**成功**或**失敗**。  
  
## <a name="see-also"></a>另請參閱  
[&#40;SybaseToSQL&#41;執行測試案例](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[&#40;SybaseToSQL&#41;測試遷移的資料庫物件](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
