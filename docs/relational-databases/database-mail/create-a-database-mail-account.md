---
title: "建立 Database Mail 帳戶| Microsoft 文件"
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
- Database Mail [SQL Server], accounts
- accounts [Database Mail]
ms.assetid: c07abbc6-fc6a-470b-8fa3-532f2e06b16a
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 603259e6c6d93d5fa92e2680dcc8939e51365033
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-database-mail-account"></a>建立 Database Mail 帳戶
  您可以使用 **「Database Mail 組態精靈」** 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，建立 Database Mail 帳戶。  
  
-   **Before you begin:**  [Prerequisites](#Prerequisites)  
  
-   **To Create a Database Mail Account, using:**  [Database Mail Configuration Wizard](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
-   **Follow Up:**  [Next Steps to Configure the Database Mail](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   判斷您用於傳送電子郵件之 Simple Mail Transfer Protocol (SMTP) 伺服器的伺服器名稱和通訊埠編號。如果 SMTP 伺服器需要驗證，請判斷 SMTP 伺服器的使用者名稱和密碼。  
  
-   (選擇性) 您也可以指定伺服器的類型和伺服器的通訊埠編號。 外寄郵件的伺服器類型一律為 'SMTP'。 大部分 SMTP 伺服器會使用通訊埠 25 (預設值)。  
  
##  <a name="SSMSProcedure"></a> 使用 Database Mail 組態精靈  
 **使用精靈建立 Database Mail 帳戶**  
  
-   在 [物件總管] 中，連接到想要在其上設定 Database Mail 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，並展開伺服器樹狀目錄。  
  
-   展開 **[管理]** 節點。  
  
-   按兩下 Database Mail，開啟 [Database Mail 組態精靈]。  
  
-   在 **[選取組態工作]** 頁面上，選取 **[管理 Database Mail 帳戶和設定檔]**，並按 **[下一步]**。  
  
-   在 **[管理設定檔和帳戶]** 頁面上，選取 **[建立新帳戶]** ，並按 **[下一步]**。  
  
-   在 **[新增帳戶]** 頁面上，指定帳戶名稱、描述、郵件伺服器資訊和驗證類型。 按 **[下一步]**  
  
-   在 **[完成精靈]** 頁面上，檢閱要執行的動作，並按一下 **[完成]** 完成新帳戶的建立。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **使用 Transact-SQL 建立 Database Mail 帳戶**  
  
 執行預存程序 **msdb.dbo.sysmail_add_account_sp** 來建立帳戶，並且指定下列資訊：  
  
-   要建立的帳戶名稱。  
  
-   帳戶的選擇性描述。  
  
-   要顯示於外寄電子郵件訊息的電子郵件地址。  
  
-   要顯示於外寄電子郵件訊息的顯示名稱。  
  
-   SMTP 伺服器的伺服器名稱。  
  
-   要用於登入 SMTP 伺服器的使用者名稱 (如果 SMTP 伺服器需要驗證的話)。  
  
-   要用於登入 SMTP 伺服器的密碼 (如果 SMTP 伺服器需要驗證的話)。  
  
 下列範例會建立新的 Database Mail 帳戶。  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
##  <a name="FollowUp"></a> 待處理：設定 Database Mail 的後續步驟  
  
-   [建立 Database Mail 設定檔](../../relational-databases/database-mail/create-a-database-mail-profile.md)  
  
  
