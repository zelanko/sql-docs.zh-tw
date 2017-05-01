---
title: "建立伺服器稽核與伺服器稽核規格 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.SWB.SQLAUDIT.FILTER.F1
- sql13.swb.sqlaudit.general.f1
- sql13.swb.sqlaudit.srvaudit.general.f1
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
ms.assetid: 6624b1ab-7ec8-44ce-8292-397edf644394
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e33a4ff076039b03c399a0f7868bf697ca1cd8d0
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-server-audit-and-server-audit-specification"></a>建立伺服器稽核與伺服器稽核規格
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中建立伺服器稽核和伺服器稽核規格。 *「稽核」* (Audit) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的執行個體牽涉到追蹤和記錄系統上所發生的事件。 *SQL Server Audit* 物件會收集要監視之動作和動作群組 (伺服器層級或資料庫層級) 的單一執行個體。 此稽核位於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體層級。 您可以針對每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體設有多個稽核。 *「伺服器稽核規格」* (Server Audit Specification) 物件屬於稽核。 您可以針對每個稽核建立一個伺服器稽核規格，因為這兩者都是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體範圍所建立。 如需詳細資訊，請參閱 [SQL Server Audit &#40;Database Engine&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目建立伺服器稽核和伺服器稽核規格：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   在您為它建立伺服器稽核規格之前，必須有稽核存在。 當建立伺服器稽核規格之後，它就會處於停用狀態。  
  
-   CREATE SERVER AUDIT 陳述式位於交易的範圍內。 如果回復交易，也會回復此陳述式。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
  
-   若要建立、更改或卸除伺服器稽核，主體需要使用 ALTER ANY SERVER AUDIT 或 CONTROL SERVER 權限。  
  
-   具有 ALTER ANY SERVER AUDIT 權限的使用者可以建立伺服器稽核規格，並將其繫結至任何稽核。  
  
-   一旦建立伺服器稽核規格之後，就可以使用具有 CONTROL SERVER 或 ALTER ANY SERVER AUDIT 權限的主體、系統管理員 (sysadmin) 帳戶或具有此稽核之明確存取權的主體來加以檢視。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>若要建立伺服器稽核  
  
1.  在 [物件總管] 中，展開 **[安全性]** 資料夾。  
  
2.  以滑鼠右鍵按一下 [稽核] 資料夾，然後選取 [新增稽核]。  
  
     下列選項可從 **[建立稽核]** 對話方塊的 **[一般]** 頁面取得。  
  
     **稽核名稱**  
     稽核的名稱。 當您建立新的稽核時會自動產生這個名稱，但是可加以編輯。  
  
     **佇列延遲 (以毫秒為單位)**  
     指定在強制處理稽核動作之前經過的時間長度 (以毫秒為單位)。  值為 0 表示同步傳遞。 預設的最小值為 **1000** (1 秒鐘)。 最大值為 2,147,483,647 (2,147,483.647 秒鐘或是 24 天 20 小時 31 分鐘又 23.647 秒鐘)。  
  
     **於稽核記錄失敗時:**  
     **Continue**  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 作業繼續進行。 系統不會保留稽核記錄。 稽核會繼續嘗試記錄事件，而且如果失敗狀況已解決，就會恢復稽核。 選取 **[繼續]** 選項會允許可能違反安全性原則的未稽核活動。 當繼續進行 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 作業比維持完整稽核更重要時，請選取此選項。 這是預設選項。  
  
     **關閉伺服器**  
     當寫入目標的伺服器執行個體無法將資料寫入稽核目標時，強制伺服器關閉。 發出此內容的登入必須具有 **SHUTDOWN** 權限。 如果登入沒有此權限，這個功能將會失敗，而且將會引發錯誤訊息。 不會發生稽核的事件。 當稽核失敗可能危害系統的安全性或完整性時，請選取此選項。  
  
     **讓作業失敗**  
     當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit 無法寫入稽核記錄時，如果資料庫動作會以其他方式導致稽核事件，這個選項就會讓這些動作失敗。 不會發生稽核的事件。 不會導致稽核事件的動作可繼續進行。 稽核會繼續嘗試記錄事件，而且如果失敗狀況已解決，就會恢復稽核。 當維持完整稽核比 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的完整存取權更重要時，請選取此選項。  
  
    > [!IMPORTANT]  
    >  當稽核處於失敗狀態時，專用管理員連接可以繼續執行稽核事件。  
  
     [稽核目的地] 清單  
     指定稽核資料的目標。 可用的選項有二進位檔案、Windows 應用程式記錄檔或 Windows 安全性記錄檔。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 就無法寫入 Windows 安全性記錄檔。 如需詳細資訊，請參閱 [將 SQL Server Audit 事件寫入安全性記錄檔](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)。  
  
     **檔案路徑**  
     指定當 [稽核目的地] 為檔案時，要寫入稽核資料的資料夾位置。  
  
     **省略符號 (...)**  
     開啟 [尋找資料夾 – *server_name*] 對話方塊，指定檔案路徑或建立要寫入稽核檔案的資料夾。  
  
     **稽核檔案最大限制:**  
     **輪用檔案數量上限**  
     指定在達到最大稽核檔案數目時，新的檔案內容就會覆寫最舊的稽核檔案。  
  
     **檔案上限**  
     指定在達到最大稽核檔案數目時，導致系統產生其他稽核事件的任何動作都將失敗並發生錯誤。  
  
     [無限制] 核取方塊  
     若已選取 [最大換用檔案] 底下的 [無限制] 核取方塊，則要建立的稽核檔案數目就不受限制。 **[無限制]** 核取方塊預設為已選取，並套用至 **[輪用檔案數量上限]** 和 **[檔案數量上限]** 選項。  
  
     [檔案數目] 方塊  
     指定要建立的稽核檔案數目，上限為 2,147,483,647。 只有未核取 **[無限制]** 時，才能使用此選項。  
  
     **檔案大小上限**  
     指定稽核檔案的大小上限，以 MB、GB 或 TB 為單位。 您可以指定介於 1024 MB 和 2,147,483,647 TB 之間的值。 選取 **[無限制]** 核取方塊並不會限制檔案大小。 指定低於 1024 MB 的值將會失敗並傳回錯誤。 依預設， **[無限制]** 核取方塊已選取。  
  
     [保留磁碟空間] 核取方塊  
     指定在磁碟上預先配置的空間等於指定的檔案大小上限。 只有未選取 **[檔案大小上限]** 底下的 **[無限制]** 核取方塊時，才能使用此設定。 依預設，這個核取方塊未選取。  
  
3.  選擇性地在 **[篩選]** 頁面上，對伺服器稽核輸入述詞或 `WHERE` 子句，以指定 **[一般]** 頁面上未提供的其他選項。 將述詞包含在括號內，例如 `(object_name = 'EmployeesTable')`。  
  
4.  當您完成選取選項之後，按一下 **[確定]**。  
  
#### <a name="to-create-a-server-audit-specification"></a>若要建立伺服器稽核規格  
  
1.  在 [物件總管] 中，按一下加號展開 **[安全性]** 資料夾。  
  
2.  以滑鼠右鍵按一下 [伺服器稽核規格] 資料夾，然後選取 [新增伺服器稽核規格]。  
  
     **[建立伺服器稽核規格]** 對話方塊有下列選項。  
  
     **名稱**  
     伺服器稽核規格的名稱。 當您建立新的伺服器稽核規格時會自動產生這個名稱，但是可加以編輯。  
  
     **稽核**  
     現有伺服器稽核的名稱。 請輸入稽核名稱或從清單中選取。  
  
     **稽核動作類型**  
     指定要擷取之伺服器層級的稽核動作群組和稽核動作。 如需資料庫層級的稽核動作群組和稽核動作清單以及其所包含的事件描述，請參閱 [SQL Server Audit 動作群組和動作](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
     **物件結構描述**  
     顯示指定之 [物件名稱] 的結構描述。  
  
     **Object Name**  
     要稽核的物件名稱。 這只適用於稽核動作，不適用於稽核群組。  
  
     **省略符號 (...)**  
     開啟 **[選取物件]** 對話方塊來瀏覽及選取可用的物件 (根據指定的 **[稽核動作類型]**)。  
  
     **主體名稱**  
     依據所稽核的物件來篩選稽核的帳戶。  
  
     **省略符號 (...)**  
     開啟 **[選取物件]** 對話方塊來瀏覽及選取可用的物件 (根據指定的 **[物件名稱]**)。  
  
3.  完成後，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>若要建立伺服器稽核  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- Creates a server audit called "HIPPA_Audit" with a binary file as the target and no options.  
    CREATE SERVER AUDIT HIPAA_Audit  
        TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
    ```  
  
#### <a name="to-create-a-server-audit-specification"></a>若要建立伺服器稽核規格  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    /*Creates a server audit specification called "HIPPA_Audit_Specification" that audits failed logins for the SQL Server audit "HIPPA_Audit" created above.  
    */  
  
    CREATE SERVER AUDIT SPECIFICATION HIPPA_Audit_Specification  
    FOR SERVER AUDIT HIPPA_Audit  
        ADD (FAILED_LOGIN_GROUP);  
    GO  
    -- Enables the audit.   
  
    ALTER SERVER AUDIT HIPAA_Audit  
    WITH (STATE = ON);  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md) 和 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)。  
  
  
