---
title: 建立登入 | Microsoft 文件
description: 了解如何使用 SQL Server Management Studio 或 Transact-SQL 在 SQL Server 或 Azure SQL Database 中建立登入。
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.login.status.f1
- sql13.swb.login.effectivepermissions.f1
- sql13.swb.login.general.f1
- sql13.swb.login.databaseaccess.f1
- sql13.swb.login.serverroles.f1
helpviewer_keywords:
- authentication [SQL Server], logins
- logins [SQL Server], creating
- creating logins with Management Studio
- Create login [SQL Server]
- SQL Server logins
ms.assetid: fb163e47-1546-4682-abaa-8c9494e9ddc7
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 77b94fa9994a42dd11b6fa5a54fffd222e87feb2
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867448"
---
# <a name="create-a-login"></a>建立登入
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中建立登入。 登入是連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體的人員或程序的識別。  
  
##  <a name="background"></a><a name="Background"></a> 背景  
 登入是安全性主體或可由安全系統驗證的實體。 使用者需要登入才能連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 您可以建立以 Windows 主體為基礎的登入 (例如網域使用者或 Windows 網域群組)，也可以建立不是以 Windows 主體為基礎的登入 (例如 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入)。  
  
> **注意：** 若要使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證，[!INCLUDE[ssDE](../../../includes/ssde-md.md)] 必須使用混合模式驗證。 如需詳細資訊，請參閱 [選擇驗證模式](../../../relational-databases/security/choose-an-authentication-mode.md)。  
  
 登入做為安全性主體時，可以將權限授與登入。 登入的範圍是整個 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。 若要連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體上的特定資料庫，則登入必須對應到資料庫使用者。 資料庫內的權限是對資料庫使用者授與或拒絕，而不是登入。 範圍包含整個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的權限 (例如 **CREATE ENDPOINT** 權限) 可以授與登入。  
  
> **注意：** 當登入連線到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，身分識別會在 master 資料庫進行驗證。 使用自主資料庫使用者來驗證 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 資料庫層級的連線。 使用自主資料庫使用者時不需要登入。 「自主資料庫」(Contained Database) 是與其他資料庫和裝載資料庫的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]/ [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 執行個體 (以及 master 資料庫) 隔離的資料庫。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援 Windows 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的自主資料庫使用者。 當使用 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]時，結合自主資料庫使用者與資料庫層級防火牆規則。 如需詳細資訊，請參閱 [自主的資料庫使用者 - 使資料庫可攜](../../../relational-databases/security/contained-database-users-making-your-database-portable.md)。  
  
##  <a name="security"></a><a name="Security"></a> Security  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 需要伺服器的 **ALTER ANY LOGIN** 或 **ALTER LOGIN** 權限。  
  
 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 需要 **loginmanager** 角色的成員資格。  
  
##  <a name="create-a-login-using-ssms"></a><a name="SSMSProcedure"></a> 使用 SSMS 建立登入  
  
  
1.  在 [物件總管] 中，展開要建立新登入之伺服器執行個體的資料夾。  
  
2.  以滑鼠右鍵按一下 [安全性] 資料夾，指向 [新增]，然後選取 [登入...]。  
  
3.  在 [登入 - 新增] 對話方塊的 [一般] 頁面上，於 [登入名稱] 方塊中輸入使用者的名稱。 或者，按一下 [搜尋...] 開啟 [選取使用者或群組] 對話方塊。  
  
     如果您按一下 [搜尋...]：  
  
    1.  按一下 [選取此物件類型] 底下的 [物件類型...]，開啟 [物件類型] 對話方塊並選取下列任何一個或所有選項：[內建安全性主體]、[群組] 和 [使用者]。 預設會選取 [內建安全性主體] 和 [使用者]。 完成後，請按一下 **[確定]** 。  
  
    2.  按一下 [從這個位置] 下的 [位置..] 開啟 [位置] 對話方塊，然後選取其中一個可用的伺服器位置。 完成後，請按一下 **[確定]** 。  
  
    3.  在 [輸入要選取的物件名稱 (範例)] 底下，輸入要尋找的使用者或群組名稱。 如需詳細資訊，請參閱＜ [選擇使用者、電腦或群組對話方塊](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771712(v=ws.11))＞。  
  
    4.  如需其他進階搜尋選項，請按一下 [進階...]。 如需詳細資訊，請參閱 [選擇使用者、電腦或群組對話方塊 - 進階頁面](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc733110(v=ws.11))。  
  
    5.  按一下 [確定]。  
  
