---
title: "建立認證 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- credentials [SQL Server], creating
- authentication [SQL Server], credentials
- logins [SQL Server], credentials
ms.assetid: c1e77e91-2a69-40d9-b8b3-97cffc710586
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 80dba3f156735179c0fb016e39f3065acd6f5ac1
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-credential"></a>建立認證
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中建立認證。  
  
 認證提供允許 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證使用者擁有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]以外之識別的方法。 這主要是用來執行具 EXTERNAL_ACCESS 權限集之組件中的程式碼。 認證也可以在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證使用者需要存取網域資源時使用，例如儲存備份的檔案位置。  
  
 認證可以同時對應至數個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入每次只能對應至一個認證。 建立認證之後，請使用 [登入屬性 (一般頁面)]**** 將登入對應至認證。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目建立認證：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果提供者沒有任何登入對應認證，系統就會使用對應至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶的認證。  
  
-   一個登入可以具有多個對應認證，只要這些認證用於不同的提供者即可。 但是，每個登入的每個提供者必須只有一個對應認證。 相同的認證可對應至其他登入。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要 ALTER ANY CREDENTIAL 權限才能建立或修改認證，以及 ALTER ANY LOGIN 權限才能將登入對應至認證。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-credential"></a>若要建立認證  
  
1.  在物件總管中，展開 [安全性] **** 資料夾。  
  
2.  以滑鼠右鍵按一下 [認證]**** 資料夾，然後選取 [新增認證…]****。  
  
3.  在 **[新增認證]** 對話方塊的 **[認證名稱]** 方塊中，輸入認證的名稱。  
  
4.  在 [識別]**** 方塊中，輸入用於傳出連線 (離開 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內容時) 的帳戶名稱。 通常，這將是 Windows 使用者帳戶，但識別可以是另一種類型的帳戶。  
  
     或者，按一下省略符號 **(...)** 開啟 [選取使用者或群組]**** 對話方塊。  
  
5.  在 **[密碼]** 與 **[確認密碼]** 方塊中，輸入 **[識別]** 方塊中所指定的帳戶密碼。 如果 **[識別]** 是 Windows 使用者帳戶，則為 Windows 密碼。 如果不需要密碼， **[密碼]** 可以是空白。  
  
6.  選取 [使用加密提供者]****，設定要由可延伸金鑰管理 (EKM) 提供者所驗證的認證。 如需詳細資訊，請參閱[可延伸金鑰管理 &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-credential"></a>若要建立認證  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- Creates the credential called "AlterEgo.".   
    -- The credential contains the Windows user "Mary5" and a password.  
    CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
        SECRET = '<EnterStrongPasswordHere>';  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)。  
  
  
