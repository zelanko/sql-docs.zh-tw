---
title: 針對自主資料庫的自主使用者存取
description: 了解如何針對自主資料庫設定自主使用者存取，以及與傳統的登入/使用者模型之間的差異。
ms.custom: seo-lt-2019
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- contained database, users
- user [SQL Server], about contained database users
ms.assetid: e57519bb-e7f4-459b-ba2f-fd42865ca91d
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b11a263953e0b58c4b3dc7072662b291f3d215ab
ms.sourcegitcommit: 6e7696a169876eb914f79706d022451a1213eb6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2020
ms.locfileid: "79375505"
---
# <a name="contained-database-users---making-your-database-portable"></a>自主的資料庫使用者 - 使資料庫可攜

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  使用自主資料庫使用者來驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 資料庫層級的連線。 「自主資料庫」(Contained Database) 是與其他資料庫和裝載資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體 (以及 master 資料庫) 隔離的資料庫。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Windows 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的自主資料庫使用者。 當使用 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]時，結合自主資料庫使用者與資料庫層級防火牆規則。 這個主題會檢閱使用自主資料庫模型時，相較於傳統的登入/使用者模型和 Windows 或伺服器層級防火牆規則的差異與優點。 特定的情況下，管理能力或應用程式商務邏輯可能仍然需要使用傳統的登入/使用者模型和伺服器層級防火牆規則。  
  
> [!NOTE]  
> 做為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 發展 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服務和移往較高保證的 Sla，您可能需要切換到自主的資料庫使用者模型和資料庫範圍的防火牆規則，以便對於給定的資料庫，達到更高的可用性 SLA 和更高的最大登入速率。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您立即考慮這類變更。  
  
## <a name="traditional-login-and-user-model"></a>傳統的登入和使用者模型

 在傳統的連線模型中，Windows 使用者或 Windows 群組的成員會藉由提供由 Windows 驗證的使用者或群組認證連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。 或者您可以提供名稱和密碼，並使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接。 在這兩種情況下，master 資料庫的登入必須符合連接的認證。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 確認 Windows 驗證認證或驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證認證之後，連接通常會嘗試連接至使用者資料庫。 若要連接至使用者資料庫，登入必須能夠對應到 (也就是相關聯) 使用者資料庫中的資料庫使用者。 連接字串也可以指定連接至在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中為選擇性但在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中為必要的特定資料庫。  
  
 最重要的原則是登入 (在 master 資料庫中) 和使用者 (在使用者資料庫中) 必須存在，且彼此相關。 這表示使用者資料庫的連接在登入 master 資料庫時有相依性，而且這會限制資料庫移到不同的裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 伺服器的能力。 如果由於任何原因，master 資料庫的連接無法使用 (例如，容錯移轉進行中)，就會增加整體的連接時間或連接可能會逾時。因此，這可能會降低連接延展性。  
  
