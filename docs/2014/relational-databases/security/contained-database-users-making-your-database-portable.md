---
title: 自主資料庫使用者 - 使資料庫可攜 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- contained database, users
- user [SQL Server], about contained database users
ms.assetid: e57519bb-e7f4-459b-ba2f-fd42865ca91d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a10f892c8fd635892d76061e9f33649340e69593
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62655471"
---
# <a name="contained-database-users---making-your-database-portable"></a>自主資料庫使用者 - 讓資料庫具有可攜性
  使用自主資料庫使用者來驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 資料庫層級的連線。 「自主資料庫」(Contained Database) 是與其他資料庫和裝載資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體 (以及 master 資料庫) 隔離的資料庫。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Windows 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的自主資料庫使用者。 當使用 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]時，結合自主資料庫使用者與資料庫層級防火牆規則。 這個主題會檢閱使用自主資料庫模型時，相較於傳統的登入/使用者模型和 Windows 或伺服器層級防火牆規則的差異與優點。 特定的情況下，管理能力或應用程式商務邏輯可能仍然需要使用傳統的登入/使用者模型和伺服器層級防火牆規則。  
  
> [!NOTE]  
>  做為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 發展 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服務和移往較高保證的 Sla，您可能需要切換到自主的資料庫使用者模型和資料庫範圍的防火牆規則，以便對於給定的資料庫，達到更高的可用性 SLA 和更高的最大登入速率。 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您立即考慮這類變更。  
  
## <a name="traditional-login-and-user-model"></a>傳統的登入和使用者模型  
 在傳統的連線模型中，Windows 使用者或 Windows 群組的成員會藉由提供由 Windows 驗證的使用者或群組認證連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。 或連線同時提供名稱和密碼，且使用連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連線 (連線到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]時這是唯一的選項)。 在這兩種情況下，master 資料庫的登入必須符合連接的認證。 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 確認 Windows 驗證認證或驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證認證之後，連接通常會嘗試連接至使用者資料庫。 若要連接至使用者資料庫，登入必須能夠對應到 (也就是相關聯) 使用者資料庫中的資料庫使用者。 連接字串也可以指定連接至在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中為選擇性但在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中為必要的特定資料庫。  
  
 最重要的原則是登入 (在 master 資料庫中) 和使用者 (在使用者資料庫中) 必須存在，且彼此相關。 這表示使用者資料庫的連接在登入 master 資料庫時有相依性，而且這會限制資料庫移到不同的裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 伺服器的能力。 而且，如果因為任何原因而無法使用 master 資料庫的連接（例如，容錯移轉正在進行中），整體連線時間將會增加，或連接可能會超時。因此，這可能會減少連接的擴充性。  
  
