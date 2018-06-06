---
title: 完成測試案例準備 (SybaseToSQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cfb86c05dd96a6184bcbacf4cc7e6ac2b107b293
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="finishing-test-case-preparation-sybasetosql"></a>完成測試案例準備 (SybaseToSQL)
精靈的最後一頁會顯示描述測試案例和測試使用到物件的相關資訊。 此外，在此頁面上您可以設定測試執行選項。  
  
**測試案例資訊**區段會顯示的測試案例的名稱和描述。  
  
**測試物件**區段包含依物件類型分組的測試物件的具名的清單。  
  
**受影響的物件，以便進行分析**區段會顯示具名的資料變更應該比較測試的物件執行後的物件清單。  
  
## <a name="test-case-settings"></a>測試案例設定  
在**測試案例設定**> 一節，您可以設定下列執行測試的選項：  
  
### <a name="stop-test-execution-after-first-failure"></a>測試之後停止執行第一次失敗  
指定要中斷測試在測試執行期間發生錯誤。  
  
-   如果您選擇**是**，測試就會發生錯誤中斷執行。  
  
-   如果您選擇**否**，測試執行會在發生錯誤之後繼續。  
  
### <a name="perform-data-rollback"></a>執行資料復原  
測試執行之後啟用自動的資料復原。  
  
-   如果您選擇**是**，測試執行之後，資料變更將會遺失。  
  
-   如果您選擇**否**，所有測試的執行資料變更將會儲存。  
  
### <a name="auxiliary-tables-saving-mode"></a>儲存模式的輔助資料表  
定義測試執行期間所建立的輔助資料表的儲存模式。 請參閱中的輔助資料表的描述[執行測試案例&#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md)主題。  
  
-   如果您選取**永遠儲存**，輔助資料表的資料一律會儲存供稍後使用。  
  
-   如果您選取**儲存資料表的比較失敗**，就會發生錯誤時，才會儲存輔助資料表資料。  
  
-   如果您選取**永遠刪除**，輔助資料表永遠刪除之後執行測試。  
  
-   如果您選取**詢問使用者，如果資料表比較失敗**，使用者可以選取必要的動作，如果發生錯誤。  
  
按一下**完成**按鈕以儲存到已備妥的測試案例[使用測試儲存機制&#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[使用測試儲存機制&#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[執行測試案例&#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[測試移轉的資料庫物件 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
