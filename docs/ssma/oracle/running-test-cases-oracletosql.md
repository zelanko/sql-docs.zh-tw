---
title: "執行測試案例 (OracleToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: ff5baf3dadeee06d33f5d75f0c62a1ee339ba2b3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="running-test-cases-oracletosql"></a>執行測試案例 (OracleToSQL)
當 SSMA 軟體測試人員執行測試案例時，它會執行測試所選取的物件，並建立驗證結果的相關報表。 如果兩個平台上相同的結果，測試成功。 Oracle 之間的物件的對應關係和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]取決於目前的 SSMA 專案的結構描述對應設定。  
  
成功的測試的必要需求是 Oracle 的所有物件會轉換和載入到目標資料庫。 此外，以便同步處理兩個平台上的資料表的內容應該移轉資料表資料。  
  
## <a name="run-test-case"></a>執行測試案例  
若要執行已備妥的測試案例：  
  
1.  按一下**執行** 按鈕。  
  
2.  在**Connect to Oracle**對話方塊中，輸入連接資訊，，然後按一下**連接**。  
  
測試完成時，會建立測試案例報表。 按一下**報表**按鈕，以檢視[測試案例報表](http://msdn.microsoft.com/en-us/8da14323-9dd6-4019-bf79-3e8b972a9bc0)。 測試 （測試案例報表） 的結果會自動儲存在[測試結果儲存機制](http://msdn.microsoft.com/en-us/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4)供日後使用。  
  
## <a name="test-case-execution-steps"></a>測試案例執行步驟  
  
### <a name="prerequisites"></a>必要條件  
SSMA 軟體測試人員會檢查測試在測試執行開始之前是否符合所有必要條件。 如果未滿足一些條件，便會出現錯誤訊息。  
  
### <a name="initialization"></a>初始化  
在此步驟中，SSMA 軟體測試人員會建立在 Oracle 伺服器 SSMATESTER_ORACLE 結構描述中輔助物件 （資料表、 觸發程序和檢視）。 可選擇進行驗證的受影響物件中所做的追蹤變更。  
  
假設已驗證的資料表，名為 USER_TABLE。 若是資料表，會在 Oracle 中建立下列輔助物件。  
  
||||  
|-|-|-|  
|名稱|型別|Description|  
|USER_TABLE$ Trg|觸發程序 (trigger)|稽核的變更已驗證的資料表中的觸發程序。|  
|USER_TABLE$ 則|table|儲存已刪除和覆寫的資料列的資料表。|  
|USER_TABLE$ AUDID|table|儲存新和已變更的資料列的資料表。|  
|USER_TABLE|檢視|資料表修改簡化表示法。|  
|新 USER_TABLE $|檢視|簡化的插入和覆寫的資料列的表示法。|  
|USER_TABLE$ NEW_ID|檢視|插入和已變更資料列的識別。|  
|USER_TABLE$ 舊|檢視|簡化的已刪除和覆寫的資料列的表示法。|  
  
在已驗證的資料表結構描述中建立下列物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
||||  
|-|-|-|  
|名稱|型別|Description|  
|USER_TABLE$ Trg|觸發程序 (trigger)|稽核的變更已驗證的資料表中的觸發程序。|  
  
下列物件會在建立和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ssmatesterdb 資料庫中。  
  
||||  
|-|-|-|  
|名稱|型別|Description|  
|USER_TABLE$ 則|table|儲存已刪除和覆寫的資料列的資料表。|  
|USER_TABLE$ AudID|table|儲存新和已變更的資料列的資料表。|  
|USER_TABLE|檢視|資料表修改簡化表示法。|  
|新的 USER_TABLE $|檢視|簡化的插入和覆寫的資料列的表示法。|  
|USER_TABLE$ new_id|檢視|插入和已變更資料列的識別。|  
|舊的 USER_TABLE $|檢視|簡化的已刪除和覆寫的資料列的表示法。|  
  
### <a name="test-object-calls"></a>測試物件呼叫  
在此步驟中，SSMA 測試人員會叫用每個測試選取的物件、 比較結果，並顯示的報表。  
  
### <a name="finalization"></a>最終處理  
在最終處理期間 SSMA 軟體測試人員會清除在建立輔助物件**初始化**步驟。  
  
## <a name="next-step"></a>下一個步驟  
[檢視測試案例報表 &#40; OracleToSQL &#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>請參閱＜  
[選取和設定物件測試 &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[選取並設定受影響物件 &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[測試移轉的資料庫物件 &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
