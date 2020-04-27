---
title: 建立登入 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- creating a login
ms.assetid: a2512310-bdb6-41dc-858a-e866b2b58afc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7ceed5f82af858f6a2dc3a88df7276d5ba2fda3f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211201"
---
# <a name="creating-a-login"></a>建立登入
  若要存取 [!INCLUDE[ssDE](../includes/ssde-md.md)]，使用者需要登入。 登入可以用 Windows 帳戶或 Windows 群組的成員來代表使用者的身分識別，或者登入也可以是只存在於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登入。 請盡可能使用「Windows 驗證」。  
  
 依預設，電腦的管理員具有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的完整存取權。 在這一課中，我們希望有權限較低的使用者，因此您將會在電腦上建立新的本機「Windows 驗證」帳戶。 若要執行此作業，您必須是電腦的管理員。 接著，您將會為新使用者授與 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的存取權。  
  
### <a name="to-create-a-new-windows-account"></a>若要建立新的 Windows 帳戶  
  
1.  按一下 [**開始**]，按一下 [**執行**]，在 [ `%SystemRoot%\system32\compmgmt.msc /s`**開啟**] 方塊中輸入，然後按一下 **[確定]** 以開啟 [電腦管理] 程式。  
  
2.  在 [系統工具]**** 底下，展開 [本機使用者和群組]****，以滑鼠右鍵按一下 [使用者]****，然後按一下 [新增使用者]****。  
  
3.  在 [使用者名稱]**** 方塊中輸入 **Mary**。  
  
4.  在 [密碼]**** 和 [確認密碼]**** 方塊中輸入強式密碼，然後按一下 [建立]****，建立新的本機 Windows 使用者。  
  
### <a name="to-create-a-login"></a>若要建立登入  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的 [查詢編輯器] 視窗中，輸入並執行下列程式碼，並以您的電腦名稱取代 `computer_name` 。 `FROM WINDOWS` 表示 Windows 將會驗證使用者。 選擇性的 `DEFAULT_DATABASE` 引數會將 `Mary` 連接到 `TestData` 資料庫，除非她的連接字串指定要連接到其他資料庫。 這個陳述式採用分號作為 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式的選擇性結束符號。  
  
    ```  
    CREATE LOGIN [computer_name\Mary]  
        FROM WINDOWS  
        WITH DEFAULT_DATABASE = [TestData];  
    GO  
    ```  
  
     這個陳述式會授權使用者名稱 `Mary`在經過電腦驗證之後，可以存取這個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。 如果電腦上有一個以上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，則您必須在 `Mary` 需要存取的每一個執行個體上分別建立登入。  
  
    > [!NOTE]  
    >  由於 `Mary` 不是網域帳戶，因此這個使用者名稱只能在這部電腦上進行驗證。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [授與資料庫的存取權](lesson-2-2-granting-access-to-a-database.md)  
  
## <a name="see-also"></a>另請參閱  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [選擇驗證模式](../relational-databases/security/choose-an-authentication-mode.md)  
  
  
