---
title: 開始使用 Linux 上的 SQL Server 安全性 |Microsoft 文件
description: 本文說明一般的安全性動作。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.custom: sql-linux
ms.openlocfilehash: 0d7f2244a20f117d2886cdee59d54adfa4029721
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020331"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>在 Linux 上的 SQL Server 的安全性功能的逐步解說

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

如果您是剛接觸 SQL Server 的 Linux 使用者時，下列工作會引導您完成一些安全性工作。 這些不是唯一或特定 Linux，但它有助於讓您了解區域以進一步調查。 在每個範例中，會提供該區域的深入文件的連結。

>  [!NOTE]
>  下列範例會使用**AdventureWorks2014**範例資料庫。 如需有關如何取得並安裝這個範例資料庫的指示，請參閱 <<c0> [ 從 Windows 的 SQL Server 資料庫還原到 Linux](sql-server-linux-migrate-restore-database.md)。


## <a name="create-a-login-and-a-database-user"></a>建立登入和資料庫使用者 

授與其他人所建立的登入在 master 資料庫中使用的 SQL Server 存取[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)陳述式。 例如：

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

>  [!NOTE]
>  在前一個命令中，永遠使用強式密碼取代星號。

登入可以連接到 SQL Server，並具有 master 資料庫 （具有有限的權限） 存取。 若要連接至使用者資料庫，登入必須在資料庫層級，呼叫資料庫使用者對應的身分識別。 使用者只適用於每個資料庫，而且必須授與他們存取的每個資料庫中個別建立。 下列範例會將您移至 AdventureWorks2014 資料庫，並接著會使用[CREATE USER](../t-sql/statements/create-user-transact-sql.md)陳述式來建立名為 Larry 與名為 Larry 登入相關聯的使用者。 登入和使用者相關 （彼此對應），但它們是不同的物件。 登入是伺服器層級原則。 使用者是資料庫層級主體。

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- SQL Server 系統管理員帳戶可以連接到任何資料庫，而且可以建立多個登入和使用者在任何資料庫中。  
- 當有人建立資料庫時，它們成為資料庫擁有者，可以連接至該資料庫。 資料庫擁有者可以建立更多使用者。

稍後您可以授權其他登入，以便建立更多的登入，授與他們`ALTER ANY LOGIN`權限。 在資料庫內，您可以授權其他使用者授與它們建立更多使用者`ALTER ANY USER`權限。 例如：   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

登入 Larry 現在可以建立多個登入和使用者 Jerry 可以建立更多使用者。


## <a name="granting-access-with-least-privileges"></a>以最低權限的存取權授與

系統管理員和資料庫擁有者帳戶，將會連接至使用者資料庫的第一個人。 不過這些使用者會擁有所有可用的資料庫上的權限。 這是更多的權限的大部分使用者應該擁有比。 

當您剛開始使用時，您就可以使用內建指派權限的某些一般分類*固定資料庫角色*。 比方說，`db_datareader`固定的資料庫角色可以讀取所有的資料表，在資料庫中，但不做任何變更。 使用授與固定的資料庫角色的成員資格[ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md)陳述式。 下列範例會將使用者新增`Jerry`至`db_datareader`固定的資料庫角色。   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

如需固定的資料庫角色的清單，請參閱 <<c0> [ 資料庫層級角色](../relational-databases/security/authentication-access/database-level-roles.md)。

稍後，當您準備好要設定更精確地存取您的資料 （強烈建議），建立您自己使用的使用者定義資料庫角色[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)陳述式。 然後，將特定的細微權限指派給您的自訂角色。

例如，下列陳述式建立名為的資料庫角色`Sales`，授與`Sales`分組的能力，請參閱、 更新和刪除資料列`Orders`資料表，然後再將使用者加入`Jerry`到`Sales`角色。   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

