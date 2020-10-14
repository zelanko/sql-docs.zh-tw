---
description: 使用測試存放庫 (OracleToSQL)
title: 使用測試存放庫 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6b070a45c7990efbb598401b241083fcb2d804f5
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035137"
---
# <a name="using-test-repositories-oracletosql"></a>使用測試存放庫 (OracleToSQL)
SSMA 測試存放庫會儲存 SSMA 測試人員測試案例和測試結果，以供稍後使用。 存放庫資料會儲存在**ssmatesterdb**資料庫的架構**ssma_oracle_utilities**的 SQL Server 資料表**TestCaseRepository**和**RunTestCaseResultRepository**中。  
  
下列按鈕可在 [測試案例] 對話方塊的 [存放庫] 中取得：  
  
-   按一下 [重新整理 **] 按鈕，** 以重新整理測試案例或測試結果清單。  
  
-   按一下 [ **關閉** ] 按鈕，關閉 [測試案例] 對話方塊的儲存機制。  
  
## <a name="test-cases-repository"></a>測試案例儲存機制  
您可以從 [測試**人員**] 功能表按一下 [**測試案例 ...** ] 來查看測試案例存放庫。 SSMA 接著會顯示 **測試案例** 對話方塊視窗的儲存機制，並在 [ **測試案例** ] 頁面上顯示已儲存的測試案例清單。  
  
方格會顯示有關每個測試案例的下列資訊：  
  
-   名稱：測試案例名稱。  
  
-   已建立：測試案例建立日期。  
  
-   已修改：測試案例上次修改日期。  
  
-   描述：測試案例描述。  
  
下列按鈕可在 [測試案例] 頁面上取得：  
  
-   按一下 [ **加入** ] 按鈕以執行測試案例嚮導，並建立新的測試。  
  
-   按一下 [ **移除** ] 按鈕，即可從存放庫中刪除選取的測試。刪除測試案例時，也會一併刪除所有相關的測試結果。  
  
-   按一下 [ **編輯** ] 按鈕，執行測試案例嚮導並變更選取的測試。  
  
-   按一下 [ **執行** ] 按鈕，開啟 [執行中的 [測試案例 (OracleToSQL) ](./running-test-cases-oracletosql.md) ] 對話方塊，並執行選取的測試。  
  
## <a name="test-results-repository"></a>測試結果存放庫  
您可以在 [**測試案例**] 視窗之儲存機制的 [**測試結果**] 頁面上，查看測試結果存放庫。 按一下 [**測試人員**] 功能表中的 [**測試結果**] 來開啟它。  
  
您可以使用 **測試結果** 頁面上的兩個篩選準則：  
  
-   測試案例名稱篩選：允許依測試案例名稱選擇測試結果。 此篩選準則的 **所有測試案例** 值允許顯示所有測試案例的測試結果。  
  
-   測試案例執行日期篩選：依儲存日期篩選測試結果。此篩選準則的 **所有期間** 值允許顯示任何儲存日期的測試結果。  
  
下列有關測試結果的資訊會顯示在方格中。  
  
-   名稱：測試案例名稱。  
  
-   已儲存：測試案例的儲存日期。  
  
-   結果：測試執行的簡短摘要 (此儲存格的工具提示會顯示測試執行) 的完整摘要。  
  
[測試結果] 頁面上提供下列按鈕：  
  
-   按一下 [ **View** ] \ （視圖 \）按鈕，開啟 [&#40;目前測試案例的 [OracleToSQL&#41;的 [查看測試案例報表 ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md) ]。  
  
-   按一下 [ **刪除** ] 按鈕，即可刪除選取的測試結果  
  
## <a name="see-also"></a>另請參閱  
[執行測試案例 &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[測試遷移的資料庫物件 &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
