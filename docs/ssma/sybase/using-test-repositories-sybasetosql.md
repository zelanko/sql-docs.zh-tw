---
title: "使用測試儲存機制 (SybaseToSQL) |Microsoft 文件"
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
- Tester Component,Test Repositories
ms.assetid: c359c25c-db2a-4a20-afa9-62d87a62df72
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a8c790666f48f142e65a0293bef2170dc12eb5f7
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="using-test-repositories-sybasetosql"></a>使用測試儲存機制 (SybaseToSQL)
SSMA 測試儲存機制存放區 SSMA Tester 測試案例和測試結果以供稍後使用。 儲存機制資料會儲存在 SQL Server 資料表**TestCaseRepository**和**RunTestCaseResultRepository**結構描述中**ssma_sybase_utilities**的**ssmatesterdb_syb**資料庫。  
  
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
  
-   按一下**執行** 按鈕以開啟[執行測試案例 &#40;SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)對話方塊，並執行選取的測試。  
  
## <a name="test-results-repository"></a>測試結果儲存機制  
您可以檢視測試結果儲存機制上**測試結果**頁面**儲存機制的測試案例**視窗。 按一下以開啟**測試結果...** 從**Tester**功能表。  
  
您可以使用兩個篩選條件上**測試結果**頁面：  
  
-   測試案例名稱篩選： 可選擇測試結果的測試案例的名稱。 此篩選器**所有測試案例**值即可顯示所有測試案例的測試結果。  
  
-   測試案例執行日期篩選： 篩選測試結果儲存日期。此篩選器**所有期間**值，可讓任何日期的儲存顯示測試結果。  
  
測試結果的下列資訊會顯示在方格中。  
  
-   名稱： 測試案例的名稱。  
  
-   開始： 測試案例的執行日期。  
  
-   結果: （這個儲存格的工具提示會顯示完整的測試執行摘要） 的測試執行簡短摘要。  
  
下列按鈕，可在測試結果 頁面上：  
  
-   按一下**檢視** 按鈕以開啟[檢視測試案例報表 &#40;SybaseToSQL &#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)的目前的測試案例結果。  
  
-   按一下**刪除**按鈕，即可刪除選取的測試結果  
  
## <a name="see-also"></a>另請參閱  
[執行測試案例 &#40;SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[測試移轉的資料庫物件 &#40;SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