## <a name="contained-database-user-model"></a>自主的資料庫使用者模型  
 在自主的資料庫使用者模型中，master 資料庫中的登入不存在。 相反地，使用者資料庫中就會發生驗證程序，而且使用者資料庫中的資料庫使用者在 master 資料庫中沒有相關聯的登入。 自主的資料庫使用者模型支援 Windows 驗證 (在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中) 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證 (在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]兩者中)。 若要以自主資料庫使用者身分連接，連接字串必須永遠包含使用者資料庫的參數，讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 知道哪一個資料庫負責管理驗證程序。 自主資料庫使用者的活動僅限於驗證資料庫，因此，當以自主資料庫使用者身分連接時，必須在使用者所需的每個資料庫中獨立建立資料庫使用者帳戶。 若要變更資料庫， [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 使用者必須建立新的連接。 如果另一個資料庫中有相同的使用者， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的自主資料庫使用者可以變更資料庫。  
  
 針對 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，從傳統模式切換至自主的資料庫使用者模型時，不需要對連接字串進行變更。 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接，資料庫的名稱必須加入至連接字串 (如果尚不存在)。  
  
> [!IMPORTANT]  
>  使用傳統的模型時，伺服器層級角色和伺服器層級權限可以限制對所有資料庫的存取。 使用自主資料庫模型時，具有 ALTER ANY USER 權限的資料庫擁有者和資料庫使用者可以授與資料庫的存取權。 這可減少高特殊權限的伺服器登入的存取控制，並擴大要包含高特殊權限的資料庫使用者的存取控制。  
  
## <a name="firewalls"></a>防火牆  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Windows 防火牆規則適用所有連線，並對登入 (傳統模型連線) 與自主資料庫使用者具備相同的效果。 如需 Windows 防火牆的詳細資訊，請參閱＜ [Configure a Windows Firewall for Database Engine Access](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)＞。  
  
### <a name="includesssdsincludessssds-mdmd-firewalls"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)]道  
 
  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 允許對伺服器層級連線 (登入) 和資料庫層級連線 (自主資料庫使用者) 使用不同的防火牆規則。 連接到使用者資料庫時，會檢查第一個資料庫的防火牆規則。 如果沒有允許存取資料庫的規則，就會勾選伺服器層級防火牆規則，它需要存取邏輯伺服器的 master 資料庫。 結合自主資料庫使用者的資料庫層級防火牆規則，不必在連線期間存取伺服器的 master 資料庫，藉此提供改善的連線延展性。  
  
 如需 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 防火牆規則的詳細資訊，請參閱下列主題：  
  
-   [Azure SQL Database 防火牆](https://msdn.microsoft.com/library/azure/ee621782.aspx)  
  
-   [如何：設定防火牆設定（Azure SQL Database）](https://msdn.microsoft.com/library/azure/jj553530.aspx)  
  
-   [sp_set_firewall_rule &#40;Azure SQL Database&#41;](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
-   [sp_set_database_firewall_rule &#40;Azure SQL Database&#41;](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
## <a name="syntax-differences"></a>語法差異  
  
|傳統的模型|自主的資料庫使用者模型|  
|-----------------------|-----------------------------------|  
|當連接到 master 資料庫：<br /><br /> `CREATE LOGIN login_name  WITH PASSWORD = 'strong_password';`<br /><br /> 然後，連接至使用者資料庫時：<br /><br /> `CREATE USER 'user_name' FOR LOGIN 'login_name';`|當連接至使用者資料庫：<br /><br /> `CREATE USER user_name  WITH PASSWORD = 'strong_password';`|  
  
|傳統的模型|自主的資料庫使用者模型|  
|-----------------------|-----------------------------------|  
|若要變更密碼，在 master 資料庫的內容中：<br /><br /> `ALTER LOGIN login_name  WITH PASSWORD = 'strong_password';`|若要變更密碼，在使用者資料庫的內容中：<br /><br /> `ALTER USER user_name  WITH PASSWORD = 'strong_password';`|  
  
## <a name="remarks"></a>備註  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，必須對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體啟用自主資料庫使用者。 如需詳細資訊，請參閱[自主資料庫驗證伺服器組態選項](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)。  
  
-   自主的資料庫使用者與登入具有非重疊的名稱，可以共存於您的應用程式。  
  
-   若以 **name1** 名稱在 master 資料庫中登入，並且您建立了名為 **name1**的自主資料庫使用者，當連接字串中提供資料庫名稱時，連接到資料庫時會優先挑選資料庫使用者的內容，而非登入內容。 也就是說，自主資料庫使用者的優先順序將高於具有相同名稱的登入。  
  
-   在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，自主的資料庫使用者名稱不能同於伺服器系統管理員帳戶的名稱。  
  
-   
  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器系統管理員帳戶不可以是自主的資料庫使用者。 伺服器管理員有足夠的權限來建立及管理自主的資料庫使用者。 伺服器管理員可以授與權限給使用者資料庫上的自主資料庫使用者。  
  
-   因為自主資料庫使用者是資料庫層級主體，所以您必須在每個您想要使用的資料庫，建立自主的資料庫使用者。 身分識別會侷限於資料庫，並且在所有層面都獨立於在相同伺服器中的另一個資料庫具有相同名稱和相同密碼的使用者。  
  
-   使用您通常會用來登入的相同強度密碼。  
  
## <a name="see-also"></a>另請參閱  
 [自主資料庫](../databases/contained-databases.md)   
 [自主資料庫的安全性最佳做法](../databases/security-best-practices-with-contained-databases.md)   
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
  
