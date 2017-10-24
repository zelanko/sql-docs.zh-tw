---
title: "建立登入 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_LOGIN_TSQL
- CREATE LOGIN
- LOGIN_TSQL
- LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], logins
- mapping logins [SQL Server]
- logins [SQL Server], creating
- CREATE LOGIN statement
- permissions [SQL Server], logins
- Windows domain accounts [SQL Server]
- re-hashing passwords
- certificates [SQL Server], logins
ms.assetid: eb737149-7c92-4552-946b-91085d8b1b01
caps.latest.revision: 101
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: e0b84743a9c3c578954560613c69f2863af8aa01
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="create-login-transact-sql"></a>CREATE LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  建立 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 登入。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  
  
CREATE LOGIN login_name { WITH <option_list1> | FROM <sources> }  
  
<option_list1> ::=   
    PASSWORD = { 'password' | hashed_password HASHED } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
    SID = sid  
    | DEFAULT_DATABASE = database      
    | DEFAULT_LANGUAGE = language  
    | CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
    | CREDENTIAL = credential_name   
  
<sources> ::=  
    WINDOWS [ WITH <windows_options>[ ,... ] ]  
    | CERTIFICATE certname  
    | ASYMMETRIC KEY asym_key_name  
  
<windows_options> ::=        
    DEFAULT_DATABASE = database  
    | DEFAULT_LANGUAGE = language  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE LOGIN login_name  
 { WITH <option_list3> }  
  
