---
title: 完成測試案例準備 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 1b66f63b66066831d7e0276049d774136c1b5138
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743816"
---
# <a name="finishing-test-case-preparation-oracletosql"></a>完成測試案例準備 (OracleToSQL)
精靈的最後一頁會顯示測試案例描述和物件參與測試的相關資訊。 此外，在此頁面上您可以設定測試執行選項。  
  
**測試案例資訊**區段會顯示測試案例的名稱和描述。  
  
**物件選取至經過**區段包含依物件類型分組的測試物件的具名的清單。  
  
**物件會受到影響的測試，就會分析**區段會顯示經過測試的物件執行之後，應該比較的資料變更物件的具名的清單。  
  
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
定義測試執行期間所建立的輔助資料表的儲存模式。 請參閱中的輔助資料表的說明[執行測試案例&#40;OracleToSQL&#41; ](../../ssma/oracle/running-test-cases-oracletosql.md)主題。  
  
-   如果您選取**永遠儲存**，輔助資料表的資料一律會儲存供日後使用。  
  
-   如果您選取**如果資料表的比較無法儲存**，就會發生錯誤時，才會儲存輔助資料表的資料。  
  
-   如果您選取**永遠刪除**，輔助資料表永遠刪除之後執行測試。  
  
-   如果您選取**詢問使用者，如果資料表比較失敗**，萬一發生錯誤，使用者可以選取所需的動作。  
  
按一下 **完成**按鈕以儲存到已備妥的測試案例[使用測試存放庫 (OracleToSQL)](http://msdn.microsoft.com/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4)。  
  
## <a name="see-also"></a>另請參閱  
[使用測試存放庫&#40;OracleToSQL&#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[執行測試案例&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[測試移轉的資料庫物件&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
