---
title: 註冊已連接的伺服器 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], register connected servers
- connected server registrations [SQL Server]
ms.assetid: 77deb5f5-0f80-484f-8b8b-29afa67ec18f
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 66e01df7c294a684e646af2864f0284813684bf5
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2019
ms.locfileid: "67683938"
---
# <a name="register-a-connected-server-sql-server-management-studio"></a>註冊連接的伺服器 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (SSMS) 註冊 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中已連接的伺服器。 透過註冊伺服器，您可以儲存經常存取之伺服器的連接資訊。 您可以在連接之前或連接時從 [物件總管] 註冊伺服器。  您可以從功能表瀏覽至 [檢視]  \\[已註冊的伺服器]  ，在 SSMS 中檢視已註冊的伺服器。
  
 **本主題內容**  
  
-   **若要使用下列項目註冊伺服器：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-register-a-connected-server"></a>若要註冊連接的伺服器  
  
在物件總管中，以滑鼠右鍵按一下已連接的伺服器，然後按一下 [註冊]  。
  
**伺服器名稱**  
此欄位預設為連接的伺服器名稱。  或者您可以輸入伺服器名稱，或從下拉式清單中選擇一個。

**驗證**  
當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體時，有兩種可用的驗證模式。 

-    **Windows 驗證**  
Windows 驗證模式允許使用者透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者帳戶連接。 

-    **SQL Server 驗證**   
當使用者從非信任連接使用指定的登入名稱與密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會查看是否已設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼，自行執行驗證。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 沒有登入帳戶集，驗證將失敗，而使用者會收到錯誤訊息。

     > [!IMPORTANT]  
     > [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] 如需詳細資訊，請參閱 [選擇驗證模式](../../relational-databases/security/choose-an-authentication-mode.md)。  

     -    **User name**  
顯示您所連接的目前使用者名稱。 只有在您已選取使用 Windows 驗證進行連接時，才能使用此唯讀選項。 若要變更 **[使用者名稱]** ，請以不同使用者登入電腦。 

     -    **登入**  
輸入要用來連接的登入。 只有在您已選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接時，才可以使用此選項。  

     -    **密碼**  
輸入登入的密碼。 只有在您已選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接時，才可以編輯此選項。 

     -    **記住密碼**  
選取即可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 加密和儲存您輸入的密碼。 只有在您已選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接時，才會顯示此選項。  

          > [!NOTE]  
          > 如果您已儲存密碼而要停止儲存密碼，請清除此核取方塊，然後按一下 [儲存]  。  

**已註冊的伺服器名稱**  
您要在 [已註冊的伺服器] 上顯示的名稱。 此名稱不需要與 **[伺服器名稱]** 方塊中的名稱相符。  
  
**已註冊的伺服器描述**  
輸入伺服器的選擇性描述。  
  
**測試**  
按一下以測試與 [伺服器名稱]  中選取之伺服器的連接。  
  
**儲存**  
按一下即可儲存已註冊的伺服器設定。 

## <a name="see-also"></a>另請參閱  
[建立新的已註冊伺服器 (SQL Server Management Studio)](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)
  
  
