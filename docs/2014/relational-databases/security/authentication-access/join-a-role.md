---
title: 加入角色 | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASEUSER.MEMBERSHIP.F1
helpviewer_keywords:
- adding a member to a role
- join a role
ms.assetid: 05c8d10d-5823-46c6-8b1a-81722da6a42b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d1c846f7ed60bbecac64021e9a881312e1f1f64c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63011350"
---
# <a name="join-a-role"></a>加入角色
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中將角色指派給登入和資料庫使用者。 您可以在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中使用角色來有效率地管理權限。 您可以將權限指派給角色，然後在這些角色中加入和移除使用者與登入。 使用角色時，不需要針對每位使用者個別維護權限。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援四種類型的角色。  
  
-   固定伺服器角色  
  
-   使用者定義伺服器角色  
  
-   固定資料庫角色  
  
-   使用者定義資料庫角色  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]會自動提供固定角色。 固定角色擁有完成一般工作的必要權限。 如需有關固定角色的詳細資訊，請參閱下列連結。 使用者定義角色是由您所建立，而且可使用您所選取的權限來自訂。 如需有關使用者定義角色的詳細資訊，請參閱下列連結。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要將角色指派給登入和資料庫使用，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   變更資料庫角色的名稱不會變更識別碼、擁有者或角色的權限。  
  
-   您可以在 sys.database_role_members 和 sys.database_principals 目錄檢視中，看到資料庫角色。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要`ALTER ANY ROLE`資料庫的許可權、 `ALTER`角色的許可權，或**db_securityadmin**的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>若要將成員加入至固定伺服器角色  
  
1.  在 [物件總管] 中，展開要在其中編輯固定伺服器角色的伺服器。  
  
2.  展開 **[安全性]** 資料夾。  
  
3.  展開 **[伺服器角色]** 資料夾  
  
4.  以滑鼠右鍵按一下要編輯的角色，並且選取 [屬性]  。  
  
5.  在 [**伺服器角色屬性-**_server_role_name_ ] 對話方塊的 [**成員**] 頁面上，按一下 [**新增**]。  
  
6.  在 [選取伺服器登入或角色]  對話方塊中，於 [輸入要選取的物件名稱 (範例)]  底下輸入要加入至此伺服器角色的登入或伺服器角色。 或者，按一下 [瀏覽]  並選取 [瀏覽物件]  對話方塊中任何或所有可用的物件。 按一下 **[確定**]，返回 [**伺服器角色屬性-**_server_role_name_ ] 對話方塊。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>若要將成員加入至使用者定義資料庫角色  
  
1.  在 [物件總管] 中，展開要在其中編輯使用者定義資料庫角色的伺服器。  
  
2.  展開 **[資料庫]** 資料夾。  
  
3.  展開您要編輯其中使用者定義資料庫角色的伺服器。  
  
4.  展開 **[安全性]** 資料夾。  
  
5.  展開 **[角色]** 資料夾。  
  
6.  展開 **[伺服器角色]** 資料夾。  
  
7.  以滑鼠右鍵按一下要編輯的角色，並且選取 [屬性]  。  
  
8.  在 [**資料庫角色屬性-**_database_role_name_ ] 對話方塊的 [**一般**] 頁面中，按一下 [**新增**]。  
  
9. 在 [選取資料庫使用者或角色]  對話方塊中，於 [輸入要選取的物件名稱 (範例)]  底下輸入要加入至此資料庫角色的登入或資料庫角色。 或者，按一下 [瀏覽]  並選取 [瀏覽物件]  對話方塊中任何或所有可用的物件。 按一下 **[確定**]，返回 [**資料庫角色屬性-**_database_role_name_ ] 對話方塊。  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>若要將成員加入至固定伺服器角色  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    ALTER SERVER ROLE diskadmin ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [ALTER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-role-transact-sql)。  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>若要將成員加入至使用者定義資料庫角色  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    ALTER ROLE Marketing ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器層級角色](server-level-roles.md)   
 [資料庫層級角色](../authentication-access/database-level-roles.md)   
 [應用程式角色](../authentication-access/application-roles.md)  
  
  