4.  若要建立以 Windows 主體為基礎的登入，請選取 **[Windows 驗證]** 。 這是預設選項。  
  
5.  若要建立儲存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫上的登入，請選取 **[SQL Server 驗證]** 。  
  
    1.  在 [密碼]  方塊中，輸入新使用者的密碼。 在 [確認密碼]  方塊中再次輸入密碼。  
  
    2.  變更現有密碼時，選取 **[指定舊密碼]** ，然後在 **[舊密碼]** 方塊中輸入舊密碼。  
  
    3.  若要強制執行複雜性和強制執行的密碼原則選項，請選取 **[強制執行密碼原則]** 。 如需詳細資訊，請參閱＜ [Password Policy](../../../relational-databases/security/password-policy.md)＞。 這是已選取 **[SQL Server 驗證]** 時的預設選項。  
  
    4.  若要強制執行逾期的密碼原則選項，請選取 **[強制執行密碼逾期]** 。 必須選取 **[強制執行密碼原則]** 才能啟用此核取方塊。 這是已選取 **[SQL Server 驗證]** 時的預設選項。  
  
    5.  若要強制使用者必須在第一次使用登入後建立新的密碼，請選取 **[使用者必須在下次登入時變更密碼]** 。 必須選取 **[強制執行密碼逾期]** 才能啟用此核取方塊。 這是已選取 **[SQL Server 驗證]** 時的預設選項。  
  
6.  若要將登入與獨立安全性憑證建立關聯，請選取 [已對應到憑證]，然後從清單中選取現有憑證的名稱。  
  
7.  若要將登入與獨立非對稱金鑰建立關聯，請選取 [已對應到非對稱金鑰]，然後從清單中選取現有金鑰的名稱。  
  
8.  若要將登入與安全性認證建立關聯，請選取 **[對應到認證]** 核取方塊，然後從清單中選取現有認證，或按一下 **[加入]** 建立新的認證。 若要從登入移除安全性認證的對應，請在 **[已對應的認證]** 中選取認證，然後按一下 **[移除]** 。 如需一般認證的詳細資訊，請參閱[認證 &#40;Database Engine&#41;](../../../relational-databases/security/authentication-access/credentials-database-engine.md)。  
  
9. 從 **[預設資料庫]** 清單中，為登入選取預設的資料庫。 **[Master]** 是此選項的預設值。  
  
10. 從 **[預設語言]** 清單中，為登入選取預設的語言。  
  
11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

### <a name="additional-options"></a>其他選項  
 [登入 - 新增] 對話方塊也在其他四個頁面上提供選項：[伺服器角色]、[使用者對應]、[安全性實體] 和 [狀態]。  
  
### <a name="server-roles"></a>[伺服器角色]  
 **[伺服器角色]** 頁面列出所有可指派給新登入的可能角色。 有下列選項可供使用：  
  
 [bulkadmin] 核取方塊  
 **bulkadmin** 固定伺服器角色的成員可以執行 BULK INSERT 陳述式。  
  
 [dbcreator] 核取方塊  
 **dbcreator** 固定伺服器角色的成員可以建立、改變、卸除及還原任何資料庫。  
  
 [diskadmin] 核取方塊  
 **diskadmin** 固定伺服器角色的成員可以管理磁碟檔案。  
  
 [processadmin] 核取方塊  
 **processadmin** 固定伺服器角色的成員可以結束在 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]執行個體中執行的處理序。  
  
 [public] 核取方塊  
 所有 SQL Server 使用者、群組和角色預設都屬於 **public** 固定伺服器角色。  
  
 [securityadmin] 核取方塊  
 **securityadmin** 固定伺服器角色的成員可以管理登入及其屬性。 他們可以 GRANT、DENY 及 REVOKE 伺服器層級權限。 他們也可以 GRANT、DENY 和 REVOKE 資料庫層級權限。 此外，他們可以重設 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入的密碼。  
  
 [serveradmin] 核取方塊  
 **serveradmin** 固定伺服器角色的成員可以變更全伺服器組態選項及關閉伺服器。  
  
 [setupadmin] 核取方塊  
 **setupadmin** 固定伺服器角色的成員可以加入和移除連結的伺服器，也可以執行一些系統預存程序。  
  
 [系統管理員] 核取方塊  
 **系統管理員** 固定伺服器角色的成員可以執行 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]中的所有活動。  
  
