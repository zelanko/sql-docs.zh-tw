---
description: 執行測試案例 (OracleToSQL)
title: 執行測試案例 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 9d44b04aba4d1ea1fa437bbd3b957178b361a4db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418434"
---
# <a name="running-test-cases-oracletosql"></a>執行測試案例 (OracleToSQL)
當 SSMA 測試人員執行測試案例時，它會執行選取要測試的物件，並建立有關驗證結果的報表。 如果兩個平臺上的結果都相同，測試就會成功。 物件與 Oracle 之間的對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據目前 SSMA 專案的架構對應設定來決定。  
  
成功測試的必要需求是所有 Oracle 物件都會轉換並載入至目標資料庫。 此外，也應該遷移資料表資料，以便同步處理兩個平臺上的資料表內容。  
  
## <a name="run-test-case"></a>執行測試案例  
若要執行已備妥的測試案例：  
  
1.  按一下 [執行]**** 按鈕。  
  
2.  在 [ **連接到 Oracle** ] 對話方塊中，輸入連接資訊，然後按一下 **[連接]**。  
  
測試完成時，會建立測試案例報表。 按一下 [ **報表** ] 按鈕，即可查看 [測試案例報表](viewing-test-case-reports-oracletosql.md)。 測試 (測試案例報表) 的結果會自動儲存在 [測試結果存放庫](using-test-repositories-oracletosql.md) 中，以供稍後使用。  
  
## <a name="test-case-execution-steps"></a>測試案例執行步驟  
  
### <a name="prerequisites"></a>先決條件  
SSMA 測試人員會在測試開始之前，檢查是否符合測試執行的所有必要條件。 如果未滿足某些條件，就會出現錯誤訊息。  
  
### <a name="initialization"></a>初始化  
在這個步驟中，SSMA 測試人員會在 Oracle 伺服器的 SSMATESTER_ORACLE 架構中， (資料表、觸發程式和 views) 建立輔助物件。 它們可讓您追蹤針對驗證所選擇之受影響物件中所做的變更。  
  
假設已驗證的資料表命名為 USER_TABLE。 針對這類資料表，會在 Oracle 中建立下列輔助物件。  
  
|名稱|類型|描述|  
|-|-|-|  
|USER_TABLE $ .Trg|觸發程序 (trigger)|觸發程式，以檢查已驗證資料表中的變更。|  
|USER_TABLE $ AUD|資料表|儲存刪除和覆寫資料列的資料表。|  
|USER_TABLE $ AUDID|資料表|儲存新的和已變更資料列的資料表。|  
|USER_TABLE|檢視|簡化資料表修改的表示。|  
|USER_TABLE $ NEW|檢視|簡化插入和覆寫資料列的表示。|  
|USER_TABLE $ NEW_ID|檢視|識別已插入和已變更的資料列。|  
|USER_TABLE $ OLD|檢視|簡化已刪除和已覆寫資料列的表示。|  
  
下列物件會在的已驗證資料表的架構中建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
|名稱|類型|描述|  
|-|-|-|  
|USER_TABLE $ .Trg|觸發程序 (trigger)|觸發程式，以檢查已驗證資料表中的變更。|  
  
而且，會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssmatesterdb 資料庫中建立下列物件。  
  
|名稱|類型|描述|  
|-|-|-|  
|USER_TABLE $ Aud|資料表|儲存刪除和覆寫資料列的資料表。|  
|USER_TABLE $ AudID|資料表|儲存新的和已變更資料列的資料表。|  
|USER_TABLE|檢視|簡化資料表修改的表示。|  
|USER_TABLE $ new|檢視|簡化插入和覆寫資料列的表示。|  
|USER_TABLE $ new_id|檢視|識別已插入和已變更的資料列。|  
|USER_TABLE $ old|檢視|簡化已刪除和已覆寫資料列的表示。|  
  
### <a name="test-object-calls"></a>測試物件呼叫  
在這個步驟中，SSMA 測試人員會叫用針對測試選取的每個物件、比較結果，並顯示報表。  
  
### <a name="finalization"></a>終止  
在完成期間，SSMA 測試人員會清除在 **初始化** 步驟建立的輔助物件。  
  
## <a name="next-step"></a>後續步驟  
[&#40;OracleToSQL&#41;觀看測試案例報表 ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[選取並設定要測試的物件 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[選取及設定受影響的物件 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[測試遷移的資料庫物件 &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
