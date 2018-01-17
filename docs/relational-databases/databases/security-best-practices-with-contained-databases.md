---
title: "自主資料庫的安全性最佳做法 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: contained database, threats
ms.assetid: 026ca5fc-95da-46b6-b882-fa20f765b51d
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 612ee0b5301554b2a078493ed2df419d992b4391
ms.sourcegitcommit: d28d9e3413b6fab26599966112117d45ec2c7045
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/11/2018
---
# <a name="security-best-practices-with-contained-databases"></a>自主資料庫的安全性最佳做法
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  自主資料庫具有一些 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 系統管理員應該了解並降低的獨特威脅。 其中大部分威脅都與 **USER WITH PASSWORD** 驗證處理序相關，而這個處理序會將驗證界限從 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 層級移至資料庫層級。  
  
## <a name="threats-related-to-users"></a>與使用者相關的威脅  
 在自主資料庫中，擁有 **ALTER ANY USER** 權限的使用者 (例如 **db_owner** 和 **db_securityadmin** 固定資料庫角色的成員) 可以在未經 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員認可或允許的情況下授與資料庫的存取權。 將自主資料庫的存取權授與使用者會針對整個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體增加潛在的攻擊面區域。 系統管理員應該了解此存取控制的委派，並且非常謹慎地將 **ALTER ANY USER** 權限授與自主資料庫中的使用者。 所有資料庫擁有者都擁有 **ALTER ANY USER** 權限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員應定期稽核自主資料庫中的使用者。  
  
### <a name="accessing-other-databases-using-the-guest-account"></a>使用 Guest 帳戶來存取其他資料庫  
 擁有 **ALTER ANY USER** 權限的資料庫擁有者與資料庫使用者可以建立自主資料庫使用者。 連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上之自主資料庫之後，如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)]上的其他資料庫已啟用 **Guest** 帳戶，自主資料庫使用者就可以存取其他資料庫。  
  
### <a name="creating-a-duplicate-user-in-another-database"></a>在另一個資料庫中建立重複的使用者  
 某些應用程式可能會要求使用者擁有多個資料庫的存取權。 只要在每個資料庫中建立相同的自主資料庫使用者，即可完成此作業。 建立第二位使用者與密碼時，請使用 SID 選項。 下列範例會在兩個資料庫中建立兩位相同的使用者。  
  
```  
USE DB1;  
GO  
CREATE USER Carlo WITH PASSWORD = '<strong password>';   
-- Return the SID of the user  
SELECT SID FROM sys.database_principals WHERE name = 'Carlo';  
  
-- Change to the second database  
USE DB2;  
GO  
CREATE USER Carlo WITH PASSWORD = '<same password>', SID = <SID from DB1>;  
GO  
```  
  
 若要執行跨資料庫查詢，您必須針對呼叫的資料庫設定 **TRUSTWORTHY** 選項。 例如，如果上述定義的使用者 (Carlo) 位於 DB1 中，為了執行 `SELECT * FROM db2.dbo.Table1;` ，則必須開啟資料庫 DB1 的 **TRUSTWORTHY** 設定。 請執行下列程式碼，將 **TRUSTWORTHY** 設定設為開啟。  
  
```  
ALTER DATABASE DB1 SET TRUSTWORTHY ON;  
```  
  
### <a name="creating-a-user-that-duplicates-a-login"></a>建立重複登入的使用者  
 如果您使用與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入相同的名稱來建立具有密碼之自主資料庫使用者，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入連接時指定自主資料庫做為初始目錄，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入將無法連接。 系統會將此連接評估為自主資料庫上具有密碼主體之自主資料庫使用者，而不是以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入為基礎的使用者。 這可能會導致系統蓄意或意外阻斷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的服務。  
  
-   最佳作法是系統管理員 ( **sysadmin** ) 固定伺服器角色的成員應該考慮永遠不使用初始目錄選項來連接。 這樣會將登入連接至 master 資料庫，並且避免資料庫擁有者濫用登入嘗試的任何嘗試行為。 然後，系統管理員就可以使用 **USE***\<資料庫>* 陳述式來變更為自主資料庫。 此外，您也可以將登入的預設資料庫設定為自主資料庫，以便完成登入 **master**的作業，然後將登入傳送至自主資料庫。  
  