如需有關權限系統的詳細資訊，請參閱[Getting Started with Database Engine 權限](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。


## <a name="configure-row-level-security"></a>設定資料列層級安全性  

[資料列層級安全性](../relational-databases/security/row-level-security.md)可讓您根據執行查詢的使用者資料庫中的資料列限制存取。 這項功能可用於確保客戶只能存取他們自己的資料或背景工作角色只能存取其部門相關的資料等案例。   

下列步驟逐步引導您設定兩個具有不同的資料列層級存取權的使用者`Sales.SalesOrderHeader`資料表。 

建立測試資料列層級安全性的兩個使用者帳戶：    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

授與讀取權限`Sales.SalesOrderHeader`兩個使用者的資料表：    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
建立新結構描述和內嵌資料表值函式。 此函數會傳回 1 中的資料列時`SalesPersonID`資料行比對識別碼`SalesPerson`登入或執行查詢的使用者如果是管理員使用者。   
   
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

建立安全性原則，做為篩選和封鎖述詞的資料表上加入函式：  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

執行下列命令來查詢`SalesOrderHeader`資料表每個使用者。 確認`SalesPerson280`只會看到 95 的資料列，從他們自己的銷售，`Manager`可以查看資料表中的所有資料列。  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
變更安全性原則，以停用原則。  現在兩個使用者可以存取所有資料列。 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>啟用動態資料遮罩

[動態資料遮罩](../relational-databases/security/dynamic-data-masking.md)可讓您完全或部分遮罩某些資料行來限制敏感性資料暴露的應用程式的使用者。 

使用`ALTER TABLE`陳述式來新增遮罩函式，以`EmailAddress`中的資料行`Person.EmailAddress`資料表： 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
建立新的使用者`TestUser`具有`SELECT`權限的資料表，然後執行查詢`TestUser`檢視遮罩的資料：   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
確認遮罩函式變更第一筆記錄，從電子郵件地址：
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>啟用透明資料加密

您的資料庫的一個威脅是有人會竊取您硬碟機上的資料庫檔案的風險。 這可能發生問題的員工的或包含的檔案 （例如膝上型電腦） 的電腦遭竊的動作取得提升權限的系統的存取權，入侵。

透明資料加密 (TDE) 會加密的資料檔案，因為它們儲存在硬碟機上。 Master 資料庫的 SQL Server database engine 的加密金鑰，以便資料庫引擎可以操作的資料。 無法讀取資料庫檔案，而不需要金鑰的存取權。 高層級的系統管理員可以管理、 備份，並重新建立索引鍵，所以可以移動資料庫，但只能由所選取人員。 當設定 TDE 時，`tempdb`資料庫也會自動加密。 

因為資料庫引擎可以讀取資料，透明資料加密無法防止未經授權的存取，他們可以直接讀取記憶體，或透過系統管理員帳戶來存取 SQL Server 之電腦的系統管理員。

### <a name="configure-tde"></a>設定 TDE

- 建立主要金鑰
- 建立或取得受到主要金鑰保護的憑證
- 建立資料庫加密金鑰，並使用憑證保護它
- 設定資料庫使用加密

需要設定 TDE`CONTROL`主要資料庫的權限和`CONTROL`使用者資料庫的權限。 通常系統管理員設定 TDE。 

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

SQL server 加密和解密作業排定在背景執行緒。 您可以使用本主題稍後出現之清單內的目錄檢視和動態管理檢視，以檢視這些作業的狀態。   

>  [!WARNING]
>  啟用了 TDE 的資料庫備份檔案也會使用資料庫加密金鑰來加密。 因此，當您要還原這些備份時，保護資料庫加密金鑰的憑證必須可以使用。 這表示，除了備份資料庫以外，您也必須確定可維護伺服器憑證的備份，以免資料遺失。 如果此憑證無法再使用，就會造成資料遺失。 如需詳細資訊，請參閱 [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  

如需 TDE 的詳細資訊，請參閱[透明資料加密 (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md)。   


## <a name="configure-backup-encryption"></a>設定備份加密
SQL Server 必須能夠建立備份時加密資料。 藉由指定的加密演算法和加密程式 （憑證或非對稱金鑰） 時建立的備份，您可以建立已加密的備份檔案。    
  
> [!WARNING]  
>  備份憑證或非對稱金鑰是非常重要的，而且最好與其用以加密的備份檔案存放於不同位置。 若沒有憑證或非對稱金鑰，您將無法還原備份，而此備份檔案將無法使用。 
 
 
下列範例會建立憑證，，，然後建立受憑證保護的備份。
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

如需詳細資訊，請參閱 <<c0> [ 備份加密](../relational-databases/backup-restore/backup-encryption.md)。


## <a name="next-steps"></a>後續的步驟

如需詳細的 SQL Server 的安全性功能的相關資訊，請參閱[SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。