### <a name="user-mapping"></a>[使用者對應]  
 **[使用者對應]** 頁面列出所有可能的資料庫和這些資料庫上可套用至此登入的資料庫角色成員資格。 所選的資料庫決定可供登入使用的角色成員資格。 此頁面提供下列選項：  
  
 **已對應到此登入的使用者**  
 選取此登入可以存取的資料庫。 選取資料庫時，[資料庫角色成員資格對象: <資料庫名稱>] 窗格會顯示有效的資料庫角色。  
  
 **地圖**  
 允許登入存取下列資料庫。  
  
 **Database**  
 列出伺服器上可用的資料庫。  
  
 **使用者**  
 指定要對應至登入的資料庫使用者。 依預設，資料庫使用者與登入的名稱相同。  
  
 **預設結構描述**  
 指定使用者的預設結構描述。 使用者最初建立時，預設結構描述為 **dbo**。 可以指定不存在的預設結構描述。 您無法為使用者指定對應至 Windows 群組、憑證或非對稱金鑰的預設結構描述。  
  
 **已啟用 <資料庫名稱> 的來賓帳戶**  
 唯讀屬性，表示選取的資料庫上是否啟用 Guest 帳戶。 使用 Guest 帳戶之 **[登入屬性]** 對話方塊的 **[狀態]** 頁面，啟用或停用 Guest 帳戶。  
  
 **資料庫角色成員資格對象: <資料庫名稱>**   
 在指定的資料庫中選取使用者的角色。 在每一個資料庫中，所有使用者都是 **public** 角色的成員，且無法移除。 如需資料庫角色的詳細資訊，請參閱 [資料庫層級角色](../../../relational-databases/security/authentication-access/database-level-roles.md)。  
  
### <a name="securables"></a>安全性實體  
 **[安全性實體]** 頁面列出所有可能的安全性實體以及可授與登入的安全性實體權限。 此頁面提供下列選項：  
  
 **上方格**  
 包含一個或多個可以設定權限的項目。 顯示在上方格中的資料行會隨著主體或安全性實體而有所不同。  
  
 若要在上方格中加入項目：  
  
1.  按一下 **[搜尋]** 。  
  
2.  在 新增物件 對話方塊中，選取下列其中一個選項：特定物件...、下列類型的所有物件... 或 伺服器 _server\_name_。 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > **注意：** 選取 [伺服器 _server\_name_] 會使用該伺服器的所有安全物件自動填滿上層方格。  
  
3.  如果您選取 [特定物件...]：  
  
    1.  在 [選取物件] 對話方塊中，按一下 [選取下列物件類型] 下的 [物件類型...]。  
  
    2.  在 [選取物件類型] 對話方塊中，選取下列任何一個或所有物件類型：[端點]、[登入]、[伺服器]、[可用性群組] 和 [伺服器角色]。 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    3.  按一下 [輸入要選取的物件名稱 (範例)] 下的 [瀏覽...]。  
  
    4.  在 **[瀏覽物件]** 對話方塊中，選取您在 **[選取物件類型]** 對話方塊中所選物件類型的任何一項，然後按一下 **[確定]** 。  
  
    5.  在 **[選取物件]** 對話方塊中，按一下 **[確定]** 。  
  