<option_list3> ::=   
    PASSWORD = { 'password' }  
    [ SID = sid ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE LOGIN loginName { WITH <option_list1> | FROM WINDOWS }  
  
<option_list1> ::=   
    PASSWORD = { 'password' } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
      CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
```  
  
## <a name="arguments"></a>引數  
 *login_name*  
 指定建立的登入名稱。 有四種類型的登入：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入、Windows 登入、憑證對應登入和非對稱金鑰對應登入。 當您從 Windows 網域帳戶建立對應的登入時，您必須使用 windows 2000 前版的使用者登入名稱格式 [\<domainName >\\< login_name >]。 您無法使用的 UPN 格式login_name@DomainName。 如需範例，請參閱本主題稍後的範例 D。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證登入屬於型別**sysname**而且必須符合的規則[識別碼](http://msdn.microsoft.com/library/ms175874.aspx)且不能包含 '**\\**'。 Windows 登入可以包含 '**\\**'。 根據 Active Directory 使用者的登入僅限於小於 21 個字元的名稱。  
  
 密碼**='***密碼***'**  
 只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 指定要建立的登入密碼。 您應該使用增強式密碼。 如需詳細資訊，請參閱[強式密碼](../../relational-databases/security/strong-passwords.md)和[密碼原則](../../relational-databases/security/password-policy.md)。 開頭為[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 預存密碼資訊會計算使用之 salt 的密碼 sha-512。  
  
 密碼會區分大小寫。 密碼長度應該一律至少為 8 個字元，且不能超過 128 個字元。  密碼可以包含 a-z、A-Z、0-9 及大多數非英數字元。 密碼不能包含單引號或*login_name*。  
  
 密碼 **=**  *hashed_password*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 僅適用於 HASHED 關鍵字。 指定要建立之登入的密碼雜湊值。  
  
 HASHED  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 指定在 PASSWORD 引數之後輸入的密碼已雜湊處理。 如果未選取這個選項，則輸入的密碼字串在儲存至資料庫之前會先雜湊處理。 只有要在兩部伺服器之間移轉資料庫時，才應使用這個選項。 請勿使用 HASHED 選項來建立新登入。 HASHED 選項無法與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7 或更早版本所建立的雜湊搭配使用。  
  
 MUST_CHANGE  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 如果有包含這個選項，第一次使用新登入時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提示使用者輸入新密碼。  
  
 認證 **=**  *credential_name*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 對應到新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的認證名稱。 認證必須已存在於伺服器中。 目前這個選項只會將認證連結到登入。 認證無法對應至系統管理員 (sa) 登入。  
  
 SID = *sid*  
 用來重新建立登入。 適用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]只驗證登入，沒有 Windows 驗證登入。 指定新的 SID[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證登入。 如果未使用此選項，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自動指派 SID。 SID 結構取決於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入 SID: 16 位元組 (**binary （16)**) GUID 為基礎的常值。 例如 `SID = 0x14585E90117152449347750164BA00A7`。  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)]登入 SID： 的有效 SID 結構[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 這通常是 32 位元組 (**binary(32)**) 常值組成`0x01060000000000640000000000000000`加上代表 GUID 的 16 位元組。 例如 `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`。  
  
DEFAULT_DATABASE  **=** *資料庫*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定要指派給登入的預設資料庫。 如果不包括這個選項，預設資料庫將設為 master。  
  
DEFAULT_LANGUAGE  **=** *語言*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定要指派給登入的預設語言。 如果不包括這個選項，預設語言將設為伺服器的目前預設語言。 如果伺服器的預設語言在未來有所變更，登入的預設語言會保持不變。  
  
CHECK_EXPIRATION  **=**  {ON |**OFF** }  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 指定是否應該對這個登入強制執行密碼逾期原則。 預設值是 OFF。  
  
CHECK_POLICY  **=**  { **ON** |OFF}  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 指定應該在這項登入上強制使用執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦的 Windows 密碼原則。 預設值是 ON。  
  
 如果 Windows 原則要求增強式密碼，則密碼必須至少包含下列四個特性的其中三個：  
  
-   大寫字元 (A-Z)。  
-   小寫字元 (a-z)。  
-   數字 (0-9)。  
-   其中一個非英數字元，例如空格、_、@、*、^、%、!、$、# 或 &。  
  
WINDOWS  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定登入對應到 Windows 登入。  
  
憑證*certname*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定與這項登入相關聯的憑證名稱。 這個憑證必須已存在於 master 資料庫中。  
  
非對稱金鑰*asym_key_name*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定與這項登入相關聯的非對稱金鑰名稱。 這個金鑰必須已存在於 master 資料庫中。  
  
## <a name="remarks"></a>備註  
 密碼會區分大小寫。  
  
 僅當您建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入時，才支援預先雜湊處理密碼。  
  
 如果指定 MUST_CHANGE，則 CHECK_EXPIRATION 和 CHECK_POLICY 必須設為 ON。 否則，陳述式便會失敗。  
  
 不支援 CHECK_POLICY = OFF 和 CHECK_EXPIRATION = ON 的結合。  
  
 當 CHECK_POLICY 設為 OFF， *lockout_time*會重設且 CHECK_EXPIRATION 會設為 OFF。  
  
> [!IMPORTANT]  
>  CHECK_EXPIRATION 和 CHECK_POLICY 只會在 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 和更新的版本中強制執行。 如需詳細資訊，請參閱＜ [Password Policy](../../relational-databases/security/password-policy.md)＞。  
  
 從憑證或非對稱金鑰建立的登入只能用於程式碼簽章。 它們不能用來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 僅當憑證或非對稱金鑰已存在於 master 時，您才能從憑證或非對稱金鑰中建立登入。  
  
 如需傳送登入的指令碼，請參閱 [如何在 SQL Server 2005 和 SQL Server 2008 的執行個體之間傳送登入和密碼](http://support.microsoft.com/kb/918992)。  
  
 建立登入會自動啟用新登入，並授與登入伺服器層級的 **CONNECT SQL** 權限。  
  
 如需設計權限系統的資訊，請參閱 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-and-includesssdwincludessssdw-mdmd-logins"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]登入  
 在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]、 **CREATE LOGIN**陳述式必須是唯一的陳述式批次中。  
  
 連接到的一些方法中[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，例如**sqlcmd**，您必須將附加[!INCLUDE[ssSDS](../../includes/sssds-md.md)]登入名稱使用的連接字串中的伺服器名稱*\<登入 >*@ *\<伺服器 >*標記法。 比方說，如果您的登入是`login1`和完整格式的名稱[!INCLUDE[ssSDS](../../includes/sssds-md.md)]伺服器`servername.database.windows.net`、 *username*的連接字串參數應該是`login1@servername`。 因為的總長度*username*參數為 128 個字元， *login_name*限制為 127 個字元減掉伺服器名稱的長度。 在此範例中，`login_name` 的長度只能是 117 個字元，因為 `servername` 為 10 個字元。  
  
 在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]您必須連接到 master 資料庫才能建立登入。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]規則可讓您建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證登入，格式\<loginname > @\<伺服器名稱 >。 如果您[!INCLUDE[ssSDS](../../includes/sssds-md.md)]伺服器**myazureserver**和您的登入是 **myemail@live.com** ，您必須提供做為登入 **myemail@live.com @myazureserver** .  
  
 在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]、 驗證連線所需的登入資料和伺服器層級防火牆規則中每個資料庫會暫時快取。 此快取會定期重新整理。 若要強制驗證快取重新整理，並請確定資料庫有登入資料表的最新版本，執行[DBCC FLUSHAUTHCACHE &#40;TRANSACT-SQL &#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
 如需有關[!INCLUDE[ssSDS](../../includes/sssds-md.md)]登入，請參閱[管理的資料庫和登入 Windows Azure SQL Database 中的](http://msdn.microsoft.com/library/ee336235.aspx)。  
  
## <a name="permissions"></a>Permissions  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，需要**ALTER ANY LOGIN**權限的伺服器或成員資格**securityadmin**固定的伺服器角色。  
  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，只有 master 資料庫中的伺服器層級主體登入 (由佈建程序所建立) 或 `loginmanager` 資料庫角色成員，才能建立新登入。  
  
 如果使用 **CREDENTIAL** 選項，則也需要伺服器的 **ALTER ANY CREDENTIAL** 權限。  
  
## <a name="next-steps"></a>後續步驟  
 之後建立的登入，登入可以連接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]或[!INCLUDE[ssSDS](../../includes/sssds-md.md)]只授與的權限，但**公用**角色。 請考慮執行下列其中一些活動。  
  
-   若要連接至資料庫，請建立用於登入的資料庫使用者。 如需詳細資訊，請參閱 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)。  
  
-   使用建立使用者定義伺服器角色[CREATE SERVER ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md). 使用 **ALTER SERVER ROLE** … **加入成員**將新的登入新增至使用者定義伺服器角色。 如需詳細資訊，請參閱[CREATE SERVER ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)和[更改伺服器角色 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
-   使用**sp_addsrvrolemember**来加入至固定的伺服器角色的登入。 如需詳細資訊，請參閱[伺服器層級角色](../../relational-databases/security/authentication-access/server-level-roles.md)和[sp_addsrvrolemember &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md).  
  
-   使用**GRANT**陳述式，以便授與新的登入或角色，包含登入的伺服器層級權限。 如需詳細資訊，請參閱 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)的相關資訊。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-login-with-a-password"></a>A. 建立具有密碼的登入  
 下列範例會針對特定的使用者建立登入，並指派密碼。  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-with-a-password"></a>B. 建立具有密碼的登入  
 下列範例會針對特定的使用者建立登入，並指派密碼。 `MUST_CHANGE` 選項需要使用者在第一次連接到伺服器時變更這個密碼。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>' MUST_CHANGE;  
GO  
```  
  
### <a name="c-creating-a-login-mapped-to-a-credential"></a>C. 建立對應到認證的登入  
 下列範例會針對特定使用者建立登入 (透過使用者)。 此登入會對應到認證。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>',   
    CREDENTIAL = <credentialName>;  
GO  
```  
  
### <a name="d-creating-a-login-from-a-certificate"></a>D. 從憑證建立登入  
 下列範例會從 master 的憑證建立特定使用者的登入。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE MASTER;  
CREATE CERTIFICATE <certificateName>  
    WITH SUBJECT = '<login_name> certificate in master database',  
    EXPIRY_DATE = '12/05/2025';  
GO  
CREATE LOGIN <login_name> FROM CERTIFICATE <certificateName>;  
GO  
```  
  
### <a name="e-creating-a-login-from-a-windows-domain-account"></a>E. 從 Windows 網域帳戶中建立登入  
 下列範例會從 Windows 網域帳戶建立登入。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE LOGIN [<domainName>\<login_name>] FROM WINDOWS;  
GO  
```  
  
### <a name="f-creating-a-login-from-a-sid"></a>F. 從 SID 建立登入  
 下列範例會先建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證登入並判斷登入的 SID。  
  
```  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 我的查詢會傳回 0x241C11948AEEB749B0D22646DB1A19F2 做為 SID。 您的查詢將傳回不同的值。 下列陳述式會刪除登入，並重新建立登入。 使用來自前一個查詢的 SID。  
  
```  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-creating-a-sql-server-authentication-login-with-a-password"></a>G. 建立具有密碼的 SQL Server 驗證登入  
 下列範例會建立登入`Mary7`密碼`A2c3456`。  
  
```tsql  
CREATE LOGIN Mary7 WITH PASSWORD = 'A2c3456$#' ;  
```  
  
### <a name="h-using-options"></a>H. 使用選項  
 下列範例會建立登入`Mary8`密碼和一些選擇性的引數。  
  
```  
CREATE LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
```  
  
### <a name="i-creating-a-login-from-a-windows-domain-account"></a>I. 從 Windows 網域帳戶中建立登入  
 下列範例會從名為 Windows 網域帳戶建立登入`Mary`中`Contoso`網域。  
  
```  
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [密碼原則](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [卸除登入 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [建立登入](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  

