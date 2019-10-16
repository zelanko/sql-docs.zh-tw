---
title: 建立 Database Mail 設定檔 | Microsoft 文件
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], public profiles
- profiles [SQL Server], Database Mail
- public profiles [Database Mail]
ms.assetid: 58ae749d-6ada-4f9c-bf00-de7c7a992a2d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 09b3759af6fc956d83daee464b5120fa80462dcf
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278318"
---
# <a name="create-a-database-mail-profile"></a>建立 Database Mail 設定檔
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  您可以使用 [Database Mail 組態精靈]  或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，建立 Database Mail 公用和私人設定檔。 如需郵件設定檔的詳細資訊，請參閱 [Database Mail 設定檔](database-mail-configuration-objects.md)。
  
-   **開始之前：** [必要條件](#Prerequisites)、[安全性](#Security)  
  
-   **使用下列方式建立 Database Mail 私人設定檔：** [Database Mail 設定精靈](#SSMSProcedure)、[Transact-SQL](#PrivateProfile)  
  
-   **使用下列方式建立 Database Mail 公用設定檔：** [Database Mail 設定精靈](#SSMSProcedure)、[Transact-SQL](#PublicProfile)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 替該設定檔建立一個或多個 Database Mail 帳戶。 如需建立 Database Mail 帳戶的詳細資訊，請參閱 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)。  
  
###  <a name="Security"></a> 安全性  
 公用設定檔可以讓任何可存取 **msdb** 資料庫的使用者使用該設定檔來傳送電子郵件。 使用者或角色可以使用私人設定檔。 為角色授與設定檔的存取權限時，會建立能夠更輕鬆維護的架構。 您必須是 **msdb** 資料庫中之 **DatabaseMailUserRole** 的成員，而且至少可以存取一個 Database Mail 設定檔，才能傳送郵件。  
  
####  <a name="Permissions"></a> 權限  
 建立設定檔帳戶以及執行預存程序的使用者，應該是系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
##  <a name="SSMSProcedure"></a> 使用 Database Mail 組態精靈  
 **建立 Database Mail 設定檔**  
  
-   在 [物件總管] 中，連接到想要在其上設定 Database Mail 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，並展開伺服器樹狀目錄。  
  
-   展開 **[管理]** 節點。  
  
-   按兩下 Database Mail，開啟 [Database Mail 組態精靈]。  
  
-   在 [選取組態工作]  頁面上，選取 [管理 Database Mail 帳戶和設定檔]  選項，然後按一下 [下一步]  。  
  
-   在 [管理設定檔和帳戶]  頁面上，選取 [建立新設定檔]  選項，然後按一下 [下一步]  。  
  
-   在 [新增設定檔]  頁面上，指定設定檔名稱、描述並新增要併入設定檔中的帳戶，然後按一下 [下一步]  。  
  
-   在 [完成精靈]  頁面上，檢閱要執行的動作，然後按一下 [完成]  完成新設定檔的建立。  
  
-   **若要設定 Database Mail 私人設定檔：**  
  
    -   開啟 [Database Mail 組態精靈]。  
  
    -   在 [選取組態工作]  頁面上，選取 [管理 Database Mail 帳戶和設定檔]  選項，然後按一下 [下一步]  。  
  
    -   在 [管理設定檔和帳戶]  頁面上，選取 [管理設定檔安全性]  選項，然後按一下 [下一步]  。  
  
    -   在 [私人設定檔]  索引標籤中，選取想要設定之設定檔的核取方塊，然後按一下 [下一步]  。  
  
    -   在 [完成精靈]  頁面上，檢閱要執行的動作，然後按一下 [完成]  完成設定檔的設定。  
  
-   **若要設定 Database Mail 公用設定檔：**  
  
    -   開啟 [Database Mail 組態精靈]。  
  
    -   在 [選取組態工作]  頁面上，選取 [管理 Database Mail 帳戶和設定檔]  選項，然後按一下 [下一步]  。  
  
    -   在 [管理設定檔和帳戶]  頁面上，選取 [管理設定檔安全性]  選項，然後按一下 [下一步]  。  
  
    -   在 [公用設定檔]  索引標籤中，選取想要設定之設定檔的核取方塊，然後按一下 [下一步]  。  
  
    -   在 [完成精靈]  頁面上，檢閱要執行的動作，然後按一下 [完成]  完成設定檔的設定。  
  
## <a name="using-transact-sql"></a>使用 Transact-SQL  
  
###  <a name="PrivateProfile"></a> 建立 Database Mail 私人設定檔  
  
-   連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
-   若要建立新的設定檔，請執行系統預存程序 [sysmail_add_profile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md)，如下所示：  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *\@profile_name* = '*設定檔名稱*'  
  
     *\@description* = '*描述*'  
  
     其中， *\@profile_name* 是定檔的名稱，而 *\@description* 是設定檔的描述。 這個參數是選擇性的。  
  
-   針對每個帳戶，執行預存程序 [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md)，如下所示：  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *\@profile_name* = '*設定檔的名稱*'  
  
     *\@account_name* = '*帳戶的名稱*'  
  
     *\@sequence_number* = '*帳戶在設定檔內的序號。* '  
  
     其中， *\@profile_name* 是設定檔的名稱， *\@account_name* 是要加入設定檔的帳戶名稱，而 *\@sequence_number* 可決定帳戶在設定檔中的使用順序。  
  
-   針對使用此設定檔傳送郵件的每個資料庫角色或使用者，授與設定檔的存取權。 作法是執行預存程序 [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql.md)，如下所示：  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *\@profile_name* = '*設定檔的名稱*'  
  
     *\@ principal_name* = '*資料庫使用者或角色的名稱*'  
  
     *\@is_default* = '*預設設定檔狀態* '  
  
     其中， *\@profile_name* 是設定檔的名稱， *\@principal_name* 是資料庫使用者或角色的名稱，而 *\@is_default* 可決定此設定檔是否為資料庫使用者或角色的預設值。  
  
 下列範例會建立 Database Mail 帳戶、建立 Database Mail 私人設定檔，然後將帳戶加入設定檔，並將設定檔的存取權授與 **msdb** 資料庫中的 **DBMailUsers** 資料庫角色。  
  
```  
-- Create a Database Mail account  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @account_name = 'AdventureWorks Administrator',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to the DBMailUsers role  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @principal_name = 'ApplicationUser',  
    @is_default = 1 ;  
```  
  
###  <a name="PublicProfile"></a> 建立 Database Mail 公用設定檔  
  
-   連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
-   若要建立新的設定檔，請執行系統預存程序 [sysmail_add_profile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md)，如下所示：  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *\@profile_name* = '*設定檔名稱*'  
  
     *\@description* = '*描述*'  
  
     其中， *\@profile_name* 是定檔的名稱，而 *\@description* 是設定檔的描述。 這個參數是選擇性的。  
  
-   針對每個帳戶，執行預存程序 [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md)，如下所示：  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *\@profile_name* = '*設定檔的名稱*'  
  
     *\@account_name* = '*帳戶的名稱*'  
  
     *\@sequence_number* = '*帳戶在設定檔內的序號。* '  
  
     其中， *\@profile_name* 是設定檔的名稱， *\@account_name* 是要加入設定檔的帳戶名稱，而 *\@sequence_number* 可決定帳戶在設定檔中的使用順序。  
  
-   若要授與公用存取權，請執行預存程序 [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql.md)，如下所示：  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *\@profile_name* = '*設定檔的名稱*'  
  
     *\@ principal_name* = '**public** 或 **0**'  
  
     *\@is_default* = '*預設設定檔狀態* '  
  
     其中， *\@profile_name* 是設定檔的名稱， *\@principal_name* 指出這是公用設定檔，而 *\@is_default* 可決定此設定檔是否為資料庫使用者或角色的預設值。  
  
 下列範例會建立 Database Mail 帳戶、建立 Database Mail 私人設定檔，然後將帳戶加入設定檔，並授與設定檔的公用存取權。  
  
```  
-- Create a Database Mail account  
  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Public Account',  
    @description = 'Mail account for use by all database users.',  
    @email_address = 'db_users@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @account_name = 'AdventureWorks Public Account',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to all users in the msdb database  
  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @principal_name = 'public',  
    @is_default = 1 ;  
```  
  
  