4.  如果您選取 [下列類型的所有物件...]，請在 [選取物件類型] 對話方塊中，選取下列任何一個或所有物件類型：[端點]、[登入]、[伺服器]、[可用性群組] 和 [伺服器角色]。 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **名稱**  
 加入此方格的每一個主體或安全性實體名稱。  
  
 **型別**  
 描述每個項目的類型。  
  
 **明確索引標籤**  
 列出上方格中選取之安全性實體的可能權限。 並非所有選項都適用於所有明確權限。  
  
 **權限**  
 權限的名稱。  
  
 **授與者**  
 授與權限的主體。  
  
 **授與**  
 選取此選項即可授與此權限給登入。 清除此選項即可撤銷這個權限。  
  
 **使用授與**  
 反映出所列權限之 WITH GRANT 選項的狀態。 這個方塊是唯讀的。 若要套用此權限，請使用 [GRANT](../../../t-sql/statements/grant-transact-sql.md) 陳述式。  
  
 **拒絕**  
 選取此選項即可拒絕授與此權限給登入。 清除此選項即可撤銷這個權限。  
  
### <a name="status"></a>狀態  
 **[狀態]** 頁面列出可在所選取之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入上設定的一些驗證和授權選項。  
  
 此頁面提供下列選項：  
  
 **連接到 Database Engine 的權限**  
 使用這個設定時，應該將選取的登入視為可對其授與或拒絕安全性實體權限的主體。  
  
 選取 **[授與]** 可為登入授與 CONNECT SQL 權限。 選取 **[拒絕]** 則可以拒絕授與登入 CONNECT SQL 權限。  
  
 **登入**  
 使用這個設定時，應該將選取的登入視為資料表中的記錄。 對此處所列的值所做的變更會套用至記錄。  
  
 已經停用的登入會繼續以記錄形式存在。 但是如果登入嘗試連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，就無法對其進行驗證。  
  
 選取此選項可啟用或停用此登入。 此選項會搭配 ENABLE 或 DISABLE 選項來使用 ALTER LOGIN 陳述式。  
  
 **SQL Server 驗證**  
 只有在選取的登入使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證進行連接，而且登入已經鎖定時，[登入已經鎖定] 核取方塊才可使用。此設定是唯讀的。 若要解除鎖定已經鎖定的登入，請搭配 UNLOCK 選項執行 ALTER LOGIN。  
  
##  <a name="create-a-login-using-windows-authentication-using-t-sql"></a><a name="TsqlProcedure"></a> 透過 T-SQL 建立使用 Windows 驗證的登入  
  
 
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- Create a login for SQL Server by specifying a server name and a Windows domain account name.  
  
    CREATE LOGIN [<domainName>\<loginName>] FROM WINDOWS;  
    GO  
  
    ```  
  
## <a name="create-a-login-using-sql-server-authentication-using-t-sql"></a>透過 T-SQL 建立使用 SQL Server 驗證的登入
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- Creates the user "shcooper" for SQL Server using the security credential "RestrictedFaculty"   
    -- The user login starts with the password "Baz1nga," but that password must be changed after the first login.  
  
    CREATE LOGIN shcooper   
       WITH PASSWORD = 'Baz1nga' MUST_CHANGE,  
       CREDENTIAL = RestrictedFaculty;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)。  
  
##  <a name="follow-up-steps-to-take-after-you-create-a-login"></a><a name="FollowUp"></a> 後續操作：建立登入之後採取的步驟  
 建立登入之後，登入就可以連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，但是不一定有足夠的權限可以執行任何實際工作。 下列清單提供常用登入動作的連結。  
  
-   若要讓登入加入角色，請參閱 [加入角色](../../../relational-databases/security/authentication-access/join-a-role.md)。  
  
-   若要授權登入使用資料庫，請參閱 [建立資料庫使用者](../../../relational-databases/security/authentication-access/create-a-database-user.md)。  
  
-   若要將權限授與登入，請參閱 [為主體授與權限](../../../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
