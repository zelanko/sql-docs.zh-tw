---
title: 使用測試存放庫 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Repositories
ms.assetid: c359c25c-db2a-4a20-afa9-62d87a62df72
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a94bd053dac04c4d595e4f2077c02d1d79858e56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020842"
---
# <a name="using-test-repositories-sybasetosql"></a>使用測試存放庫 (SybaseToSQL)
SSMA 測試儲存機制存放區 SSMA Tester 測試案例和測試結果以供稍後使用。 儲存機制資料會儲存在 SQL Server 資料表**TestCaseRepository**並**RunTestCaseResultRepository**結構描述中**ssma_sybase_utilities** 的**ssmatesterdb_syb**資料庫。  
  
在存放庫的測試案例 對話方塊中可顯示下列按鈕：  
  
-   按一下 **重新整理**按鈕以重新整理測試案例或測試結果的清單。  
  
-   按一下 **關閉** 按鈕，關閉存放庫的測試案例 對話方塊。  
  
## <a name="test-cases-repository"></a>測試案例儲存機制  
您可以檢視測試案例儲存機制，依序按一下**測試案例...** 從**Tester**功能表。 接著會顯示 SSMA**存放庫的測試案例**對話方塊視窗中已儲存的測試案例，在上一份**測試案例**頁面。  
  
此方格會顯示每個測試案例的下列資訊：  
  
-   名稱：測試案例的名稱。  
  
-   建立：測試案例建立日期。  
  
-   修改：測試案例上次修改日期。  
  
-   描述：測試案例描述中。  
  
下列的按鈕可在測試案例 頁面上：  
  
-   按一下 **新增**按鈕以執行測試案例精靈並建立新的測試。  
  
-   按一下 [**移除**從儲存機制中刪除選取的測試] 按鈕。刪除測試案例時，也會一併刪除所有相關的測試結果。  
  
-   按一下 **編輯**按鈕，以執行測試案例精靈並變更選取的測試。  
  
-   按一下 [**執行**] 按鈕以開啟[執行測試案例&#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md)對話方塊，然後執行選取的測試。  
  
## <a name="test-results-repository"></a>測試結果儲存機制  
您可以檢視測試結果儲存機制**測試結果**頁**存放庫的測試案例**視窗。 按一下以開啟**測試結果...** 從**Tester**功能表。  
  
您可以使用兩個篩選條件**測試結果**頁面：  
  
-   測試案例名稱篩選：可選擇測試結果的測試案例的名稱。 此篩選條件**所有的測試案例**值可允許顯示所有測試案例的測試結果。  
  
-   測試案例執行日期篩選條件：篩選測試結果所儲存的日期。此篩選條件**所有期間**值可讓任何日期的節約顯示測試結果。  
  
下列測試結果的相關資訊會顯示在方格中。  
  
-   名稱：測試案例的名稱。  
  
-   開始：測試案例執行日期。  
  
-   結果：（這個儲存格的工具提示會顯示測試執行的完整摘要） 的測試執行的簡短摘要。  
  
下列的按鈕可在測試結果 頁面上：  
  
-   按一下 [**檢視**] 按鈕以開啟[檢視測試案例報表&#40;SybaseToSQL&#41; ](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)目前的測試案例結果。  
  
-   按一下 [**刪除**] 按鈕來刪除選取的測試結果  
  
## <a name="see-also"></a>另請參閱  
[執行測試案例&#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[測試移轉的資料庫物件&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
