---
title: Linux 上的 SQL Server 安全性入門
description: 逐步解說 Linux 上的 SQL Server 安全性功能，以了解需進一步研究的領域。
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 031005dcb6a5353e9e4f0b73a7a45d667d2212e7
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088796"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Linux 上的 SQL Server 安全性功能逐步解說

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

如果您是剛開始使用 SQL Server 的 Linux 使用者，下列工作將逐步解說其中一些安全性工作。 這不是 Linux 唯一或特定功能，但可協助您大致了解哪些區域需要進一步調查。 在每個範例中，會提供該區域的深入文件連結。

> [!NOTE]
>  下列範例使用 **AdventureWorks 2014** 範例資料庫。 如需如何取得和安裝此範例資料庫的指示，請參閱[將 SQL Server 資料庫從 Windows 還原到 Linux](sql-server-linux-migrate-restore-database.md)。


## <a name="create-a-login-and-a-database-user"></a>建立登入和資料庫使用者 

使用 [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) 陳述式，在 master 資料庫中建立登入，以將 SQL Server 的存取權授與其他人。 例如：

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  請一律使用強式密碼來取代上一個命令中的星號。

登入可以連線到 SQL Server 且可以存取 (權限受限) master 資料庫。 若要連線到使用者資料庫，登入需要資料庫層級的對應識別，稱為資料庫使用者。 使用者特定於每個資料庫，且必須在每個資料庫中個別建立，才能授與其存取權。 下列範例會將您移至 AdventureWorks2014 資料庫，然後使用 [CREATE USER](../t-sql/statements/create-user-transact-sql.md) 陳述式來建立名為 Larry 的使用者，其與名為 Larry 的登入建立關聯。 雖然登入和使用者相互關聯 (彼此對應)，但它們是不同的物件。 登入是伺服器層級的主體。 使用者是資料庫層級的主體。

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- SQL Server 的系統管理員帳戶可以連線到任何資料庫，且可以在任何資料庫中建立更多登入和使用者。  
- 當有人建立資料庫時，他們就會成為資料庫擁有者，因而可以連線到該資料庫。 資料庫擁有者可以建立更多的使用者。

稍後，您可以授權其他登入，藉由授與其 `ALTER ANY LOGIN` 權限來建立更多登入。 在資料庫內，您可以授權其他使用者，藉由授與其 `ALTER ANY USER` 權限來建立更多使用者。 例如：   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

現在登入 Larry 可以建立更多登入，而使用者 Jerry 可以建立更多使用者。


## <a name="granting-access-with-least-privileges"></a>以最低權限授與存取權

第一個連線到使用者資料庫的人員，將會是系統管理員和資料庫擁有者帳戶。 不過，這些使用者擁有資料庫上所有可用權限。 這比大部分使用者擁有更多的權限。 

當您剛開始使用時，可以使用內建的「固定資料庫角色」來指派一些一般的權限類別。 例如，`db_datareader` 固定資料庫角色可以讀取資料庫中的所有資料表，但不會進行任何變更。 請使用 [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) 陳述式來授與固定資料庫角色中的成員資格。 下列範例會將使用者 `Jerry` 新增至 `db_datareader` 固定資料庫角色。   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

如需固定資料庫角色的清單，請參閱[資料庫層級角色](../relational-databases/security/authentication-access/database-level-roles.md)。

之後，當您準備好設定更精確的資料存取 (強烈建議) 時，請使用 [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) 陳述式來建立您自己的使用者定義資料庫角色。 然後，將特定的細微權限指派給您的自訂角色。

例如，下列陳述式會建立名為 `Sales` 的資料庫角色，授與 `Sales` 群組從 `Orders` 資料表查看、更新及刪除資料列的能力，然後將使用者 `Jerry` 新增至該 `Sales` 角色。   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```

如需權限系統的詳細資訊，請參閱[資料庫引擎權限使用者入門](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。


## <a name="configure-row-level-security"></a>設定資料列層級安全性  

[資料列層級安全性](../relational-databases/security/row-level-security.md)可讓您根據執行查詢的使用者，限制對資料庫中資料列的存取。 此功能適用於確保客戶只能存取自己的資料，或背景工作角色只能存取其部門相關資料的情況。   

下列步驟將逐步解說如何設定兩個對 `Sales.SalesOrderHeader` 資料表具有不同資料列層級存取權的使用者。 

建立兩個使用者帳戶來測試資料列層級安全性：    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```

