---
title: 完成測試案例準備 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b31739bb4db23ccd2159ec8146ef857d7a5d66e5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631546"
---
# <a name="finishing-test-case-preparation-sybasetosql"></a>完成測試案例準備 (SybaseToSQL)
精靈的最後一頁會顯示測試案例描述和物件參與測試的相關資訊。 此外，在此頁面上您可以設定測試執行選項。  
  
**測試案例資訊**區段會顯示測試案例的名稱和描述。  
  
**測試物件**區段包含依物件類型分組的測試物件的具名的清單。  
  
**受影響的物件，以便進行分析**區段會顯示經過測試的物件執行之後，應該比較的資料變更物件的具名的清單。  
  
## <a name="test-case-settings"></a>測試案例設定  
在 **測試案例設定**區段，您可以設定下列執行測試選項：  
  
### <a name="stop-test-execution-after-first-failure"></a>停止後第一次失敗的測試執行  
指定要在測試執行期間發生錯誤時中斷測試。  
  
-   如果您選擇**是**，測試執行中斷，萬一發生錯誤。  
  
-   如果您選擇**No**，會發生錯誤之後繼續測試執行。  
  
### <a name="perform-data-rollback"></a>執行資料復原  
在測試執行後啟用自動的資料復原。  
  
-   如果您選擇**是**，測試執行之後，資料變更將會遺失。  
  
-   如果您選擇**No**，所有測試的執行將會儲存資料變更。  
  
### <a name="auxiliary-tables-saving-mode"></a>儲存模式的輔助資料表  
定義測試執行期間所建立的輔助資料表的儲存模式。 請參閱中的輔助資料表的說明[執行測試案例&#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md)主題。  
  
-   如果您選取**永遠儲存**，輔助資料表的資料一律會儲存供日後使用。  
  
-   如果您選取**如果資料表的比較無法儲存**，就會發生錯誤時，才會儲存輔助資料表的資料。  
  
-   如果您選取**永遠刪除**，輔助資料表永遠刪除之後執行測試。  
  
-   如果您選取**詢問使用者，如果資料表比較失敗**，萬一發生錯誤，使用者可以選取所需的動作。  
  
按一下 **完成**按鈕以儲存到已備妥的測試案例[使用測試存放庫&#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[使用測試存放庫&#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[執行測試案例&#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[測試移轉的資料庫物件&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
