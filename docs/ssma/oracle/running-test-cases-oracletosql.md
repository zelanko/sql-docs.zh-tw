---
title: 執行測試案例 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 917f18c705c5cb0615cc5ac0b702f31372cf8a8a
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393605"
---
# <a name="running-test-cases-oracletosql"></a>執行測試案例 (OracleToSQL)
當 SSMA 軟體測試人員執行測試案例時，它會執行測試所選取的物件，並建立驗證結果的相關報表。 如果這兩個平台上相同的結果，測試成功。 Oracle 之間的物件的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取決於目前的 SSMA 專案的結構描述對應設定。  
  
Oracle 的所有物件會轉換和載入到目標資料庫的成功測試的必要需求。 此外，以便同步處理的兩個平台上的資料表內容，應該移轉資料表的資料。  
  
## <a name="run-test-case"></a>執行測試案例  
若要執行已備妥的測試案例：  
  
1.  按一下 [**執行**] 按鈕。  
  
2.  在 [**連接到 Oracle** ] 對話方塊中，輸入連接資訊，，然後按一下**Connect**。  
  
測試完成時，會建立測試案例報表。 按一下 **報表**按鈕，以檢視[測試案例報表](viewing-test-case-reports-oracletosql.md)。 測試 （測試案例報表） 的結果會自動儲存在[測試結果儲存機制](using-test-repositories-oracletosql.md)供稍後使用。  
  
## <a name="test-case-execution-steps"></a>測試案例執行步驟  
  
### <a name="prerequisites"></a>先決條件  
SSMA 軟體測試人員會檢查是否符合所有必要條件，以測試執行開始前的測試。 如果不符合一些條件，便會出現錯誤訊息。  
  
### <a name="initialization"></a>初始化  
此步驟中，SSMA 軟體測試人員會在 Oracle 伺服器的 SSMATESTER_ORACLE 結構描述中建立輔助物件 （資料表、 觸發程序和檢視）。 它們可讓受影響的物件選擇的驗證中所做的追蹤變更。  
  
假設已驗證的資料表名為 USER_TABLE。 如需這類的表格中，會在 Oracle 中建立下列輔助物件。  
  
||||  
|-|-|-|  
|名稱|類型|描述|  
|USER_TABLE$ Trg|觸發程序 (trigger)|稽核的變更已驗證的資料表中的觸發程序。|  
|USER_TABLE$ 澳幣|資料表|儲存已刪除和覆寫的資料列的資料表。|  
|USER_TABLE$ AUDID|資料表|儲存新的和變更的資料列的資料表。|  
|USER_TABLE|檢視|資料表修改簡化表示法。|  
|新 USER_TABLE $|檢視|簡化的插入與覆寫的資料列表示。|  
|USER_TABLE$ NEW_ID|檢視|識別已插入和已變更的資料列。|  
|USER_TABLE$ 舊|檢視|簡化的已刪除和覆寫的資料列表示。|  
  
在已驗證的資料表結構描述中建立下列物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
||||  
|-|-|-|  
|名稱|類型|描述|  
|USER_TABLE$ Trg|觸發程序 (trigger)|稽核的變更已驗證的資料表中的觸發程序。|  
  
下列物件會在建立和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ssmatesterdb 資料庫中。  
  
||||  
|-|-|-|  
|名稱|類型|描述|  
|USER_TABLE$ 澳幣|資料表|儲存已刪除和覆寫的資料列的資料表。|  
|USER_TABLE$ AudID|資料表|儲存新的和變更的資料列的資料表。|  
|USER_TABLE|檢視|資料表修改簡化表示法。|  
|新的 USER_TABLE $|檢視|簡化的插入與覆寫的資料列表示。|  
|USER_TABLE$ new_id|檢視|識別已插入和已變更的資料列。|  
|USER_TABLE $ 舊|檢視|簡化的已刪除和覆寫的資料列表示。|  
  
### <a name="test-object-calls"></a>測試物件呼叫  
在此步驟中，SSMA 軟體測試人員會叫用所選測試每個物件，比較結果，並顯示報表。  
  
### <a name="finalization"></a>最終處理  
在最終處理期間 SSMA 軟體測試人員會清除在建立輔助物件**初始化**步驟。  
  
## <a name="next-step"></a>下一個步驟  
[檢視測試案例報表&#40;OracleToSQL&#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[選取並設定要測試的物件&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[選取並設定受影響的物件&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[測試移轉的資料庫物件&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