## <a name="contained-database-user-model"></a>自主的資料庫使用者模型

 在自主的資料庫使用者模型中，master 資料庫中的登入不存在。 相反地，使用者資料庫中就會發生驗證程序，而且使用者資料庫中的資料庫使用者在 master 資料庫中沒有相關聯的登入。 自主資料庫使用者模型支援 Windows 驗證和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]兩者中使用。 若要以自主資料庫使用者身分連接，連接字串必須永遠包含使用者資料庫的參數，讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 知道哪一個資料庫負責管理驗證程序。 自主資料庫使用者的活動僅限於驗證資料庫，因此，當以自主資料庫使用者身分連接時，必須在使用者所需的每個資料庫中獨立建立資料庫使用者帳戶。 若要變更資料庫， [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 使用者必須建立新的連接。 如果另一個資料庫中有相同的使用者， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的自主資料庫使用者可以變更資料庫。  
  
**Azure：** [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 和 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]支援以 Azure Active Directory 身分識別作為自主資料庫使用者。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 支援使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 驗證的自主資料庫使用者，但 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 則不支援。 如需詳細資訊，請參閱[使用 Azure Active Directory 驗證連線到 SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 使用 Azure Active Directory 驗證時，可以使用 Active Directory 通用驗證建立來自 SSMS 的連接。  系統管理員可以將通用驗證設定為需要 Multi-Factor Authentication，以透過撥打電話、簡訊、智慧卡和 PIN 碼或	行動裝置應用程式通知，來驗證身分識別。 如需詳細資訊，請參閱 [適用於與 SQL Database 和 SQL 資料倉儲搭配使用之 Azure AD MFA 的 SSMS 支援](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)。  
  
 針對 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 和 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]，由於連接字串中一律要有資料庫名稱，因此從傳統模式切換至自主資料庫使用者模型時，不需要對連接字串進行變更。 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接，資料庫的名稱必須加入至連接字串 (如果尚不存在)。  
  
> [!IMPORTANT]  
> 使用傳統的模型時，伺服器層級角色和伺服器層級權限可以限制對所有資料庫的存取。 使用自主資料庫模型時，具有 ALTER ANY USER 權限的資料庫擁有者和資料庫使用者可以授與資料庫的存取權。 這可減少高特殊權限的伺服器登入的存取控制，並擴大要包含高特殊權限的資料庫使用者的存取控制。  
  
## <a name="firewalls"></a>防火牆  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

 Windows 防火牆規則適用所有連線，並對登入 (傳統模型連線) 與自主資料庫使用者具備相同的效果。 如需 Windows 防火牆的詳細資訊，請參閱＜ [設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)＞。  
  
### <a name="sssds-firewalls"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 防火牆

 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 允許對伺服器層級連線 (登入) 和資料庫層級連線 (自主資料庫使用者) 使用不同的防火牆規則。 連接到使用者資料庫時，會檢查第一個資料庫的防火牆規則。 如果沒有允許存取資料庫的規則，就會檢查伺服器層級防火牆規則，其需要存取 SQL Database 伺服器的 master 資料庫。 結合自主資料庫使用者的資料庫層級防火牆規則，不必在連線期間存取伺服器的 master 資料庫，藉此提供改善的連線延展性。  
  
 如需 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 防火牆規則的詳細資訊，請參閱下列主題：  
  
- [Azure SQL Database 防火牆](https://msdn.microsoft.com/library/azure/ee621782.aspx)  
- [操作說明：設定防火牆設定 (Azure SQL Database)](https://msdn.microsoft.com/library/azure/jj553530.aspx)  
- [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
- [sp_set_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
  
## <a name="syntax-differences"></a>語法差異  
  
|傳統的模型|自主的資料庫使用者模型|  
|-----------------------|-----------------------------------|  
|當連接到 master 資料庫：<br /><br /> `CREATE LOGIN login_name  WITH PASSWORD = 'strong_password';`<br /><br /> 然後，連接至使用者資料庫時：<br /><br /> `CREATE USER 'user_name' FOR LOGIN 'login_name';`|當連接至使用者資料庫：<br /><br /> `CREATE USER user_name  WITH PASSWORD = 'strong_password';`|  
  
|傳統的模型|自主的資料庫使用者模型|  
|-----------------------|-----------------------------------|  
|若要變更密碼，在 master 資料庫的內容中：<br /><br /> `ALTER LOGIN login_name  WITH PASSWORD = 'strong_password';`|若要變更密碼，在使用者資料庫的內容中：<br /><br /> `ALTER USER user_name  WITH PASSWORD = 'strong_password';`|  

### <a name="managed-instance"></a>受控執行個體

Azure SQL Database 受控執行個體的運作方式，類似於自主資料庫內容中的內部部署 SQL Server。 建立包含的使用者時，請務必將資料庫的內容從 master 資料庫變更為使用者資料庫。 此外，設定內含項目選項時，使用者資料庫不應有使用中的連線。 

例如： 

```sql
Use MASTER;
GO 

ALTER DATABASE Test
SET containment=partial


USE Test;  
GO  
CREATE USER Carlo  
WITH PASSWORD='Enterpwdhere*'  


SELECT containment_desc FROM sys.databases
WHERE name='test'
```

  
## <a name="remarks"></a>備註  
  
- 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，必須對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體啟用自主資料庫使用者。 如需詳細資訊，請參閱[自主資料庫驗證伺服器組態選項](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)。  
- 自主的資料庫使用者與登入具有非重疊的名稱，可以共存於您的應用程式。  
- 若以 **name1** 名稱在 master 資料庫中登入，並且您建立了名為 **name1**的自主資料庫使用者，當連接字串中提供資料庫名稱時，連接到資料庫時會優先挑選資料庫使用者的內容，而非登入內容。 也就是說，自主資料庫使用者的優先順序將高於具有相同名稱的登入。  
- 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，自主的資料庫使用者名稱不能同於伺服器系統管理員帳戶的名稱。  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器系統管理員帳戶不可以是自主的資料庫使用者。 伺服器管理員有足夠的權限來建立及管理自主的資料庫使用者。 伺服器管理員可以授與權限給使用者資料庫上的自主資料庫使用者。  
- 因為自主資料庫使用者是資料庫層級主體，所以您必須在每個您想要使用的資料庫，建立自主的資料庫使用者。 身分識別會侷限於資料庫，並且在所有層面都獨立於在相同伺服器中的另一個資料庫具有相同名稱和相同密碼的使用者。  
- 使用您通常會用來登入的相同強度密碼。  
  
## <a name="see-also"></a>另請參閱

 [自主資料庫](../../relational-databases/databases/contained-databases.md)   
 [自主資料庫的安全性最佳做法](../../relational-databases/databases/security-best-practices-with-contained-databases.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)  
  