-   最佳作法是不要使用具有密碼且與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入具有相同名稱之自主資料庫使用者。  
  
-   如果存在重複的登入，請連接至 **master** 資料庫而不指定初始目錄，然後執行 **USE** 命令來變更為自主資料庫。  
  
-   當自主資料庫存在時，非自主資料庫的資料庫使用者應該連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 而不使用初始目錄，或指定非自主資料庫的資料庫名稱做為初始目錄。 這樣可避免連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 系統管理員直接控制權較低之自主資料庫。  
  
### <a name="increasing-access-by-changing-the-containment-status-of-a-database"></a>變更資料庫的內含項目狀態來提高存取權  
 擁有 **ALTER ANY DATABASE** 權限的登入 (例如 **dbcreator** 固定伺服器角色的成員) 以及非自主資料庫中擁有 **CONTROL DATABASE** 權限的使用者 (例如 **db_owner** 固定資料庫角色的成員) 都可以變更資料庫的內含項目設定。 如果資料庫的內含項目設定從 **NONE** 變更為 **PARTIAL** 或 **FULL**，您就可以透過建立具有密碼之自主資料庫使用者，授與使用者存取權。 這樣可能會在未經 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員認可或同意的情況下提供存取權。 若要防止包含任何資料庫，請將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [自主資料庫驗證] 選項設為 0。 若要針對選取之自主資料庫防止具有密碼之自主資料庫使用者連接，請使用登入觸發程序來取消具有密碼之自主資料庫使用者所進行的登入嘗試。  
  
### <a name="attaching-a-contained-database"></a>附加自主資料庫  
 透過附加自主資料庫，系統管理員可能會將 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體的存取權提供給不想要的使用者。 擔心這項風險的系統管理員可以在 **RESTRICTED_USER** 模式下讓資料庫上線，以便防止系統驗證具有密碼之自主資料庫使用者。 此時，只有透過登入授權的主體才能存取 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
 建立使用者時所使用的密碼需求會在建立時生效，而且系統不會在附加資料庫時重新檢查密碼。 透過將允許弱式密碼之自主資料庫附加至密碼原則更嚴格的系統，系統管理員可能會允許不符合附加 [!INCLUDE[ssDE](../../includes/ssde-md.md)]之目前密碼原則的密碼。 系統管理員可以要求針對附加的資料庫重設所有密碼，藉以避免保留弱式密碼。  
  
### <a name="password-policies"></a>密碼原則  
 資料庫中的密碼可能必須是強式密碼，但不受強固的密碼原則所保護。 若要運用 Windows 所提供的更廣泛密碼原則，請盡可能使用 Windows 驗證。  
  
### <a name="kerberos-authentication"></a>Kerberos 驗證  
 具有密碼之自主資料庫使用者無法使用 Kerberos 驗證。 請盡可能使用 Windows 驗證來運用 Kerberos 等 Windows 功能。  
  
### <a name="offline-dictionary-attack"></a>離線字典攻擊  
 具有密碼之自主資料庫使用者的密碼雜湊會儲存在自主資料庫中。 擁有資料庫檔案之存取權的任何人都可以針對未稽核系統上具有密碼之自主資料庫使用者執行字典攻擊。 若要降低這項威脅，請限制資料庫檔案的存取權，或是只允許使用 Windows 驗證來連接至自主資料庫。  
  
## <a name="escaping-a-contained-database"></a>逸出自主資料庫  
 如果資料庫處於部分自主狀態， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員就應該定期稽核自主資料庫中使用者和模組的功能。  
  
## <a name="denial-of-service-through-autoclose"></a>透過 AUTO_CLOSE 阻斷服務  
 請勿將自主資料庫設定為自動關閉。 如果已關閉，開啟資料庫來驗證使用者會耗用額外的資源，而且可能會導致阻斷服務攻擊。  
  
## <a name="see-also"></a>另請參閱  
 [自主資料庫](../../relational-databases/databases/contained-databases.md)   
 [移轉至部分自主資料庫](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)  
  
  
