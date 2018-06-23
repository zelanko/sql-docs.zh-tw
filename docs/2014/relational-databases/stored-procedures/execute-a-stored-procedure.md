---
title: 執行預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-stored-procs
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.executeprocedure.f1
- sql12.swb.executeprocedure.general.f1
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- extended stored procedures [SQL Server], executing
- system stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- user-defined stored procedures [SQL Server]
ms.assetid: a0b1337d-2059-4872-8c62-3f967d8b170f
caps.latest.revision: 37
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7ee1299fa575af8e2d19798a2bd38bf0a7a0acf4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034951"
---
# <a name="execute-a-stored-procedure"></a>執行預存程序
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的預存程序。  
  
 有兩種不同的方法可執行預存程序。 第一種是最常用的方法，可讓應用程式或使用者呼叫程序。 第二種方法是設定讓程序在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體啟動時自動執行。 當應用程式或使用者呼叫程序時， [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE 或 EXEC 關鍵字會在呼叫中明確陳述。 如果程序是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中的第一個陳述式，則呼叫和執行程序時也可以不用關鍵字。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要執行預存程序，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   比對系統程序名稱時，會使用呼叫資料庫定序。 因此，您務必在程序呼叫中使用大小寫完全相符的系統程序名稱。 例如，如果此程式碼是在有區分大小寫定序的資料庫內容中執行，就會失敗：  
  
    ```tsql  
    EXEC SP_heLP; -- Will fail to resolve because SP_heLP does not equal sp_help  
    ```  
  
     若要顯示完全相符的系統程序名稱，請查詢 [sys.system_objects](/sql/relational-databases/system-catalog-views/sys-system-objects-transact-sql) 和 [sys.system_parameters](/sql/relational-databases/system-catalog-views/sys-system-parameters-transact-sql) 目錄檢視。  
  
-   如果使用者定義程序與系統程序的名稱相同，則使用者定義程序可能永遠不會執行。  
  
###  <a name="Recommendations"></a> 建議  
  
-   執行系統預存程序  
  
     系統程序會以 **sp_** 前置詞開頭。 由於這些程序會以邏輯的方式出現在所有使用者和系統定義的資料庫中，因此可以從任何資料庫中執行，而不必完整限定程序名稱。 不過，我們建議您使用結構描述將所有系統程序名稱限定為 **sys** 結構描述名稱，以避免名稱衝突。 下列範例示範呼叫系統程序的建議方法。  
  
    ```tsql  
    EXEC sys.sp_who;  
    ```  
  
-   執行使用者自訂預存程序  
  
     當執行使用者定義的程序時，我們建議以結構描述名稱限定程序名稱。 這種作法可稍微提升效能，因為 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 不必搜尋多個結構描述。 如果資料庫在多個結構描述中有相同名稱的程序，它還可以避免執行錯誤的程序。  
  
     下列範例示範執行使用者定義程序的建議方法。 您會發現程序接受一個輸入參數。 如需指定輸入和輸出參數的相關資訊，請參閱 [指定參數](specify-parameters.md)。  
  
    ```tsql  
    USE AdventureWorks2012;  
    GO  
    EXEC dbo.uspGetEmployeeManagers @BusinessEntityID = 50;  
    ```  
  
     -或-  
  
    ```tsql  
    EXEC AdventureWorks2012.dbo.uspGetEmployeeManagers 50;  
    GO  
    ```  
  
     如果指定的是非限定使用者定義程序，則 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 會以下列順序搜尋該程序：  
  
    1.  目前資料庫的 **sys** 結構描述。  
  
    2.  如果在批次或動態 SQL 中執行，則為呼叫端的預設結構描述。 或者，如果非限定程序名稱出現在其他程序定義的主體內，則接下來會掃描包含這個其他程序的結構描述。  
  
    3.  目前資料庫中的 **dbo** 結構描述。  
  
-   自動執行預存程序  
  
     標記為自動執行的程序會在每次 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時執行，且 **master** 資料庫會在該啟動處理序期間復原。 設定自動執行程序在執行資料庫維護作業或讓程序做為背景處理序連續執行時相當實用。 自動執行的另一個用處就是讓程序執行 **tempdb**中的系統或維護工作，如建立全域的暫存資料表。 這樣可確保在 **啟動期間重新建立** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，這個暫存資料表一定會存在。  
  
     自動執行的程序運作時所使用的權限與 **sysadmin** (系統管理員) 固定伺服器角色的成員相同。 程序所產生的任何錯誤訊息都會寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中。  
  
     對於您能擁有的啟動程序數量並沒有限制，但請留意每一程序執行時都會佔用掉一個工作者執行緒。 如果您在啟動時必須執行多個程序但是並不需要同時執行它們，那麼您可以讓某一個程序成為啟動程序並且讓它叫用其他的程序。 這樣就只會使用一個工作者執行緒。  
  
    > [!TIP]  
    >  請不要從自動執行的程序傳回任何結果集。 因為這類程序是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而非應用程式或使用者執行，所以結果集會無處可去。  
  
-   設定、清除和控制自動執行  
  
     只有系統管理員 (**sa**) 可以將程序標示為自動執行。 此外，該程序必須位於 **master** 資料庫中，由 **sa**所擁有，並且不能有輸入或輸出參數。  
  
     使用 [sp_procoption](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql) 可以：  
  
    1.  指定一個現有的程序做為啟動程序。  
  
    2.  停止某個程序在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時執行。  
  
###  <a name="Security"></a> 安全性  
 如需詳細資訊，請參閱 [EXECUTE AS &#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-transact-sql) 和 [EXECUTE AS 子句 &#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-clause-transact-sql)。  
  
####  <a name="Permissions"></a> 權限  
 如需詳細資訊，請參閱 [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)中的預存程序。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-execute-a-stored-procedure"></a>若要執行預存程序  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，展開該執行個體，然後展開 [資料庫] 。  
  
2.  依序展開您要的資料庫、 **[可程式性]** 和 **[預存程序]**。  
  
3.  以滑鼠右鍵按一下您要的使用者定義預存程序，然後按一下 [執行預存程序]。  
  
4.  在 **[執行程序]** 對話方塊中，指定每個參數的值，以及是否應傳遞 null 值。  
  
     **參數**  
     指出參數的名稱。  
  
     **資料類型**  
     指出參數的資料類型。  
  
     **輸出參數**  
     指出這是否為輸出參數。  
  
     **傳遞 Null 值**  
     傳遞 NULL 作為參數的值。  
  
     **ReplTest1**  
     呼叫程序時輸入參數的值。  
  
5.  若要執行預存程序，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-execute-a-stored-procedure"></a>若要執行預存程序  
  
1.  連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例示範如何執行需要一個參數的預存程序。 此範例會執行 `uspGetEmployeeManagers` 預存程序，並指定值  `6` 做為 `@EmployeeID` 參數。  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
#### <a name="to-set-or-clear-a-procedure-for-executing-automatically"></a>若要設定或清除自動執行的程序  
  
1.  連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [sp_procoption](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql) 設定自動執行程序。  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = ] 'startup'   
    , @OptionValue = 'on';  
```  
  
#### <a name="to-stop-a-procedure-from-executing-automatically"></a>若要停止自動執行程序  
  
1.  連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [sp_procoption](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql) 設定停止自動執行程序。  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';  
```  
  
###  <a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
  
## <a name="see-also"></a>另請參閱  
 [指定參數](specify-parameters.md)   
 [設定 scan for startup procs 伺服器組態選項](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)   
 [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)   
 [預存程序 &#40;Database Engine&#41;](stored-procedures-database-engine.md)  
  
  
