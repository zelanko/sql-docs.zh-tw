---
title: 使用測試儲存機制 (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: b17f0cf6eabbf1268b849e63c24233aefabc089c
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34778474"
---
# <a name="using-test-repositories-oracletosql"></a>使用測試儲存機制 (OracleToSQL)
SSMA 測試儲存機制存放區 SSMA Tester 測試案例和測試結果以供稍後使用。 儲存機制資料會儲存在 SQL Server 資料表**TestCaseRepository**和**RunTestCaseResultRepository**結構描述中**ssma_oracle_utilities**的**ssmatesterdb**資料庫。  
  
下列按鈕上可用的儲存機制的測試案例 對話方塊：  
  
-   按一下**重新整理**按鈕以重新整理測試案例或測試結果的清單。  
  
-   按一下**關閉**按鈕以關閉儲存機制的測試案例 對話方塊。  
  
## <a name="test-cases-repository"></a>測試案例的儲存機制  
您可以按一下來檢視測試案例的儲存機制**測試案例...** 從**Tester**功能表。 然後顯示 SSMA**儲存機制的測試案例**對話方塊視窗中的已儲存測試案例清單**測試案例**頁面。  
  
此方格會顯示每個測試案例的下列資訊：  
  
-   名稱： 測試案例名稱。  
  
-   建立： 測試案例建立日期。  
  
-   已修改： 測試案例上次修改日期。  
  
-   描述： 測試案例描述。  
  
下列按鈕，可在測試案例 頁面上：  
  
-   按一下**新增**執行測試案例精靈並建立新的測試 按鈕。  
  
-   按一下**移除**從儲存機制中刪除選取的測試 按鈕。刪除測試案例時，也會一併刪除所有相關的測試結果。  
  
-   按一下**編輯**執行測試案例精靈和變更所選的測試 按鈕。  
  
-   按一下**執行** 按鈕以開啟[執行測試案例 (OracleToSQL)](http://msdn.microsoft.com/en-us/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02)對話方塊，並執行選取的測試。  
  
## <a name="test-results-repository"></a>測試結果儲存機制  
您可以檢視測試結果儲存機制上**測試結果**頁面**儲存機制的測試案例**視窗。 按一下以開啟**測試結果...** 從**Tester**功能表。  
  
您可以使用兩個篩選條件上**測試結果**頁面：  
  
-   測試案例名稱篩選： 可選擇測試結果的測試案例的名稱。 此篩選器**所有測試案例**值即可顯示所有測試案例的測試結果。  
  
-   測試案例執行日期篩選： 篩選測試結果儲存日期。此篩選器**所有期間**值，可讓任何日期的儲存顯示測試結果。  
  
測試結果的下列資訊會顯示在方格中。  
  
-   名稱： 測試案例的名稱。  
  
-   儲存： 測試案例的儲存日期。  
  
-   結果: （這個儲存格的工具提示會顯示完整的測試執行摘要） 的測試執行簡短摘要。  
  
下列按鈕，可在測試結果 頁面上：  
  
-   按一下**檢視** 按鈕以開啟[檢視測試案例報表&#40;OracleToSQL&#41; ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)的目前的測試案例結果。  
  
-   按一下**刪除**按鈕，即可刪除選取的測試結果  
  
## <a name="see-also"></a>另請參閱  
[執行測試案例&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[測試移轉的資料庫物件&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
