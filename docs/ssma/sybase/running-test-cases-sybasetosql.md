---
title: 執行測試案例 (SybaseToSQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 5751a704fdea6e7c87aa43e1b4fedc1107d89f8c
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34779354"
---
# <a name="running-test-cases-sybasetosql"></a>執行測試案例 (SybaseToSQL)
當 SSMA 軟體測試人員執行測試案例時，它會執行測試所選取的物件，並建立驗證結果的相關報表。 如果兩個平台上相同的結果，測試成功。 Sybase 之間物件的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]取決於目前的 SSMA 專案的結構描述對應設定。  
  
成功的測試的必要需求是所有 Sybase 物件會轉換和載入到目標資料庫。 此外，以便同步處理兩個平台上的資料表的內容應該移轉資料表資料。  
  
## <a name="run-test-case"></a>執行測試案例  
若要執行已備妥的測試案例：  
  
1.  按一下**執行** 按鈕。  
  
2.  在**連接到 Sybase**對話方塊中，輸入連接資訊，，然後按一下**連接**。  
  
測試完成時，會建立測試案例報表。 按一下**報表**按鈕，以檢視[檢視測試案例報表&#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)。 測試 （測試案例報表） 的結果會自動儲存在[使用測試儲存機制&#40;SybaseToSQL&#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md)供日後使用。  
  
## <a name="test-case-execution-steps"></a>測試案例執行步驟  
  
### <a name="prerequisites"></a>必要條件  
SSMA 軟體測試人員會檢查測試在測試執行開始之前是否符合所有必要條件。 如果未滿足一些條件，便會出現錯誤訊息。  
  
### <a name="initialization"></a>初始化  
在此步驟中，SSMA 軟體測試人員建立輔助物件 （資料表、 觸發程序和檢視） 這兩個在 Sybase 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 它們可讓受影響的資料表選擇進行驗證，如果資料表比較模式中所做的追蹤變更**只變更**。  
  
假設已驗證的資料表，名為 USER_TABLE。 若是資料表，下列的輔助物件會建立 Sybase 中。  
  
下列物件會建立在 Sybase SSMATESTER2005db 或 SSMATESTER2008db 資料庫中，而是在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ssmatesterdb_syb 資料庫中。  
  
|[屬性]|類型|描述|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|觸發程序|稽核的變更已驗證的資料表中的觸發程序。|  
|USER_TABLE$ 則|Table|儲存已刪除和覆寫的資料列的資料表。|  
|USER_TABLE$ AudID|Table|儲存新和已變更的資料列的資料表。|  
|USER_TABLE|檢視|資料表修改簡化表示法。|  
|新的 USER_TABLE $|檢視|簡化的插入和覆寫的資料列的表示法。|  
|USER_TABLE$ new_id|檢視|插入和已變更資料列的識別。|  
|舊的 USER_TABLE $|檢視|簡化的已刪除和覆寫的資料列的表示法。|  
  
已驗證的 Sybase 資料表的資料庫中建立下列物件和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
|[屬性]|類型|描述|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|觸發程序|稽核的變更已驗證的資料表中的觸發程序。|  
  
### <a name="test-object-calls"></a>測試物件呼叫  
在此步驟中，SSMA 測試人員會叫用每個測試選取的物件、 比較結果，並顯示的報表。  
  
### <a name="finalization"></a>最終處理  
在最終處理期間 SSMA 軟體測試人員會清除在建立輔助物件**初始化**步驟。  
  
## <a name="next-step"></a>下一個步驟  
[檢視測試案例報表&#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[選取和設定測試的物件&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[選取並設定受影響的物件&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[測試移轉的資料庫物件&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