將 `Sales.SalesOrderHeader` 資料表的讀取權限授與這兩個使用者：    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;
```
   
建立新的結構描述，以及內嵌資料表值函式。 `SalesPersonID` 資料行中的資料列符合 `SalesPerson` 登入的識別碼，或執行查詢的使用者是管理員使用者時，此函數會傳回 1。   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```

建立安全性原則，同時將函式新增為資料表上的篩選述詞和區塊述詞：  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

執行下列動作，以每個使用者的身分查詢 `SalesOrderHeader` 資料表。 確認 `SalesPerson280` 只會看到其本身銷售額的 95 個資料列，且 `Manager` 可以查看資料表中的所有資料列。  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
變更安全性原則，以停用原則。  現在這兩個使用者都可以存取所有資料列。 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>啟用動態資料遮罩

[動態資料遮罩](../relational-databases/security/dynamic-data-masking.md)可讓您藉由完整或部分遮罩特定資料行，限制敏感性資料對應用程式使用者的曝光程度。 

使用 `ALTER TABLE` 陳述式，將遮罩函式新增至 `Person.EmailAddress` 資料表中的 `EmailAddress` 資料行： 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
建立具有資料表 `SELECT` 權限的新使用者 `TestUser`，然後以 `TestUser` 的形式執行查詢，以檢視已遮罩的資料：   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
確認遮罩函式會從下列位置變更第一筆記錄中的電子郵件地址：
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>啟用透明資料加密

對資料庫的威脅之一，就是有人會從您的硬碟竊取資料庫檔案的風險。 當入侵透過問題員工的動作，或是透過竊取包含檔案的電腦 (例如膝上型電腦) 而取得系統更高權限的存取權，就可能發生這種情況。

透明資料加密 (TDE) 會加密儲存在硬碟上的資料檔案。 SQL Server 資料庫引擎的 master 資料庫具有加密金鑰，因此資料庫引擎可以操作資料。 需要存取金鑰才可讀取資料庫檔案。 高層級的管理員可以管理、備份及重新建立金鑰，因此可以移動資料庫，但只能由所選人員移動。 設定 TDE 時，也會自動加密 `tempdb` 資料庫。 

由於資料庫引擎可以讀取資料，透明資料加密無法保護可直接讀取記憶體或透過管理員帳戶存取 SQL Server 之電腦管理員進行未經授權的存取。

### <a name="configure-tde"></a>設定 TDE

- 建立主要金鑰
- 建立或取得受到主要金鑰保護的憑證
- 建立資料庫加密金鑰，並使用憑證保護它
- 設定資料庫使用加密

設定 TDE 需要 master 資料庫的 `CONTROL` 權限，以及使用者資料庫的 `CONTROL` 權限。 通常管理員會設定 TDE。 

下列範例說明如何使用 `AdventureWorks2014` 伺服器上安裝的憑證來加密和解密 `MyServerCert`資料庫。


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;  
GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

若要移除 TDE，請執行 `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

SQL Server 會將加密和解密作業排定在背景執行緒上。 您可以使用本主題稍後出現之清單內的目錄檢視和動態管理檢視，以檢視這些作業的狀態。   

> [!WARNING]
>  啟用了 TDE 的資料庫備份檔案也會使用資料庫加密金鑰來加密。 因此，當您要還原這些備份時，保護資料庫加密金鑰的憑證必須可以使用。 這表示，除了備份資料庫以外，您也必須確定可維護伺服器憑證的備份，以免資料遺失。 如果此憑證無法再使用，就會造成資料遺失。 如需詳細資訊，請參閱 [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  

如需 TDE 的詳細資訊，請參閱[透明資料加密 (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md)。   


## <a name="configure-backup-encryption"></a>設定備份加密
SQL Server 可在建立備份時加密資料。 在建立備份時透過指定加密演算法及加密程式 (憑證或非對稱金鑰)，即可建立加密的備份檔案。    
  
> [!WARNING]
> 備份憑證或非對稱金鑰是非常重要的，而且最好與其用以加密的備份檔案存放於不同位置。 若沒有憑證或非對稱金鑰，您將無法還原備份，而此備份檔案將無法使用。 
 
 
下列範例會建立憑證，然後建立受該憑證保護的備份。

```
USE master;  
GO  
CREATE CERTIFICATE BackupEncryptCert   
   WITH SUBJECT = 'Database backups';  
GO 
BACKUP DATABASE [AdventureWorks2014]  
TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

如需詳細資訊，請參閱 [備份加密](../relational-databases/backup-restore/backup-encryption.md)。


## <a name="next-steps"></a>後續步驟

如需 SQL Server 中的安全性功能詳細資訊，請參閱 [SQL Server 資料庫引擎和 Azure SQL Database 的資訊安全中心](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。
